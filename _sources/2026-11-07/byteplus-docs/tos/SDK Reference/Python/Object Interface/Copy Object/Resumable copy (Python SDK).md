---
title: "Resumable copy (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-continuation-copy-python-sdk"
---

The TOS Python SDK provides a resumable copy feature that is suitable for copying large objects within a single bucket or between two buckets in the same region. This feature uses a local checkpoint mechanism to track successfully copied parts. If a copy operation is interrupted due to network issues or machine failure, you can call the same API again to resume the copy process. Resumable copy splits the source object into multiple parts and supports concurrent copying. After all parts are successfully copied, they are merged into a complete object. You can configure the part size, the number of threads for concurrent copying, and event callback functions for the resumable copy task. You can also cancel the task while it is running.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* Cross\-region bucket copying is not supported when copying objects.

* To copy objects, the account must have read permission on the source object and write permission on the destination bucket.

* When copying an object, you can either retain all metadata (default) or specify new metadata. However, the ACL is not retained and is set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Example code

<span id=".5pat54K557ut5Lyg5aSN5Yi2"></span>
### **Resumable copy**

The following code copies the object `src_object_key` from the `src_bucket_name` bucket to the `bucket_name` bucket, sets the object name as `object_key`. It supports resuming the copy if it fails. If a network timeout error occurs during the copy process, you can call `resumable_copy_object` with the same parameters to resume the interrupted copy.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
# Name of the destination bucket
bucket_name = "bucket-test"
# New object key in the destination bucket after copy
object_key = "object-test"
# Name of the source bucket
src_bucket_name = "your src bucket name"
# Name of the source object
src_object_key = "your src object key"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.resumable_copy_object(bucket_name, object_key, src_bucket_name, src_object_key,
                                 # Configure the number of concurrent threads through task_num,
                                 task_num=3,
                                 # Configure the size of each partthrough part_size
                                 part_size=20 * 1024 * 1024)
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

The following code customizes the resumable copy callback function.

```python
import os
import tos
from tos import CopyEventType

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
# Name of the destination bucket
bucket_name = "bucket-test"
# New object key in the destination bucket after copy
object_key = "object-test"
# Name of the source bucket
src_bucket_name = "your src bucket name"
# Name of the source object
src_object_key = "your src object key"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    def copy_event(copy_event_type: CopyEventType, err, bucket, key, upload_id, src_bucket, src_key, src_version_id, checkpoint, copy_part):
        print(copy_event_type, err, bucket, key, upload_id, src_bucket, src_key, src_version_id, checkpoint, copy_part)

    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.resumable_copy_object(bucket_name, object_key, src_bucket_name, src_object_key,
                                 # Configure the number of concurrent threads through task num,
                                 task_num=3,
                                 # Configure the size of each part through part size
                                 part_size=20 * 1024 * 1024,
                                 copy_event_listener=copy_event)
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

The following code pauses or cancels the resumable copy task.

```python
import time
from threading import Thread

import os
import tos
from tos import CopyEventType
from tos.checkpoint import CancelHook

 Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
# Name of the destination bucket
bucket_name = "bucket-test"
# New object key in the destination bucket after copy
object_key = "object-test"
# Name of the source bucket
src_bucket_name = "your src bucket name"
# Name of the source object
src_object_key = "your src object key"
try:
    # Inherit the CancelHook class to implement the functionality of canceling resumable copy tasks.
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

    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.resumable_copy_object(bucket_name, object_key, src_bucket_name, src_object_key,
                                 # Configure the number of concurrent threads through task_num,
                                 task_num=3,
                                 # Configure the size of each part through part_size
                                 part_size=20 * 1024 * 1024,
                                 cancel_hook=cancel)
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
