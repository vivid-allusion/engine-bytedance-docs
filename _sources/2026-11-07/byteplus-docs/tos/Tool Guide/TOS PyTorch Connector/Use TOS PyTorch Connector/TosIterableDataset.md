---
title: "TosIterableDataset"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/TosIterableDataset"
---

This article explains how to build a Dataset using TosIterableDataset.

<span id="bb85e0d7"></span>
## Prerequisites

TOS PyTorch Connector must be installed and configured. For detailed instructions, see [installing TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Install_TOS_PyTorch_Connector) and [configuring TOS PyTorch Connector](https://docs.byteplus.com/docs/tos/Configure_TOS_PyTorch_Connector).

<span id="ddc913cc"></span>
## Build Dataset

<span id="94a2c8d3"></span>
### Build Method

There are two ways to build a Dataset using TosIterableDataset:


* TOS_URI prefix: suitable when TOS storage paths follow a consistent pattern.

* List of TOS_URIs: Suitable when TOS storage paths are distinct but scattered.


<span id="a050bf31"></span>
### Build Dataset using TOS_URI prefix

The following example demonstrates building a Dataset using TosIterableDataset’s from_prefix() method.

```Python
class TosIterableDataset(torch.utils.data.IterableDataset):
    @classmethod
    def from_prefix(cls, prefix: str, *, region: str, endpoint: Optional[str] = None,
                transform: Callable[[TosObjectReader], Any] = None,
                cred: Optional[CredentialProvider] = None,
                client_conf: Optional[TosClientConfig] = None,
                sharding:bool = False,
                use_native_client: bool = True,
                reader_type: Optional[ReaderType] = None,
                buffer_size: Optional[int] = None,
                enable_crc: bool = True,
                prefetch_concurrency: int = 0):
        ... 
```


<span id="6be3d63f"></span>
### Build Dataset from TOS_URI list

The following example shows how to build a Dataset using the from_urls() method of TosIterableDataset.

```Python
class TosIterableDataset(torch.utils.data.IterableDataset):
    @classmethod
    def from_urls(cls, urls: Union[str, Iterator[str]], *, region: str, endpoint: Optional[str] = None,
              transform: Callable[[TosObjectReader], Any] = None,
              cred: Optional[CredentialProvider] = None,
              client_conf: Optional[TosClientConfig] = None,
              sharding: bool = False,
              use_native_client: bool = True,
              reader_type: Optional[ReaderType] = None,
              buffer_size: Optional[int] = None,
              enable_crc: bool = True,
              prefetch_concurrency: int = 0):
        ...
```


<span id="c7bb5471"></span>
## Parameter description


|Parameter list |Required |Condition operator type |Example value |Description |
|---|---|---|---|---|
|urls |Yes |str ｜ Iterator[str] |['tos://bucket/key1', 'tos://bucket/key2']<br><br> |The format for a single URL is tos://{bucketname}/{objectname}. |
|prefix |Yes |str |tos://bucket/prefix |Format is tos://{bucketname}/{prefix}. |
|region |Yes |str |cn\-beijing |Volcano TOS region. |
|endpoint |No |str |http://tos\-cn\-beijing.volces.com |Volcano TOS Endpoint.<br><br> |
|transform |No |Callable[[TosObjectReader], Any] |```Python```<br>```def transform(item):```<br>```    data = item.read()```<br>```    return item.key, item.size```<br> |Transformation function. |
|cred |No |CredentialProvider |CredentialProvider('ak', 'sk') |Configure access credentials. |
|client_conf |No |TosClientConfig |\- |Connector parameter configuration. |
|sharding |No |bool |True |Enable multi\-process shared data mode. |
|reader_type |No |ReaderType |ReaderType.RANGED |TosObjectReader subtype, supported values:<br><br><br>* ReaderType.SEQUENTIAL: BufferedReader that caches all data.<br><br>* ReaderType.RANGED: buffered Reader that caches only the data of the corresponding block size.<br><br>* ReaderType.DIRECT: unbuffered Reader.<br><br><br> |
|buffer_size |No |int |8388608 |Effective when ReaderType is ReaderType.RANGED, representing the cache block size. |
|enable_crc |No |bool |True |Verify data consistency between read and write operations in upload and sequential read scenarios. |
|prefetch_concurrency |No |int |32 |Concurrency for preloading dataset reading. |


<span id="739987a0"></span>
## Code example

The following code example demonstrates creating a data loader with PyTorch; replace parameters such as region, endpoint, ak/sk with your required values.

```Python
from tostorchconnector import CredentialProvider
from tostorchconnector import TosIterableDataset
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
# Number of worker processes
NUM_WORKERS = 32
# Data Conversion Functions
def transform(item):
    data = item.read()
    return item.key, item.size

# Use TosIterableDataset.from_prefix to construct a dataset object from the specified dataset prefix
with TosIterableDataset.from_prefix(dataset_uri,
                                    region=region, endpoint=endpoint,
                                    transform=transform,
                                    sharding=True,
                                    cred=CredentialProvider(
                                        ak=ak,
                                        sk=sk)) as dataset:
    # Create a DataLoader based on the constructed dataset                                    
    train_loader = DataLoader(dataset=dataset, batch_size=BATCH_SIZE, num_workers=NUM_WORKERS, shuffle=False)
    #Use DataLoader for iterative training/reading
    for data in train_loader:
        print(data)                                        
```
