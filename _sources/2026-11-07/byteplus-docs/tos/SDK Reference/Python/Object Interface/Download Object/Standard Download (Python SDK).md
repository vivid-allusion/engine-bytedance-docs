---
title: "Standard Download (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-download-python-sdk"
---

Standard download refers to downloading a single object through the get_object method, which supports downloading the object to memory and downloading it to a local device. At the same time, it supports progress bars, client\-side rate limiting, and rewriting HTTP response headers when downloading objects.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have the `tos: GetObject` permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* For a bucket with versioning enabled, you must have the `tos: GetObjectVersion` permission when downloading a specified object version. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* If an application downloads a large number of the same object at the same time, your access speed will be limited by TOS bandwidth and geography. It is recommended that you use CDN products to improve performance while also reducing your costs.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5LiL6L295a-56LGh5Yiw5YaF5a2Y"></span>
### **Download an object to memory**

The following code downloads the object `object-test` from the bucket `bucket-test` to memory.

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
    object_stream = client.get_object(bucket_name, object_key)
    # The get_object method returns an iterable object, which can be iterated to read the object content
    # for content in object_stream:
    #     print(content)
    # Alternatively, the read() method can be called directly to obtain the complete data in memory.
    print(object_stream.read())
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


<span id=".5LiL6L295Yiw5pys5Zyw5paH5Lu2"></span>
### **Download an object to a local device**

The following code downloads `object-test` from `bucket-test` to a local device.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
# /usr/local/file/test.txt
file_name = "your local file name"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # If file_name is a directory, download the object to this directory with the object name as the file name.
    client.get_object_to_file(bucket_name, object_key, file_name)
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


<span id=".5LiL6L295pe26YeN5YaZLWh0dHAt5ZON5bqU5aS0"></span>
### **Rewrite HTTP response headers when downloading**

The following code downloads `object-test` in `bucket-test` and rewrites the HTTP response header.

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
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # get_object returns an iterable object.
    object_stream = client.get_object(bucket_name, object_key,
                                      # Specify the Cache-Control response header returned by the server.
                                      response_cache_control='no-cache',
                                      response_content_disposition='attachment; filename=123.txt')
    # Iteratively read the contents of an object.
    for content in object_stream:
        print(content)

    # Print and rewrite response headers.
    print('response_cache_control', object_stream.cache_control)
    print('response_content_disposition', object_stream.content_disposition)
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


<span id=".6YWN572u6L-b5bqm5p2h"></span>
### **Configure progress bar**

The following code is used to configure the download progress bar.

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
try:

    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)


    def percentage(consumed_bytes, total_bytes, rw_once_bytes, type: DataTransferType):
        if total_bytes:
            rate = int(100 * float(consumed_bytes) / float(total_bytes))
            print("rate:{}, consumed_bytes:{},total_bytes{}, rw_once_bytes:{}, type:{}".format(rate, consumed_bytes,
                                                                                               total_bytes,
                                                                                               rw_once_bytes, type))


    # The download object progress bar can be configured through data_transfer_listener=percentage.
    object_stream = client.get_object(bucket_name, object_key, data_transfer_listener=percentage)
    # Iteratively read object content.
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

The following code is used to configure client\-side download rate limiting.

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
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # The download object client is limited in speed by the optional parameter rate_limiter.
    # The TOS Python SDK implements client-side rate limiting using the basic token bucket algorithm, where rate is the rate at which tokens are sent and capacity is the total capacity.
    # The following configuration means an average upload speed of 5 MB/s and a maximum download speed of 10 + 5 MB/s.
    rate_limiter = tos.RateLimiter(rate=5 * 1024 * 1024, capacity=10 * 1024 * 1024)
    object_stream = client.get_object(bucket_name, object_key, rate_limiter=rate_limiter)
    # Iteratively read object content
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

For API documentation on downloading objects,see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
