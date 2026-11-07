---
title: "Resumable upload (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resumption-python-sdk"
---

Before uploading the file to TOS by resuming the upload through a breakpoint, you can set the sharding size, the number of threads to upload the sharding, the speed limit on the client side when uploading, the event callback function, etc. At the same time, the task can also be cancelled during the execution of the resume upload task at the breakpoint. If the file upload fails due to network abnormalities, etc., you can resume uploading the unfinished part from the breakpoint.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before uploading an object, you must have `tos: PutObject`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* When uploading an object, the object name must meet certain specifications. For details, see [Common Concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for mass storage, which stores object index data in internal partition. To scale out the maximum throughput when you upload and download objects and reduce the probability of hotspot partitions, please avoid lexicographically increasing object naming.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing object. If versioning is enabled in your bucket, the original object is preserved and a new version number is generated to identify the newly uploaded object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5aSx6LSl5ZCO6YeN5YWl5LiK5Lyg"></span>
### **Reenter upload after failure**

The following code is used to resume uploading with a breakpoint. Upload the local file to the object\-test object in the target bucket bucket\-test`object-test object in the target bucket bucket-test`. If TosClientError is thrown during uploading and the reason for the error is a network timeout, the user can call `upload_file`with the same parameters to achieve breakpoint reentry uploading.

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
filename = "/usr/local/testfile.txt"
try:
    # Create TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # The optional parameter part_size can be used to specify the size of each part
    # The enable_checkpoint parameter can be used to enable or disable the checkpoint feature
    # The task_num parameter can be used to set the number of threads
    client.upload_file(bucket_name, object_key, filename,
                       # Set the number of threads for resumable upload, default is 1
                       task_num=3,
                       # Set the chunk size for resumable upload, default is 20mb
                       part_size=1024 * 1024 * 5)
                  
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
### **Processing progress bar**

The following code is used to configure the breakpoint continuation upload progress bar function.

```python
import os
import tos

from tos import DataTransferType

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
filename = "/usr/local/testfile.txt"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    def percentage(consumed_bytes: int, total_bytes: int, rw_once_bytes: int, type: DataTransferType):
        if total_bytes:
            rate = int(100 * float(consumed_bytes) / float(total_bytes))
            print("rate:{}, consumed_bytes:{},total_bytes{}, rw_once_bytes:{}, type:{}".format(rate, consumed_bytes,
                                                                                               total_bytes,
                                                                                               rw_once_bytes, type))


    # The optional parameter part_size can be used to specify the size of each chunk.
    # The enable_checkpoint parameter can be used to enable or disable the feature of resumable uploads.
    # The task_num parameter can be used to set the number of threads.
    client.upload_file(bucket_name, object_key, filename,
                       # Set the number of threads for resumable upload, default is 1
                       task_num=3,
                       # Set the size of each part for resumable upload, default is 20mb
                       part_size=1024 * 1024 * 5,
                       # Set the progress bar callback function for resumable upload
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
### **Handling event callbacks**

The following code is used to customize the breakpoint continuation upload callback function.

```python
import os
import tos

from tos import UploadEventType
from tos.models2 import PartInfo

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
filename = "/usr/local/testfile.txt"
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Custom event callback handler function
    def upload_event(type: UploadEventType, err: Exception, bucket: str, key: str, upload_id: str, file_path: str,
                     checkpoint_file: str, part: PartInfo):
        print(type, err, bucket, key, upload_id, file_path, checkpoint_file, part)

    # The optional parameter part_size can be used to specify the size of each chunk.
    # The enable_checkpoint parameter can be used to enable or disable the feature of resuming from checkpoints.
    # The task_num can be set to determine the number of threads.
    client.upload_file(bucket_name, object_key, filename,
                       # Set the number of threads for resumable upload, default is 1
                       task_num=3,
                       # Set the chunk size for resumable upload, default is 5mb
                       part_size=1024 * 1024 * 5,
                       # Enable resumable upload, default is enabled
                       enable_checkpoint=True,
                       # Configure custom event callbacks
                       upload_event_listener=upload_event)
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
### **Processing client side speed limit**

The following code is used to set the client side speed limit for a breakpoint continuation upload.

```python
import os
import tos


from tos import UploadEventType
from tos.models2 import PartInfo
# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
filename = "/usr/local/testfile.txt"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # The TOS Python SDK implements client throttling using the basic token bucket algorithm, where rate is the rate at which tokens are sent and capacity is the total capacity.
    # The following configuration means an average upload speed of 5mb/s, with a maximum supported upload speed of 10 + 5 mb/s.
    rate_limiter = tos.RateLimiter(5 * 1024 * 1024, 10 * 1024 * 1024)
    client.upload_file(bucket_name, object_key, filename,
                       # Set the number of threads for resumable upload to 3 by default.
                       task_num=3,
                       # Set the size of each part for resumable upload to 5mb by default.
                       part_size=1024 * 1024 * 5,
                       # Enable resumable upload by default.
                       enable_checkpoint=True,
                       # rate_limiter is an optional parameter used for client-side rate limiting.
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

The following code is used to cancel an ongoing breakpoint continuation upload task at runtime.

```python
import time
from threading import Thread

import os
import tos
from tos.checkpoint import CancelHook
# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# Local file full path, for example usr/local/testfile.txt
filename = "/usr/local/testfile.txt"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Inherit the CancelHook class to implement the function of canceling breakpoint resumable upload tasks.
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

    upload_out = client.upload_file(bucket_name, object_key, file_path=filename,
                                    # Set the function for canceling resumable upload.
                                    cancel_hook=cancel,
                                    # Set the number of threads for uploading files, default is 1.
                                    task_num=3,
                                    # Set the file chunk size, default is 20MB, minimum is 5MB.
                                    part_size=1024 * 1024 * 5)
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
