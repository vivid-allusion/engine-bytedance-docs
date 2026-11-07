---
title: "Rename Object (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Rename-objects-python-sdk"
---

TOS supports renaming the key of a single object within a bucket without copying or deleting data.

<span id="ad08aab0"></span>
## **Notes**


* You need to enable the rename feature before renaming objects.

* RenameObject only supports renaming objects uploaded after it is enabled. Objects uploaded before this feature is enabled are not supported.

* Concurrent renaming is not supported for the same object.

* All metadata of the renamed object is consistent with the source object.


<span id="b1446e86"></span>
## **Sample Code**

The following code demonstrates the object renaming feature.

```Python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
object_new_key = "object-new-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Display the rename object functionality for opening a bucket.
    client.put_bucket_rename(bucket_name, rename_enable=True)
    client.rename_object(bucket=bucket_name, key= object_key, new_key= object_new_key)
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


<span id="908963df"></span>
## Related documentation

For the API documentation of RenameObject, see [RenameObject](https://docs.byteplus.com/docs/tos/Renameobject).
