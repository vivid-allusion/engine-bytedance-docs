---
title: "Configure TOS PyTorch Connector"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Configure_TOS_PyTorch_Connector"
---

TOS PyTorch Connector requires valid access credentials to authenticate requests when interacting with TOS. This article details how to configure authentication information and parameters for TOS PyTorch Connector.

<span id="7a414603"></span>
## **Prerequisites**

TOS PyTorch Connector is installed. For detailed steps, see [Install TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Install_TOS_PyTorch_Connector).

<span id="bcde19f7"></span>
## Authentication methods

To ensure secure access to TOS services, you must provide valid access keys (AK/SK). TOS PyTorch Connector recommends passing credentials explicitly as parameters in the code. Pass the `cred` parameter directly when creating `TosMapDataset`, `TosIterableDataset`, or `TosCheckpoint` instances using the `CredentialProvider(ak=ak, sk=sk)` object. This method offers strong code portability and clear credential scope without polluting the global environment.

<span id="162ed776"></span>
## **Configure TOS PyTorch Connector**

Passing access keys directly to TOS PyTorch Connector via `CredentialProvider` is the most flexible and recommended method.

<span id="23aaaba4"></span>
### 1. Obtain access keys (AK/SK)

Access keys are your secure credentials for accessing TOS services. Keep them safe.


* How to obtain: log in to the [BytePlus Console](https://console.byteplus.com/home) and create or manage your Access Key on the **Access Control** \> **API Access Keys** page.

* Permission management: For security, strictly follow the principle of least privilege. Assign precise permission policies to your AK/SK. If your application only needs to read training data, grant it TOS read\-only permission `TosReadOnlyAccess`. This effectively prevents risks of data tampering or deletion caused by key leaks.


<span id="bbfc758a"></span>
### 2. Pass credentials

After obtaining AK/SK, you can pass them via the `cred` parameter when initializing the TOS PyTorch Connector class.

The basic configuration parameters are listed in the following table:


|configuration item |Required |Condition operator type |Example value |Description |
|---|---|---|---|---|
|region |Yes |str |cn\-beijing |Volcano TOS region. |
|endpoint |No |str |http://tos\-cn\-beijing.ivolces.com |Volcano TOS Endpoint<br><br> |
|cred |No |CredentialProvider |CredentialProvider('ak', 'sk') |Configure access credentials. |
|ak |Yes |str |AKLT\*\*\*\*\*\*\*\*\*\*\* |Access Key ID, that is, the key ID.<br><br>Parent node: cred. |
|sk |Yes |str |WIRk\*\*\*\*\*\*\*\*\*\*\* |Secret Access Key, the private access key.<br><br>Parent node: cred. |
|client_conf |No |TosClientConfig |\- |Connector parameter configuration. |
|part_size |No |int |8388608 |Shard size for reading and writing objects.<br><br>Parent node: client_conf. |
|max_retry_count |No |int |3 |Maximum retry count per request.<br><br>Parent node: client_conf. |
|shared_prefetch_tasks<br><br> |No |int |32 |Concurrent count of Range reads in sequential object reading scenarios.<br><br>Parent node: client_conf. |
|shared_upload_part_tasks |No |int<br><br> |32 |Set the number of concurrent segmented uploads for the object scene.<br><br>Parent node: client_conf. |
|enable_crc |No |bool |True |Verify data consistency between upload scenario and sequential read scenario for read\-write operations |


<span id="8c6eb69e"></span>
## Code examples

TOS PyTorch Connector offers ready\-to\-use datasets and checkpoints, enabling dataset loading and checkpoint access with simple configuration. Replace parameters like region, endpoint, and ak/sk with your own values.

<span id="34a8ac18"></span>
### Use dataset

```Python
from tostorchconnector import CredentialProvider
from tostorchconnector import TosMapDataset

# Dataset Conversion Function
def transform(item):
    data = item.read()
    return item.key, item.size

# dataset path
dataset_uri = 'tos://bucket/prefix'
region = 'cn-beijing'
# Volcano TOS endpoint
endpoint = 'http://tos-cn-beijing.ivolces.com'
ak = '<your-access-key>'
sk = '<your-secret-key>'

with TosMapDataset.from_prefix(dataset_uri,
                                    region=region, endpoint=endpoint,
                                    transform=transform,
                                    cred=CredentialProvider(
                                        ak=ak,
                                        sk=sk)) as dataset:

    # get dataset size
    dataset_len = len(dataset)
    # Randomly fetch a data item
    item = dataset[0]
    bucket = item.bucket
    key = item.key
    # Read all data
    content = item.read()
    print(len(content))
```


<span id="4d4567fc"></span>
### Use checkpoint

```Python
import torch
from tostorchconnector import TosCheckpoint, CredentialProvider

checkpoint_uri = 'tos://bucket/key'
region = 'cn-beijing'
endpoint = 'http://tos-cn-beijing.ivolces.com'
ak = '<your-access-key>'
sk = '<your-secret-key>'

with TosCheckpoint(region, endpoint, cred=CredentialProvider(ak, sk)) as checkpoint:
    # Write data
    with checkpoint.writer(checkpoint_uri) as writer:
        writer.write(b'hello')
        writer.write(b'world')
    
    # Read data
    with checkpoint.reader(checkpoint_uri) as reader:
        data = reader.read()
        assert data == b'helloworld'
```
