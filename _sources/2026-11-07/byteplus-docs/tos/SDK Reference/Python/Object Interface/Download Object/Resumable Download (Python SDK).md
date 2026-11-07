---
title: "Resumable Download (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-download-python-sdk"
---

Download failures may occur when downloading large objects due to network fluctuations or other issues. The TOS Python SDK provides a retry mechanism to ensure stability during these downloads. However, there may still be cases where the download cannot be completed, even after multiple retries. To address this, the TOS Python SDK offers resumable downloads, which allow downloads to resume after a failure. Resumable downloads split the object into multiple parts and support concurrent downloading. Once all parts are downloaded, they are merged into a complete file. Before using the resumable download feature to download an object to a local device, you can configure parameters such as part size, the number of threads for concurrent downloading, client\-side bandwidth throttling, and callback functions. You can also cancel the resumable download task while it is executing.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos: GetObject`permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* For a bucket with versioning enabled, you must have the `tos: GetObjectVersion`permission when downloading the specified object version. For details,see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* If an application downloads a large number of the same object at the same time, your access speed will be limited by TOS bandwidth and geography. It is recommended that you use CDN products to improve performance while also reducing your costs.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5aSx6LSl5ZCO6YeN5YWl"></span>
### **Resume after failure**

The following code is used to resume the download of the object `object-test` in the bucket `bucket-test` to the local device. If a TosClientError exception is thrown during the download process and the error is network timeout, you can call download_file with the same parameters to resume download.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
file_path = "/usr/local/testfile.txt"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.download_file(bucket_name, object_key, file_path,
                         # Configure the part size for downloading using the optional parameter part_size, with a default value of 20 MB.
                         part_size=1024 * 1024 * 20,
                         # Configure the number of threads for downloading the parts using the optional parameter task_num, with a default value of 1.
                         task_num=3)
except tos.exceptions.TosClientError as e:
    # Operation failed, catch client error, usually caused by invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, catch server error, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # request id can be used to locate specific issues, it is strongly recommended to save it in the log.
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<span id=".5aSE55CG6L-b5bqm5p2h"></span>
### **Configure progress bar**

The following code is used to configure the resumable download progress bar function.

```python
import os
import tos
from tos import DataTransferType

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
file_path = "/usr/local/testfile.txt"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    def percentage(consumed_bytes, total_bytes, rw_once_bytes, type: DataTransferType):
        if total_bytes:
            rate = int(100 * float(consumed_bytes) / float(total_bytes))
            print("rate:{}, consumed_bytes:{},total_bytes{}, rw_once_bytes:{}, type:{}".format(rate, consumed_bytes,
                                                                                               total_bytes,
                                                                                               rw_once_bytes, type))
    client.download_file(bucket_name, object_key, file_path,
                         # Configure the size of each part during download using the optional parameter part_size. The default size is 20 MB.
                         part_size=1024 * 1024 * 20,
                         # Configure the number of threads for downloading parts using the optional parameter task_num. The default number is 1.
                         task_num=3,
                         # Configure the progress bar using the optional parameter data_transfer_listener.
                         data_transfer_listener=percentage)
except tos.exceptions.TosClientError as e:
    # Operation failed, catch client error, usually caused by invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, catch server error, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # request id can be used to locate specific issues, it is strongly recommended to save it in the log.
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<span id=".5aSE55CG5LqL5Lu25Zue6LCD"></span>
### **Configure event callbacks**

The following code is used to customize the resumable download callback function.

```python
import os
import tos
from tos import DownloadEventType

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
file_path = "/usr/local/testfile.txt"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # User-defined event callback function
    def download_event(type: DownloadEventType, err, bucket, key, version_id, file_path, checkpint_file, tmp_file,
                       download_part):
        print(type, err, bucket, key, version_id, file_path, checkpint_file, tmp_file, download_part)
    client.download_file(bucket_name, object_key, file_path,
                         # Configure the download part size with the optional parameter part_size, default is 20 MB.
                         part_size=1024 * 1024 * 20,
                         # Configure the number of threads for downloading parts with the optional parameter task_num, default is 1.
                         task_num=3,
                         # Configure the progress bar with the optional parameter data_transfer_listener.
                         download_event_listener=download_event)
except tos.exceptions.TosClientError as e:
    # Operation failed, catch client error, usually caused by invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, catch server error, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # request id can be used to locate specific issues, it is strongly recommended to save it in the log.
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<span id=".5aSE55CG5a6i5oi356uv6ZmQ6YCf"></span>
### **Configure client side rate limiting**

The following code is used to set the resumable download client side rate limiting.

```python
import os
import tos
from tos import DownloadEventType

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
file_path = "/usr/local/testfile.txt"
try:

    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # The download object client is limited in speed by the optional parameter rate_limiter.
    # The TOS Python SDK implements client rate limiting using the basic token bucket algorithm, where rate is the rate at which tokens are sent and capacity is the total capacity.
    # The following configuration means an average upload speed of 5 MB/s and a maximum supported download speed of 10 + 5 MB/s.
    rate_limiter = tos.RateLimiter(rate=5 * 1024 * 1024, capacity=10 * 1024 * 1024)

    client.download_file(bucket_name, object_key, file_path,
                         # Configure the download chunk size during downloading with the optional parameter part_size, default is 20 MB.
                         part_size=1024 * 1024 * 20,
                         # Configure the number of threads for downloading chunks with the optional parameter task_num, default is 1.
                         task_num=3,
                         # Configure the client rate limiter with the optional parameter rate_limiter.
                         rate_limiter=rate_limiter)
except tos.exceptions.TosClientError as e:
    # Operation failed, catch client error, usually caused by invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, catch server error, detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # request id can be used to locate specific issues, it is strongly recommended to save it in the log.
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<span id=".5Y-W5raI5py65Yi2"></span>
### **Cancellation mechanism**

The following code is used to cancel an ongoing resumable download task.

```python
import time
from threading import Thread

import os
import tos
from tos.checkpoint import CancelHook
from tos.exceptions import TosClientError

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
file_path = "/usr/local/testfile.txt"

# Create a TosClientV2 object to perform operations on buckets and objects.
client = tos.TosClientV2(ak, sk, endpoint, region)


# Inherit the CancelHook class to implement the functionality of canceling resumable download tasks.
class MyCancel(CancelHook):
    def cancel(self, is_abort: bool):
        # When is_abort is true, delete the context information and abort the segmented upload task. When is_abort is false, only interrupt the current execution.
        # When overriding the cancel method, it is necessary to call the cancel method of the parent class.
        # Simulate canceling the task after 10 seconds.
        time.sleep(10)
        super(MyCancel, self).cancel(is_abort=is_abort)
        print('some user define')


cancel = MyCancel()

t1 = Thread(target=cancel.cancel, args=(False,))
t1.start()

try:
    client.download_file(bucket_name, object_key, file_path,
                         # Configuring the download part size with the optional parameter part_size, default is 20 MB
                         part_size=1024 * 1024 * 20,
                         # Configuring the number of threads for downloading parts with the optional parameter task_num, default is 1
                         task_num=3,
                         # Implementing cancellation mechanism with the optional parameter cancel_hook
                         cancel_hook=cancel)
except TosClientError as e:
    # If the resumable download task is canceled, it will throw a TosClientError with the message 'the task is canceled'.
    if e.message == 'the task is canceled':
        print('the task is canceled')
except Exception as e:
    print(e)
```
