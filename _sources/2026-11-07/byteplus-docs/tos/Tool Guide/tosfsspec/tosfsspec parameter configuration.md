---
title: "tosfsspec parameter configuration"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_parameter_configuration"
---

This article mainly explains how to use tosfsspec to configure the core and advanced parameters of `TosFileSystem` and achieve high\-performance log initialization in multi\-process scenarios.

<span id="0775bdc5"></span>
## Core parameters of TosFileSystem

The core parameters of the `TosFileSystem` constructor complete authentication and establish a connection to Volcengine TOS.


|**Parameter** |**Item** |**Required** |**Description** |
|---|---|---|---|
|key |str |Yes |The Access Key ID (AK) of the BytePlus account. |
|secret |str |Yes |The secret access key (SK) of your BytePlus account. |
|region |str |Yes |The region where the target Bucket is located, for example, `cn-beijing`. |
|endpoint |str |No |TOS access domain name. If empty, the SDK generates it automatically based on the `region`; configure here for specific access points like intranet. |


<span id="c5e1b2fd"></span>
#### Example: basic initialization

```Python
import tosfsspec
import os
import tos

# Obtain AKSK information from environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')
# Initialize
fs = tosfsspec.TosFileSystem(
    key,secret,
    region='cn-beijing'
)
```


<span id="caa1b648"></span>
## Advanced parameters of TosFileSystem

Besides credentials, advanced parameters control sharding, concurrency, retries, and other behaviors.


|**Parameter** |**Item** |**Default value** |**Description** |
|---|---|---|---|
|part_size |int |8 \* 1024 \* 1024 (8MB) |The size of each part in chunked upload/copy, in bytes.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><code>part_size</code> must be at least 4MB (<code>4 * 1024 * 1024</code>).</div><br> |
|max_retry_count |int |3 |The maximum number of automatic retries for a failed request. |
|shared_prefetch_tasks |int |32 |Concurrency of internal prefetch tasks when reading data. |
|shared_upload_part_tasks |int |32 |Concurrency of multipart upload tasks. |
|shared_upload_part_copy_tasks |int |32 |Concurrency of multipart copy tasks. |
|enable_crc |bool |True |Enable CRC64 verification. After enabling, `tosfsspec` automatically performs data consistency checks after uploading and downloading to ensure data integrity. |


<span id="bee91697"></span>
### Example: custom advanced parameters

```Python
import tosfsspec
import os
import tos

# Set AK/SK via environment variables
key = os.getenv('TOS_ACCESS_KEY')
secret = os.getenv('TOS_SECRET_KEY')

# Customize part size to 16MB and increase concurrent tasks
fs_advanced = tosfsspec.TosFileSystem(
    key,secret,
    region='cn-beijing',
    part_size=16 * 1024 * 1024,  # 16MB
    shared_upload_part_tasks=64,
    enable_crc=False
)
```


<span id="498c5d42"></span>
## Log initialization

`tosfsspec` provides `init_logs()` to initialize high\-performance kernel log output. In multiprocessing scenarios, log initialization must be completed before each process starts execution.


|**Parameter** |**Item** |**Description** |
|---|---|---|
|directory |str |log file directory. |
|common_log |str |Prefix for the runtime log file name; the actual file name will include the process ID appended to this prefix. |
|common_level |str |Standard runtime log levels, such as `INFO` and `DEBUG`. |
|audit_log |str |The prefix of the audit log file name; the actual file name will append the process ID to this prefix. |
|audit_level |str |The audit log level, such as `INFO` or `DEBUG`. |


<span id="b5f5553d"></span>
#### Example: log initialization in multiprocessing scenarios

```Python
import multiprocessing
from tosfsspec import init_logs, TosFileSystem
def worker(index):
    init_logs(
        directory='./logs',
        common_log='tosfsspec-common',
        common_level='INFO',
        audit_log='tosfsspec-audit',
        audit_level='INFO',
    )
    fs = TosFileSystem(key='YOUR_ACCESS_KEY_ID', secret='YOUR_SECRET_ACCESS_KEY', region='cn-beijing')
    path = f'tos://your-bucket/log-demo/file-{index}.txt'
    with fs.open(path, 'wb') as f:
        f.write(f'worker {index}\n'.encode('utf-8'))

if __name__ == '__main__':
    processes = [multiprocessing.Process(target=worker, args=(i,)) for i in range(4)]
    for p in processes:
        p.start()
    for p in processes:
        p.join() 
```
