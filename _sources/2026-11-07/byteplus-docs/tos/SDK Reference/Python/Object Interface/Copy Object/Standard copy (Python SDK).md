---
title: "Standard copy (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-copy-python-sdk"
---

You can use the copy_object API to copy objects between buckets in the same region or within the same bucket. Copy does not support cross\-region transfers and requires read permissions on the source object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* Copy does not support cross\-region bucket\-to\-bucket copying.

* To copy objects, your account must have read access to the source object and write access to the target bucket.

* When copying objects, you can retain all metadata (default) or specify new metadata. However, ACLs are not preserved and default to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

You can use standard copy for objects smaller than 5 GiB. The following code copies the `src_object_key` object from the `src_bucket_name` bucket to the `bucket_name` bucket and sets the object name as `object_key`.

```python
import os
import tos
from tos import MetadataDirectiveType

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
# Name of the destination bucket
bucket_name = "bucket-test"
# New object key in the destination bucket after copy
object_key = "object-test"
# Name of the source bucket
src_bucket_name = "your src bucket name"
# 源对象名称
src_object_key = "your src object key"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Copy the object with key src_object_key from the bucket src_bucket_name to the bucket bucket_name and set the object key as object_key.
    client.copy_object(bucket_name, object_key, src_bucket_name, src_object_key,
                       # Set the ACL permission of the copied object using the optional field "acl"
                       acl=tos.ACLType.ACL_Private,
                       # Set the storage type of the copied object using the optional field
                       storage_class=tos.StorageClassType.Storage_Class_Standard,
                       # Set metadata_directive=MetadataDirectiveType.Metadata_Directive_Copy to copy metadata from the source object.
                       metadata_directive=MetadataDirectiveType.Metadata_Directive_Copy)

    # client.copy_object(bucket_name, object_key, src_bucket_name, src_object_key,
    #                  #  Set metadata_directive=MetadataDirectiveType.Metadata_Directive_Replace to replace the metadata provided in the request.
    #                   metadata_directive=MetadataDirectiveType.Metadata_Directive_Replace,
    #                  # Replacement Object Metadata
    #                  meta={'key1': 'replaceValue'})  
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

For the API documentation on standard copy, see [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
