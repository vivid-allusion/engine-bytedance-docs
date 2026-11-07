---
title: "List objects V2 (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-v2-python-sdk"
---

This article explains how to list all objects in a specified bucket, files with a specified prefix, files and subdirectories under a specified directory using ListObjectsType2.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* The ListObjects interface has been revised to ListObjectsType2. Developers are strongly recommended to use ListObjectsType2. To ensure backward compatibility, TOS continues to support the ListObjects interface.

* To use list objects V2, you must have `tos:ListBucket` permission. For details, see [IAM policy overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

ListObjectsType2 supports the following parameters.


|**Parameter** |**Description** |
|---|---|
|prefix |Prefix for this query result. |
|delimiter |The character used to group object names. |
|start_after |The starting point of this listing target. |
|continuation_token |Specify the token from which the listing operation starts. Can be obtained from the next_continuation_token in the previous listing result. |
|max_keys |The maximum number of listing targets returned, default is 1000.<br><br>Value range: greater than 0 and less than or equal to 1000. |


<span id=".56S65L6L5Luj56CB"></span>
## Example code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Simple listing**

The following code lists up to 10 objects in the `bucket-test` bucket.

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

    # The code example for listing 10 objects in a bucket is as follows:
    result = client.list_objects_type2(bucket_name, max_keys=10)
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
### **List with pagination**

The following code lists objects in the `bucket-test` bucket with pagination.

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

    # List the first 1000 objects in the pagination bucket.
    result = client.list_objects_type2(bucket_name)
    for item in result.contents:
        print(item.key)
    # If the pagination has not listed all subsequent 1000 objects.
    if result.is_truncated:
        result = client.list_objects_type2(bucket_name, continuation_token=result.next_continuation_token)
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
### **List all objects with a specific prefix**

The following code lists all objects with a specific prefix in the `bucket-test` bucket.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
prefix = "your prefix"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # List all objects with a specific prefix under a specified bucket.
    truncated = True
    continuation_token = ''

    while truncated:
        result = client.list_objects_type2(bucket_name, prefix=prefix, continuation_token=continuation_token)
        for item in result.contents:
            print(item.key)
        truncated = result.is_truncated
        continuation_token = result.next_continuation_token
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
### **List all objects in the bucket**

The following code lists all objects in the `bucket-test` bucket.

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
    # List all objects under a specified bucket.
    truncated = True
    continuation_token = ''
    while truncated:
        result = client.list_objects_type2(bucket_name, continuation_token=continuation_token)
        for item in result.contents:
            print(item.key)
        truncated = result.is_truncated
        continuation_token = result.next_continuation_token
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
### **List files and subdirectories under a specific directory**

TOS only has the concept of objects, and you can simulate directory functionality by creating an object ending with a slash and has a size of 0.`/`Ending with a slash to simulate directory functionality.

You can simulate directory functions using two parameters: `delimiter` and `prefix`.


* First, set `delimiter` to`/`Set `prefix` to empty to return objects and subdirectory information under the root directory.

* Set `delimiter` to`/`Set `prefix` to the subdirectory to return objects and subdirectories within that subdirectory.


The following code lists files and subdirectories in a specified directory.

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
    # Add subdirectories named fun1, fun2, and fun3, along with a file named test, to the Bucket.
    client.put_object(bucket_name, "fun1/")
    client.put_object(bucket_name, "fun1/test/")
    client.put_object(bucket_name, "fun1/obj.txt")
    client.put_object(bucket_name, "fun2/")
    client.put_object(bucket_name, "fun3/")
    client.put_object(bucket_name, "test")

    # 1. List files and subdirectories in the root directory.
    is_truncated = True
    next_continuation_token = ''
    while is_truncated:
        out = client.list_objects_type2(bucket_name, delimiter="/", continuation_token=next_continuation_token)
        is_truncated = out.is_truncated
        next_continuation_token = out.next_continuation_token
        # common_prefixes returns the subdirectories under the root directory.
        for prefix in out.common_prefixes:
            print('subDir', prefix.prefix)

        # The contents return the objects in the root directory.
        for content in out.contents:
            print('file', content.key)

    # 2. List files and subdirectories under the fun1/ directory.
    is_truncated = True
    next_continuation_token = ''
    while is_truncated:
        out = client.list_objects_type2(bucket_name, delimiter="/", prefix="fun1/", continuation_token=next_continuation_token)
        is_truncated = out.is_truncated
        next_continuation_token = out.next_continuation_token
        # common_prefixes returns the subdirectories under the fun1/ directory.
        for prefix in out.common_prefixes:
            print('subDir', prefix.prefix)

        # The contents returned the objects under the directory fun1.
        for content in out.contents:
            print('file', content.key)
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
