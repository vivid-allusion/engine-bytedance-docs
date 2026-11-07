---
title: "Append upload (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-python-sdk"
---

The object type created by append upload is Appendable Object, which can append and write data to the end of the object. The object types created by ordinary uploads and sharded uploads are of normal type (Normal Object), and data cannot be appended and written.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* You must have the `tos: PutObject`permission before appending an object, see [Overview](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must meet certain specifications. For details, see [Common Concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for mass storage. The internal partition stores object index data. In order to scale out the maximum throughput when uploading and downloading objects, and reduce the probability of hotspot partitions, please avoid using lexicographically increasing object naming.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing object. In the case of multiple versions of the bucket, the original object will be retained and a new version number will be generated to identify the newly uploaded object.

* The additional upload object does not support the Chunk\-Encoded request method. When you add the upload network stream, please iterate to obtain the data and then add the upload.


<span id=".6ZmQ5Yi26K-05piO"></span>
## Restriction statement

When using append uploads, the restrictions are as follows:


* The append object size cannot be greater than 5GiB.

* An object created by append upload. When a normal upload is performed, the object is overwritten and the object type is changed from append type to normal type. On the contrary, objects uploaded through normal do not support additional write operations.

* The object created by append upload does not support copying.

* If your bucket is in a state where multi\-version functionality is on or on, or if the bucket type is low\-frequency storage, you cannot append write objects.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".6L-95Yqg5LiK5Lyg5a2X56ym5rWB"></span>
### **Append upload character stream**

The following code is used to append the character stream to the object\-test object in the target bucket\-test`object-test object in the target bucket-test`.

```python
from io import StringIO

import os
import tos

from tos import RateLimiter

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Create a file of appendable type with the initial offset set to 0.
    # Set the access permission of the object to private by using the acl=tos.ACLType.ACL_Private parameter.
    # Set the storage type of the object to standard by using the storage_class=tos.StorageClassType.Storage_Class_Standard parameter.
    content_1 = 'Hello TOS A'
    content_2 = 'Hello TOS B'
    content_3 = 'Hello TOS C'

    # Append data, the offset is obtained from the previous response <next_append_offset>, or obtained from the content-length returned by head_object
    # Create a file type that can be appended, with the initial offset set to 0
    # Set the object's access permission to private using the acl=tos.ACLType.ACL_Private parameter
    # Set the object's storage type to storage_class=tos.StorageClassType.Storage_Class_Standard
    # For the first append write with offset=0, set pre_hash_crc64_ecma to 0
    # Passing in pre_hash_crc64_ecma ensures the integrity of the appended object data.
    result_1 = client.append_object(bucket_name, object_key, 0, content=StringIO(content_1), pre_hash_crc64_ecma=0)

    # Second append, the offset is obtained from the previous response <next_append_offset>, or obtained from the content-length returned by head_object.
    # Set offset=next_append_offset and set pre_hash_crc64_ecma as the hash_crc64_ecma from the upload response.
    # Passing pre_hash_crc64_ecma ensures the integrity of the appended object data.
    result_2 = client.append_object(bucket_name, object_key, result_1.next_append_offset, content=StringIO(content_2),
                                    pre_hash_crc64_ecma=result_1.hash_crc64_ecma)

    # Third append, the offset is obtained from the previous response <next_append_offset>, or obtained from the content-length returned by head_object.
    # Set offset=next_append_offset, set pre_hash_crc64_ecma as hash_crc64_ecma in the upload response
    # Passing pre_hash_crc64_ecma ensures the integrity of the appended object data.
    result_3 = client.append_object(bucket_name, object_key, result_2.next_append_offset, content=StringIO(content_3),
                                    pre_hash_crc64_ecma=result_2.hash_crc64_ecma)
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


<span id=".6L-95Yqg5LiK5LygLWJ5dGVzLea1gQ=="></span>
### **Append upload Bytes stream**

The following code appends the Bytes stream to the object\-test object in the target bucket\-test`object-test object in the target bucket-test`.

```python
from io import BytesIO

import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Create an appendable file with initial offset set to 0
    # Set the object's access permission to private using acl=tos.ACLType.ACL_Private parameter
    # Set the object's storage type to Standard using storage_class=tos.StorageClassType.Storage_Class_Standard parameter
    content_1 = b'Hello TOS A'
    content_2 = b'Hello TOS B'
    content_3 = b'Hello TOS C'

    # Append data, obtain the offset from the previous response <next_append_offset>, or from the content-length returned by head_object
    # Create an appendable file with initial offset set to 0
    # Set the object's access permission to private using acl=tos.ACLType.ACL_Private parameter
    # Set the object's storage type to Standard using storage_class=tos.StorageClassType.Storage_Class_Standard parameter
    # For the first append, set offset=0 and pre_hash_crc64_ecma does not need to be set
    # Passing pre_hash_crc64_ecma ensures the integrity of the appended object data
    result_1 = client.append_object(bucket_name, object_key, 0, content=BytesIO(content_1), pre_hash_crc64_ecma=0)

    # Second append, obtain the offset from the previous response <next_append_offset>, or from the content-length returned by head_object
    # Set offset=next_append_offset and set pre_hash_crc64_ecma to the hash_crc64_ecma from the upload response
    # Passing pre_hash_crc64_ecma ensures the integrity of the appended object data
    result_2 = client.append_object(bucket_name, object_key, result_1.next_append_offset, content=BytesIO(content_2),
                                    pre_hash_crc64_ecma=result_1.hash_crc64_ecma)

    # Third append, obtain the offset from the previous response <next_append_offset>, or from the content-length returned by head_object
    # Set offset=next_append_offset and set pre_hash_crc64_ecma to the hash_crc64_ecma from the upload response
    # Passing pre_hash_crc64_ecma ensures the integrity of the appended object data
    result_3 = client.append_object(bucket_name, object_key, result_2.next_append_offset, content=BytesIO(content_3),
                                    pre_hash_crc64_ecma=result_2.hash_crc64_ecma)
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


<span id=".6L-95Yqg5LiK5Lyg572R57uc5rWB"></span>
### **Append upload network stream**

The following code appends the network stream to the object\-test object in the target bucket \-test .`object-test object in the target bucket -test`.

```python
import requests
import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    next_append_offset = 0
    pre_hash_crc64_ecma = 0
    stream = requests.get('https://www.volcengine.com')
    for chunk in stream:
        # next_append_offset is the offset, which can be obtained from the previous response <next_append_offset>, or from the <content-length> obtained through head_object.
        # pre_hash_crc64_ecma is the crc64 value of the current data, which can be obtained from the previous response <hash_crc64_ecma>, or from the <hash_crc64_ecma> obtained through head_object.
        # Passing in pre_hash_crc64_ecma ensures the integrity of the appended object data.
        result = client.append_object(bucket_name, object_key, next_append_offset, content=chunk,
                                      pre_hash_crc64_ecma=pre_hash_crc64_ecma)
        next_append_offset = result.next_append_offset
        pre_hash_crc64_ecma = result.hash_crc64_ecma
    stream.close()
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


<span id=".6L-b5bqm5p2h5aSE55CG"></span>
### **Progress bar processing**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For data in the form of strings, bytes, and local files, progress bar functionality is supported. Data of types such as network streams cannot obtain the size of the uploaded content, so the callback does not return the overall size of the object.</div>


The following code is used to add a progress bar feature to the append upload process.

```python
import os
import tos

from tos import DataTransferType


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
bucket_name = "bucket-test"
object_key = "object-test"
try:
    def percentage(consumed_bytes: int, total_bytes: int, rw_once_bytes: int, type: DataTransferType):
        if total_bytes:
            rate = int(100 * float(consumed_bytes) / float(total_bytes))
            print("rate:{}, consumed_bytes:{},total_bytes{}, rw_once_bytes:{}, type:{}".format(rate, consumed_bytes,
                                                                                               total_bytes,
                                                                                               rw_once_bytes, type))


    client = tos.TosClientV2(ak, sk, endpoint, region)
    # data_transfer_listener is an optional parameter used to implement the progress bar feature.
    client.append_object(bucket_name, object_key, 0, content='a' * 1024 * 1024, data_transfer_listener=percentage)
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


<span id=".5a6i5oi356uv6ZmQ6YCf"></span>
### **Client side speed limit**

The following code is used to append the client side speed limit during upload.

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
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # The rate_limiter is an optional parameter used to implement client-side rate limiting.
    # The TOS Python SDK implements client-side rate limiting using the basic token bucket algorithm, where rate is the rate at which tokens are generated and capacity is the total capacity.
    # The following configuration means an average upload speed of 5mb/s and a maximum supported upload speed of 10 + 5 mb/s.
    rate_limiter = tos.RateLimiter(rate=1024 * 1024 * 5, capacity=10 * 1024 * 1024)
    client.append_object(bucket_name, object_key, 0, content='a' * 1024 * 1024, rate_limiter=rate_limiter)
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


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For additional uploaded API documentation, see [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject).
