---
title: "Multipart copy (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-copy-python-sdk"
---

You can use multipart copy when the object is larger than 5 GiB.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* Copying files does not support cross\-region bucket copy.

* When copying objects, the account must have read permission on the source object and write permission on the target bucket.

* When copying objects, you can retain all metadata (default) or specify new metadata. However, ACL is not retained and is set to private.


<span id=".5YiG54mH5ou36LSd5q2l6aqk"></span>
## Multipart Copy Steps

When the object is larger than 5 GiB, use upload_part_copy for multipart copy, which includes three steps:


1. Initialize the multipart copy task via create_multipart_upload.

2. Copy by upload_part_copy in fragments.

3. Merge fragments through complete_multipart_upload.


<span id=".56S65L6L5Luj56CB"></span>
## Example code

The following code copies the object `src_object_key` from bucket `src_bucket_name` to bucket `bucket_name` and sets the object name as `object_key`.

```python
import os
import tos
from tos.models2 import UploadedPart

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
# Name of the source object
src_object_key = "your src object key"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Get the size of the existing object src_object in the bucket src_bucket.
    head_info = client.head_object(src_bucket_name, src_object_key)
    total_size = head_info.content_length
    part_size = 1024 * 1024 * 5
    # Initialize a Multipart task.
    resp = client.create_multipart_upload(bucket_name, object_key)
    upload_id = resp.upload_id

     # Copy shard
    parts = []
    part_number = 1
    offset = 0
    while offset < total_size:
        num_to_upload = min(part_size, total_size - offset)
        end = offset + num_to_upload - 1

        result = client.upload_part_copy(bucket_name, object_key, upload_id, part_number, src_bucket_name,
                                         src_object_key,
                                         copy_source_range_start=offset, copy_source_range_end=end)

        parts.append(UploadedPart(part_number, result.etag))
        offset += num_to_upload
        part_number += 1
    # Complete the chunk copy.
    resp = client.complete_multipart_upload(bucket_name, object_key, upload_id, parts=parts)
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


* For API documentation on creating multipart upload tasks, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on multipart copy, see [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy).

* For API documentation on merging fragments, see [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).
