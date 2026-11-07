---
title: "Delete bucket (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-python-sdk"
---

When you no longer need to keep a bucket, you can delete it to avoid incurring additional charges.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* After the bucket is deleted, it cannot be recovered. Please proceed with caution.

* Before you can delete a bucket, you must have the `tos: DeleteBucket`permission. For specific operations, please refer to [Overview](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

Before deleting a bucket, make sure you have deleted all the data in the bucket.


* If the bucket has version control turned on, make sure that all current version and history objects in the current bucket have been deleted. For specific operations, please refer to [Permanently deleting a file](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations).

* If there are unmerged shardings in the bucket, make sure to delete all sharding data. For details, see [Managing Parts](https://docs.byteplus.com/docs/tos/docs-managing-parts).

* If there are many objects in the bucket, you can set the bulk deletion of objects through the life cycle rule. For specific operations, please refer to [Setting Lifecycle Rules](https://docs.byteplus.com/docs/tos/Lifecycle-rules-based-on-last-accesstime).


<span id=".56S65L6L5Luj56CB"></span>
## **Sample code**

The following code is used to remove `bucket-test`.

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
    client.delete_bucket(bucket_name)
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
## Related documentation

For API documentation on deleting buckets, see [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
