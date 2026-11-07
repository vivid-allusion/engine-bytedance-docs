---
title: "TosMapDataset"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/TosMapDataset"
---

This article explains how to build a Dataset using TosMapDataset.

<span id="b5f75101"></span>
## Prerequisites

TOS PyTorch Connector must be installed and configured. For detailed instructions, see [installing TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Install_TOS_PyTorch_Connector) and [configuring TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Configure_TOS_PyTorch_Connector).

<span id="8d93a486"></span>
## Build Dataset

<span id="d0a27912"></span>
### Build methods

There are two methods to build a Dataset using TosMapDataset:


* The TOS_URI prefix: suitable for TOS storage paths with a consistent pattern.

* List of TOS_URI: suitable for scenarios where TOS storage paths are clear but scattered.


<span id="aa38ee45"></span>
### Build Dataset using the TOS_URI prefix

The following example demonstrates how to build a Dataset using the from_prefix() method of TosMapDataset.

```Python
class TosMapDataset(torch.utils.data.Dataset):
 #Build a Dataset using the from_prefix method
    @classmethod
    def from_prefix(cls, prefix: str, *, region: str, endpoint: Optional[str] = None,
                transform: Callable[[TosObjectReader], Any] = None,
                cred: Optional[CredentialProvider] = None,
                client_conf: Optional[TosClientConfig] = None,
                use_native_client: bool = True,
                reader_type: Optional[ReaderType] = None,
                buffer_size: Optional[int] = None,
                enable_crc: bool = True,
                prefetch_concurrency: int = 0):
        ... 
```


<span id="3229c3f2"></span>
### Build Dataset using a list of TOS_URI

The following example demonstrates how to build a Dataset using the from_urls() method of TosMapDataset.

```Python
class TosMapDataset(torch.utils.data.Dataset):
#Build a Dataset using the from_urls method
    @classmethod
    def from_urls(cls, urls: Union[str, Iterator[str]], *, region: str, endpoint:     Optional[str] = None,
              transform: Callable[[TosObjectReader], Any] = None,
              cred: Optional[CredentialProvider] = None,
              client_conf: Optional[TosClientConfig] = None,
              use_native_client: bool = True,
              reader_type: Optional[ReaderType] = None,
              buffer_size: Optional[int] = None,
              enable_crc: bool = True,
              prefetch_concurrency: int = 0)
        ...   
```


<span id="32043f94"></span>
## Parameter description


|parameter list |Required |Condition operator type |Example value |Description |
|---|---|---|---|---|
|urls |Yes |str ｜ Iterator[str] |['tos://bucket/key1', 'tos://bucket/key2']<br><br> |The format of a single URL is tos://{bucketname}/{objectname}. |
|prefix |Yes |str |tos://bucket/prefix |Format: tos://{bucketname}/{prefix}. |
|region |Yes |str |cn\-beijing |Volcano TOS Region. |
|endpoint |No |str |http://tos\-cn\-beijing.ivolces.com |Volcano TOS Endpoint.<br><br> |
|transform |No |Callable[[TosObjectReader], Any] |```Python```<br>```def transform(item):```<br>```    data = item.read()```<br>```    return item.key, item.size```<br> |Conversion function. |
|cred |No |CredentialProvider |CredentialProvider('ak', 'sk') |Access key configuration. |
|client_conf |No |TosClientConfig |\- |Connector parameter configuration. |
|reader_type |No |ReaderType |ReaderType.RANGED |TosObjectReader subtype, supported values:<br><br><br>* ReaderType.SEQUENTIAL: cached reader that caches all data.<br><br>* ReaderType.RANGED: cached reader that caches only the cache block size of data.<br><br>* ReaderType.DIRECT: Reader without cache.<br><br><br> |
|buffer_size |No |int |8388608 |Effective when ReaderType is ReaderType.RANGED; represents the cache block size. |
|enable_crc |No |bool |True |Verify data consistency between uploading scenarios and sequential reading scenarios in read\-write operations. |
|prefetch_concurrency |No |int |32 |Concurrency for preloading dataset reads. |


<span id="a7d09650"></span>
## Code example

The following code example shows how to create a data loader in PyTorch; replace region, endpoint, ak/sk, and other parameters with your required values.

```Python
from tostorchconnector import CredentialProvider
from tostorchconnector import TosMapDataset
from torch.utils.data import DataLoader

# Dataset Path
dataset_uri = 'tos://bucket/prefix'
region = 'cn-beijing'
# Volcano TOS Endpoint
endpoint = 'http://tos-cn-beijing.ivolces.com'
ak = '<your-access-key>'
sk = '<your-secret-key>'

# Data Batch Size
BATCH_SIZE = 256
# Number of Worker Processes
NUM_WORKERS = 32
# Data Conversion Functions
def transform(item):
    data = item.read()
    return item.key, item.size
    
# Use TosMapDataset.from_prefix to construct a dataset object from the specified dataset prefix
with TosMapDataset.from_prefix(dataset_uri,
                                    region=region, endpoint=endpoint,
                                    transform=transform,
                                    cred=CredentialProvider(
                                        ak=ak,
                                        sk=sk)) as dataset:
 #Create DataLoader based on the constructed dataset                                   
    train_loader = DataLoader(dataset=dataset, batch_size=BATCH_SIZE, num_workers=NUM_WORKERS, shuffle=True)
  # Use DataLoader for iterative training/reading
    for data in train_loader:
        print(data)                                        
```
