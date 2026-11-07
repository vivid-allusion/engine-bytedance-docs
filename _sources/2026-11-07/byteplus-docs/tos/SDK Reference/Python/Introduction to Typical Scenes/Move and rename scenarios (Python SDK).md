---
title: "Move and rename scenarios (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Move-and-rename-scenes-python-sdk"
---

If you need to rename files in a Bucket, you can copy the source object to the target object using the CopyObject API and then delete the source object using the DeleteObject API.

<span id=".6YeN5ZG95ZCN5Y2V5Liq5a-56LGh"></span>
## **Rename a single object**

The following code renames the object `src-object` to `dest-object` in the bucket `bucket-test`.

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

    resp = client.copy_object('bucket-test', 'dest-object', 'bucket-test', 'src-object')
    # Check the return status. If it is 200, it indicates successful execution.
    print('result status', resp.status_code)
    resp = client.delete_object('bucket-test', 'src-object')
    # Check the return status. If it is 200, it indicates successful execution.
    print('result status', resp.status_code)
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


<span id=".6YeN5ZG95ZCN55uu5b2V"></span>
## **Rename a directory**

The following code renames the directory `exampledir1/` to `exampledir2/` in the bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
dir_1 = 'exampledir1/'
dir_2 = 'exampledir2/'

client = tos.TosClientV2(ak, sk, endpoint, region)

truncated = True
continuation_token = ''
while truncated:
    result = client.list_objects_type2(bucket_name, continuation_token=continuation_token, prefix=dir_1)
    for iterm in result.contents:
        new_key = iterm.key
        if iterm.key == dir_1:
            new_key = dir_2
        else:
            new_key = dir_2 + new_key.removeprefix(dir_1)
        client.copy_object(bucket_name, new_key, bucket_name, iterm.key)
        client.delete_object(bucket_name, iterm.key)
    truncated = result.is_truncated
    continuation_token = result.next_continuation_token
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**


* For the CopyObject API, see [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).

* For the DeleteObject API, see [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).
