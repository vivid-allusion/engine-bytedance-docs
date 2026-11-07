---
title: "List objects (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-python-sdk"
---

This article explains how to use ListObject to list all objects in a specified bucket, files with a specified prefix, files, and subdirectories under a specified directory.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* The ListObjects interface has been updated to ListObjectsType2. Developers are strongly recommended to use ListObjectsType2. To ensure backward compatibility, TOS continues to support the ListObjects interface.

* To use ListObjects V2, you must have the `tos:ListBucket` permission. For details, see [IAM policy overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


|**Parameter** |**Description** |
|---|---|
|prefix |Prefix for this query's results. |
|delimiter |Character to group object names. |
|marker |Specifies where to start listing objects. Lists objects in alphabetical order after this value. Usually the next_marker value returned from the last request. |
|max_keys |Returns the maximum number of objects listed, default is 1000.<br><br>Value range: greater than 0 and less than or equal to 1000 |


<span id=".56S65L6L5Luj56CB"></span>
## Example code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Simple listing**

The following code lists 10 objects in the specified bucket.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # The example code for listing 10 files in a bucket is as follows:
    result = client.list_objects(bucket_name, max_keys=10)
    for item in result.contents:
        print(item.key)
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


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paginated listing**

The following code paginates the listing of objects in bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # List the first 1000 objects in the paginated bucket.
    result = client.list_objects(bucket_name)
    for item in result.contents:
        print(item.key)
    # List the next 1000 objects in pages.
    if result.is_truncated:
        result = client.list_objects(bucket_name, marker=result.next_marker)
        for item in result.contents:
            print(item.key)
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


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with the specified prefix**

The following code lists all objects in bucket `bucket-test` with the specified prefix.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
prefix = "your prefix"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)

    is_truncated = True
    marker = ""
    # List all objects with a specified prefix.
    while is_truncated:
        result = client.list_objects(bucket_name, prefix=prefix, marker=marker)
        for item in result.contents:
            print(item.key)
        is_truncated = result.is_truncated
        marker = result.next_marker
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


<span id=".5YiX5Li-5qG25YaF5omA5pyJ5a-56LGh"></span>
### **List all objects in a bucket**

The following code lists all objects in the specified bucket `bucket-test`.

```python
import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # List all objects under a specified bucket.
    truncated = True
    marker = ''
    while truncated:
        result = client.list_objects(bucket_name, marker=marker)
        for item in result.contents:
            print(item.key)
        truncated = result.is_truncated
        marker = result.next_marker
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


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### **List files and subdirectories under the specified directory**

TOS only has the concept of objects; directories can be simulated by creating an object of size 0 that ends with a slash /.

The directory function can be simulated using the parameters `delimiter` and `prefix`:


* First, set `delimiter` to`/`Set `prefix` to empty to return objects and subdirectory information in the root directory.

* Then set `delimiter` to`/`Set `prefix` to a subdirectory to return objects and subdirectories within that subdirectory.


The following code lists the objects and subdirectories under the specified directory of bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'

try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Add subdirectories named fun1, fun2, and fun3 to the Bucket, along with a file named test.
    client.put_object(bucket_name, "fun1/")
    client.put_object(bucket_name, "fun1/test/")
    client.put_object(bucket_name, "fun1/obj.txt")
    client.put_object(bucket_name, "fun2/")
    client.put_object(bucket_name, "fun3/")
    client.put_object(bucket_name, "test")

    # List the folders and files in the root directory.
    marker = ''
    is_truncated = True
    while is_truncated:
        out = client.list_objects(bucket_name, delimiter="/", marker=marker)
        # common_prefixes returns the subdirectories under the root directory.
        for prefix in out.common_prefixes:
            print('subDir', prefix.prefix)

        # The contents return the objects in the root directory.
        for content in out.contents:
            print('file', content.key)
        is_truncated = out.is_truncated
        marker = out.next_marker


    # List the files and objects under the fun1/ directory.
    marker = ''
    is_truncated = True
    while is_truncated:
        out = client.list_objects(bucket_name, delimiter="/", prefix='fun1/', marker=marker)
        # common_prefixes returns the subdirectories under the root directory.
        for prefix in out.common_prefixes:
            print('subDir', prefix.prefix)

        # The contents return the objects in the root directory.
        for content in out.contents:
            print('file', content.key)
        is_truncated = out.is_truncated
        marker = out.next_marker
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

For the API documentation on listing objects, see [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects).
