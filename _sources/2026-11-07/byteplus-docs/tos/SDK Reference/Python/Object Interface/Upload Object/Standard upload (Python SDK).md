---
title: "Standard upload (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-python-sdk"
---

A standard upload refers to the process of uploading a single object using the `put_object` method. This method supports four types of input: string (character stream), bytes (byte stream), network stream, and local file.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before uploading an object, you must have the `tos: PutObject` permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must meet certain specifications. For details, see [Common concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for mass storage, which stores object index data in internal partition. To scale out the maximum throughput when you upload and download objects and reduce the probability of hotspot partitions, please avoid lexicographically increasing object naming.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing object. If versioning is enabled in your bucket, the original object is preserved and a new version number is generated to identify the newly uploaded object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5LiK5Lyg5a2X56ym5rWB"></span>
### **Upload a character stream**

The following code uploads a character stream as the object `object-test` to the bucket `bucket-test`.

```python
from io import StringIO

import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
content = StringIO('Hello TOS')

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # If you set the file storage type (x-tos-storage-class) and access permissions (x-tos-acl) when uploading an object, please set the relevant parameters in put_object.
    # Users can customize metadata when uploading objects for custom management.
    # result = client.put_object(bucket_name, object_key, content=content, acl=tos.ACLType.ACL_Private, storage_class=tos.StorageClassType.Storage_Class_Standard, meta={'name': '张三', 'age': '20'})
    result = client.put_object(bucket_name, object_key, content=content)
    # HTTP status code
    print('http status code:{}'.format(result.status_code))
    # Request ID. The request ID is a unique identifier for this request. It is recommended to add this parameter to the log.
    print('request_id: {}'.format(result.request_id))
    # hash_crc64_ecma represents the 64-bit CRC value of the object, which can be used to verify the integrity of the uploaded object.
    print('crc64: {}'.format(result.hash_crc64_ecma))
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


<span id=".5LiK5LygYnl0ZXPmtYE="></span>
### **Upload a byte stream**

The following code uploads a byte stream as `object-test` to `bucket-test`.

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
content = BytesIO(b'Hello TOS')

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    result = client.put_object(bucket_name, object_key, content=content)
    # HTTP Status Code
    print('http status code:{}'.format(result.status_code))
    # Request ID. The request ID is a unique identifier for this request, it is recommended to add this parameter in the log
    print('request_id: {}'.format(result.request_id))
    # hash_crc64_ecma represents the 64-bit CRC value of the object, which can be used to verify the integrity of the uploaded object
    print('crc64: {}'.format(result.hash_crc64_ecma))
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


<span id=".5LiK5Lyg572R57uc5rWB"></span>
### **Upload a network stream**

The following code is used to upload a network stream as `object-test` to `bucket-test`. TOS treats network streams as iterable objects and uploads them as Chunked Encoding.

```python
from io import BytesIO

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
    # Create TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Use requests.get to retrieve network stream, Python SDK supports uploading network streams
    # requests.get returns an Iterable object, and Python SDK uploads it using Chunked Encoding.
    content = requests.get('https://www.volcengine.com')
    result = client.put_object(bucket_name, object_key, content=content)
    content.close()
    # HTTP status code
    print('http status code:{}'.format(result.status_code))
    # Request ID. Request ID is a unique identifier for this request, it is recommended to include this parameter in logs.
    print('request_id: {}'.format(result.request_id))
    # hash_crc64_ecma represents the 64-bit CRC value of the object, which can be used to verify the integrity of the uploaded object.
    print('crc64: {}'.format(result.hash_crc64_ecma))
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


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu2"></span>
### **Upload a local file**

The following code uploads a local file as `object-test` to `bucket-test`.

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
file_name = "/usr/local/test.txt"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Upload a local file to the destination bucket
    # file_name is the full path of the local file.
    client.put_object_from_file(bucket_name, object_key, file_name)
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


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu25aS5"></span>
### **Upload a local folder**

The following code is used to upload the local folder `test/` to the bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
# The current path of the local file.
file_dir = 'test/'
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)


    def upload_dir(root_dir):
        list = os.listdir(root_dir)
        for i in list:
            path = os.path.join(root_dir, i)
            if os.path.isdir(path):
                upload_dir(path)

            if os.path.isfile(path):
                client.put_object_from_file(bucket_name, path, path)


    upload_dir(file_dir)

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
### **Configure progress bar**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For data in the form of strings, bytes, and local files, progress bar functionality is supported. Data of types such as network streams cannot obtain the size of the uploaded content, so the callback does not return the overall size of the object.</div>


The following code uses a string as an example to illustrate how to use a progress bar.

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
try:
    def percentage(consumed_bytes: int, total_bytes: int, rw_once_bytes: int,
                   type: DataTransferType):
        if total_bytes:
            rate = int(100 * float(consumed_bytes) / float(total_bytes))
            print("rate:{}, consumed_bytes:{},total_bytes{}, rw_once_bytes:{}, type:{}".format(rate, consumed_bytes, total_bytes, rw_once_bytes, type))
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # data_transfer_listener is an optional parameter used to implement the progress bar feature.
    client.put_object(bucket_name, object_key, content='a' * 1024 * 1024, data_transfer_listener=percentage)
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


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### **Configure client\-side rate limiting**

The following code is used for client\-side rate limiting for a standard upload.

```python
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

    # The TOS Python SDK implements client rate limiting using the basic token bucket algorithm, where rate is the rate at which tokens are sent and capacity is the total capacity.
    # The following configuration means an average upload speed of 5 MB/s and a maximum supported download speed of 10 + 5 MB/s.
    rate_limiter = RateLimiter(rate=5 * 1024 * 1024, capacity=10 * 1024 * 1024)
    client.put_object(bucket_name, object_key, content='a' * 1024 * 1024, rate_limiter=rate_limiter)
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

For API documentation on uploading objects, see [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).
