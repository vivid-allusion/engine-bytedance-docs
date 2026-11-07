---
title: "List unmerged objects (list multipart upload tasks) - Python SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-unmerged-objects-python-sdk"
---

This API is used to list multiversion objects in a bucket. This API returns a maximum of 1,000 multiversion objects in the bucket for each request. You can use request parameters to define the selection criteria for the objects to list.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**

To list multipart upload tasks, you need `tos:ListBucketMultipartUploads` permission on the bucket. For details, see [IAM policy overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


|**Parameter** |**Description** |
|---|---|
|prefix |Prefix for this query result. |
|delimiter |The character used to group object names. |
|max_uploads |Returns the maximum number of objects listed, default is 1000.<br><br>Values: greater than 0 and less than or equal to 1000. |
|key_marker |Starting position for listing versioned objects. Objects are listed in alphabetical order after the specified start. Usually the next_marker value returned from the last request. |


<span id=".56S65L6L5Luj56CB"></span>
## Example code

<span id=".566A5Y2V5YiX5Li-5pyq5ZCI5bm25YiG54mH5Lu75Yqh"></span>
### **Simply list unmerged multipart upload tasks**

The following code lists up to 10 unmerged multipart upload tasks in the specified bucket `bucket-test`.

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
    client = tos.TosClientV2(ak, sk, endpoint, region)
    out = client.list_multipart_uploads(bucket_name, max_uploads=10)
    for upload in out.uploads:
        print('object key', upload.key)
        print('upload id', upload.upload_id)
        print('owner', upload.owner)
        print('storage class', upload.storage_class)
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


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5pyq5ZCI5bm255qE5YiG54mH5Lu75Yqh"></span>
### **List all unmerged multipart upload tasks with the specified prefix**

The following code lists all unmerged multipart upload tasks under the prefix `exampledir/` in bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
prefix = 'exampledir/'
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    is_truncated = True
    marker = ''
    while is_truncated:
        out = client.list_multipart_uploads(bucket_name, prefix=prefix, key_marker=marker)
        for upload in out.uploads:
            print('object key', upload.key)
            print('upload id', upload.upload_id)
            print('owner', upload.owner)
            print('storage class', upload.storage_class)
        is_truncated = out.is_truncated
        marker = out.next_key_marker
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


<span id=".5YiX5Li-5omA5pyJ5pyq5ZCI5bm255qE5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### **List all unmerged multipart upload tasks**

The following code lists all unmerged multipart upload tasks in bucket `bucket-test`.

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
    client = tos.TosClientV2(ak, sk, endpoint, region)
    is_truncated = True
    marker = ''
    while is_truncated:
        out = client.list_multipart_uploads(bucket_name, key_marker=marker)
        for upload in out.uploads:
            print('object key', upload.key)
            print('upload id', upload.upload_id)
            print('owner', upload.owner)
            print('storage class', upload.storage_class)
        is_truncated = out.is_truncated
        marker = out.next_key_marker
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


<span id=".5oyJ55uu5b2V6YCS5b2S5YiX5Li-5pyq5ZCI5bm25YiG54mH5Lu75Yqh"></span>
### **Recursively list unmerged multipart upload tasks by directory**

TOS only has the concept of objects. You can simulate directory functionality by creating an object that is 0 bytes and ends with a slash`/`.

The directory function can be simulated using the parameters `delimiter` and `prefix`:


* First set `delimiter` to`/`Then set `prefix` to empty to return objects and subdirectory information in the root directory.

* Set `delimiter` to`/`Set the `prefix` as a subdirectory to return objects and subdirectories within that subdirectory.


The following code lists unmerged multipart upload tasks in the bucket bucket\-test by directory.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
prefix = 'exampledir/'
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    is_truncated = True
    marker = ''
    while is_truncated:
        out = client.list_multipart_uploads(bucket_name, key_marker=marker, delimiter='/', prefix=prefix)
        for prefix in out.common_prefixes:
            print('subDir', prefix)
            
        for upload in out.uploads:
            print('object key', upload.key)
            print('upload id', upload.upload_id)
            print('owner', upload.owner)
            print('storage class', upload.storage_class)
        is_truncated = out.is_truncated
        marker = out.next_key_marker
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
