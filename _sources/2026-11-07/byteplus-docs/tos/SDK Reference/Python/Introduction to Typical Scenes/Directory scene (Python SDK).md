---
title: "Directory scene (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Directory-scenes-python-sdk"
---

TOS only has the concept of objects and internally stores data in a flat structure. To help you group objects and simplify permission management, you can organize objects using directory hierarchies.

<span id=".5Yib5bu655uu5b2V"></span>
## **create directory**

TOS only has the concept of objects. You can simulate directory functionality by creating an object with size 0 and ending with a slash`/`to mimic a directory.

The following code creates the directory `exampledir/` and the subdirectory `exampledir/test/` in the bucket `bucket-test`.

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

    # Create bucket
    client.create_bucket(bucket_name)

    # Enter the directory name, the directory must end with a forward slash.
    client.put_object(bucket_name, 'exampledir/')
    # Enter the directory name, create a multi-level directory, and the directory must end with a forward slash.
    client.put_object(bucket_name, 'exampledir/test/')
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


<span id=".5qih5ouf55uu5b2V5p-l6K-i"></span>
## **simulate directory listing**

You can simulate directory functionality using the `delimiter` and `prefix` parameters:


* First, set `delimiter` to`/`and set `prefix` to empty; this returns objects and subdirectory information in the root directory.

* Set `delimiter` to`/`Set `prefix` as the subdirectory to return objects and subdirectories within it.


The following code lists objects and subdirectories under directory `log/` in bucket `bucket-test`.

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
    is_truncated = True
    next_continuation_token = ''
    while is_truncated:
        out = client.list_objects_type2(bucket_name, delimiter="/", prefix="log/",
                                        continuation_token=next_continuation_token)
        is_truncated = out.is_truncated
        next_continuation_token = out.next_continuation_token
        # common_prefixes returns the subdirectories under the root directory.
        for prefix in out.common_prefixes:
            print('subDir', prefix.prefix)

        # The following code is used to delete a specified directory in a bucket.
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


<span id=".5Yig6Zmk55uu5b2V"></span>
## **Delete directory**

The following code deletes all data in directory `log/` within bucket `bucket-test`.

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
    is_truncated = True
    continuation_token = ''
    # The following code is used to delete a specified directory in a bucket.
    while is_truncated:
        out = client.list_objects_type2(bucket_name, continuation_token=continuation_token, prefix='log/')
        for content in out.contents:
            client.delete_object(bucket_name, content.key)
        continuation_token = out.next_continuation_token
        is_truncated = out.is_truncated
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
