---
title: "Topic"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Topic"
---

This article introduces the standard programming template, recommendations for optimizing performance, and configuration logs of the TOS PyTorch Connector.

<span id="b2a30fab"></span>
## Standard programming template

TosMapDataset, TosIterableDataset, and TosCheckpoint all implement `__enter__` and `__exit__` functions. Therefore, using context management programming is recommended, and TosException should be handled uniformly.

```Python
from tostorchconnector import TosMapDataset, TosIterableDataset, TosCheckpoint, CredentialProvider, TosException

# Dataset Path
dataset_uri = 'tos://bucket/prefix'
checkpoint_uri = 'tos://bucket/key'
region = 'cn-beijing'
#Volcano TOS Endpoint
endpoint = 'http://tos-cn-beijing.ivolces.com'
ak = '<your-access-key>'
sk = '<your-secret-key>'

#Use TosMapDataset
try:
    with TosMapDataset.from_prefix(dataset_uri,
                                        region=region, endpoint=endpoint,
                                        cred=CredentialProvider(
                                            ak=ak,
                                            sk=sk)) as dataset:
        for item in dataset:
            print(item.key)
except TosException as ex:
    print(str(ex))
    
#Using TosIterableDataset
try:
    with TosIterableDataset.from_prefix(dataset_uri,
                                        region=region, endpoint=endpoint,
                                        cred=CredentialProvider(
                                            ak=ak,
                                            sk=sk)) as dataset:
        for item in dataset:
            print(item.key)
except TosException as ex:
    print(str(ex))
    
#Use TosCheckpoint
try:
    with TosCheckpoint(region, endpoint, cred=CredentialProvider(ak, sk)) as checkpoint:
        #Using TosObjectWriter
        with checkpoint.writer(checkpoint_uri) as writer:
            writer.write(b'hello')
            writer.write(b'world')
        
        #Use TosObjectReader
        with checkpoint.reader(checkpoint_uri) as reader:
            data = reader.read()
            assert data == b'helloworld'
except TosException as ex:
    print(str(ex))
```


<span id="11020819"></span>
## Performance Optimization


1. Large object read/write scenarios: performance can be improved by configuring higher concurrency.

2. PyTorch dataset loading scenarios: performance can improve by configuring concurrent preloading.

3. Single object repeated read scenarios: performance can improve by selecting a cached Reader.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">ReaderType.SEQUENTIAL: cached Reader that caches all data in memory; suitable for scenarios involving repeated reads of a single object.</div>


* <div data-tips="true" data-tips-type="default">ReaderType.RANGED: cached Reader that caches only a limited amount of data in memory; suitable for repeated reads of small data chunks from a single object while controlling memory cache size.</div>


* <div data-tips="true" data-tips-type="default">ReaderType.DIRECT: a Reader without caching, suitable for one\-time read scenarios.</div>



&nbsp;

```Python
from tostorchconnector import CredentialProvider, TosClientConfig, ReaderType, TosIterableDataset, TosCheckpoint

region = 'cn-beijing'
# Volcano TOS Endpoint
endpoint = 'http://tos-cn-beijing.ivolces.com'
ak = '<your-access-key>'
sk = '<your-secret-key>'

#1. Large Object Read and Write Scenarios
shared_prefetch_tasks = 200
shared_upload_part_tasks = 200
with TosCheckpoint(region, endpoint, cred=CredentialProvider(ak, sk),    
    client_conf=TosClientConfig(shared_prefetch_tasks=shared_prefetch_tasks,
    shared_upload_part_tasks=shared_upload_part_tasks)) as checkpoint:
    pass 
    
#2. PyTorch Dataset Loading Scenario
dataset_uri = 'tos://bucket/prefix'
prefetch_concurrency = 256
with TosIterableDataset.from_prefix(dataset_uri, region=region, endpoint=endpoint,        cred=CredentialProvider(ak=ak, sk=sk), prefetch_concurrency=prefetch_concurrency) as dataset:
    pass

#3. Single Object Repeated Read Scenario
checkpoint_uri = 'tos://bucket/key'
with TosCheckpoint(region, endpoint, cred=CredentialProvider(ak, sk)) as checkpoint:
    with checkpoint.reader(checkpoint_uri, reader_type=ReaderType.SEQUENTIAL) as reader:
        pass
        
with TosIterableDataset.from_prefix(dataset_uri, region=region, endpoint=endpoint,        cred=CredentialProvider(ak=ak, sk=sk), reader_type=ReaderType.SEQUENTIAL) as dataset:
    pass
```


<span id="9a2d4252"></span>
## Configure Logs

The TOS PyTorch Connector supports daily rolling logs, which can be enabled through `tostorchconnector.init_log` as shown below.

```Python
from tostorchconnector import init_log
#Log levels
level = 'info'
#Log directory
directory = 'logs' 
#Log file name prefix
file_name_prefix = 'connector'
init_log(level, directory, file_name_prefix)
```


Since log initialization requires each process to initialize separately at startup, in multi\-process dataset loading scenarios, the `worker_init_fn` function must be used to configure log initialization for each process, as shown below:

```Python
from tostorchconnector import TosMapDataset, CredentialProvider, init_log

region = 'cn-beijing'
#Volcano TOS Endpoint
endpoint = 'http://tos-cn-beijing.ivolces.com'
ak = '<your-access-key>'
sk = '<your-secret-key>'
dataset_uri = 'tos://bucket/prefix'

def transform(item):
    data = item.read()
    return item.key, item.size

def worker_init_fn(x):
    init_log('info', 'logs', 'connector.log')
    
with TosMapDataset.from_prefix(dataset_uri, region=region, endpoint=endpoint,
                               cred=CredentialProvider(ak, sk),
                               transform=transform) as dataset:
    train_loader = DataLoader(dataset=dataset, batch_size=256, num_workers=32,
                              shuffle=True, worker_init_fn=worker_init_fn)
    for data in train_loader:
        print(data)
```
