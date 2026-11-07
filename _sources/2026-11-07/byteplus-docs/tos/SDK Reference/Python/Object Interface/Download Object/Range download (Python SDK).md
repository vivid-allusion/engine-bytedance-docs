---
title: "Range download (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scope-download-python-sdk"
---

If you only need to retrieve part of the data in an object, you can use range download to download data within a specified range. This article describes range download.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos: GetObject` permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* For a bucket with versioning enabled, you must have the `tos: GetObjectVersion` permission when downloading the specified object version. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* If an application downloads a large number of the same object at the same time, your access speed will be limited by TOS bandwidth and geography. It is recommended that you use CDN products to improve performance while also reducing your costs.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5oyH5a6aLXN0YXJ0LWVuZC3kuIvovb3lr7nosaE="></span>
### **Download partial data of an object using start and end offsets**

The following code downloads a portion of the object `object-test` from the bucket `bucket-test` by specifying the range_start and range_end parameters.

```python
import os
import tos

# # Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Get an object stream by specifying the start and end range for downloading an object. The object already exists and has a size of 1048576 bytes.
    object_stream = client.get_object(bucket_name, object_key, range_start=0, range_end=1048576)
    # Iterate to read the content of the object.
    for content in object_stream:
        print(content)
    client.get_object(bucket_name, object_key, range_start=2, range_end=1)
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


<span id=".5oyH5a6aLXJhbmdlLeS4i-i9veWvueixoQ=="></span>
### **Download partial data of an object using the range header**

The following code downloads a portion of the object `object-test` from the bucket `bucket-test` by specifying the HTTP Range header.

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
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Download an object by specifying a range, from the 100th byte to the end
    client.get_object(bucket_name, object_key, range='bytes=100-')
    # Throw an exception if an invalid range is returned
    client.get_object(bucket_name, object_key, range='bytes=100-99')
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

The following code is used to configure the progress bar during partial downloads.

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
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    def percentage(consumed_bytes, total_bytes, rw_once_bytes, type: DataTransferType):
        if total_bytes:
            rate = int(100 * float(consumed_bytes) / float(total_bytes))
            print("rate:{}, consumed_bytes:{},total_bytes{}, rw_once_bytes:{}, type:{}".format(rate, consumed_bytes,
                                                                                               total_bytes,                                                                                               rw_once_bytes, type))
    # An object with a size of 1048577 bytes already exists, and it will be downloaded by specifying the Start/End download object.
    object_stream = client.get_object(bucket_name, object_key, range_start=0, range_end=1048576, data_transfer_listener=percentage)
    # Iteratively read the content of the object.
    for content in object_stream:
        print(content)
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

The following code is used to configure the client\-side rate limiting during partial downloads.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Limiting the download speed of the client using the optional parameter rate_limiter
    # The TOS Python SDK implements client-side rate limiting using the basic token bucket algorithm, where rate is the rate at which tokens are sent and capacity is the total capacity.
    # The following configuration signifies an average upload speed of 5 Mb/s and a maximum download speed of 10 + 5 Mb/s.
    rate_limiter = tos.RateLimiter(rate=5 * 1024 * 1024, capacity=10 * 1024 * 1024)
    # Downloading the object by specifying the Start/End range. There is already an object of size 1048577 bytes.
    object_stream = client.get_object(bucket_name, object_key, range_start=0, range_end=1048576, rate_limiter=rate_limiter)
    # Iteratively reading the object content.
    for content in object_stream:
        print(content)
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

For API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
