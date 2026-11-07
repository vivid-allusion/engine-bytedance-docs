---
title: "Delete scenarios (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-the-scenes-python-sdk"
---

This article introduces common code scenarios for deleting objects.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To delete an object, your account must have `tos:DeleteObject` permission. For detailed steps, see [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete multi\-version objects, your account must have `tos:DeleteObjectVersion` permission. For detailed steps, see [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Use delete operations cautiously, as deleted files cannot be recovered.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5Yig6Zmk5qG25Lit5oyH5a6a55uu5b2V"></span>
### Delete a specified directory in the bucket

The following code deletes the specified directory `example-test/` in bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

client = tos.TosClientV2(ak, sk, endpoint, region)

is_truncated = True
next_continuation_token = ''
while is_truncated:
    out = client.list_objects_type2(bucket_name, prefix="example-test/")
    is_truncated = out.is_truncated
    next_continuation_token = out.next_continuation_token
    for content in out.contents:
        client.delete_object(bucket_name, content.key)
```


<span id=".5riF56m65pyq5byA5ZCv54mI5pys5o6n5Yi255qE5qG25Lit5omA5pyJ5a-56LGh"></span>
### Clear all objects in a bucket without versioning enabled

The following code clears all objects (including unmerged fragments) in the multi\-version bucket `bucket-test` that is not enabled.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

# Create a TosClientV2 object to perform operations on buckets and objects.
client = tos.TosClientV2(ak, sk, endpoint, region)

# Delete all objects in the unversioned bucket.
truncated = True
continuation_token = ''
while truncated:
    result = client.list_objects_type2(bucket_name, continuation_token=continuation_token)
    for iterm in result.contents:
        client.delete_object(bucket_name, iterm.key)
    truncated = result.is_truncated
    continuation_token = result.next_continuation_token

# Delete all unmerged objects.
is_truncated = True
marker = ''
while is_truncated:
    out = client.list_multipart_uploads(bucket_name, key_marker=marker)
    for upload in out.uploads:
        client.abort_multipart_upload(bucket_name, upload.key, upload.upload_id)
    is_truncated = out.is_truncated
    marker = out.next_key_marker
```


<span id=".5riF56m65byA5ZCv54mI5pys5o6n5Yi255qE5qG25Lit5omA5pyJ5a-56LGh"></span>
### Clear all objects in the version\-controlled bucket

The following code clears all objects (including unmerged fragments) in the multi\-version bucket `bucket-test` that is enabled.

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
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Delete all versions of all objects, delete all versions with delete markers.
    is_truncated = True
    key_marker = ''
    version_id_marker = ''
    while is_truncated:
        out = client.list_object_versions(bucket_name, key_marker=key_marker, version_id_marker=version_id_marker)
        # version contains information about multiple versions of an object.
        for version in out.versions:
            client.delete_object(bucket_name, version.key, version.version_id)
        # Delete markup information.
        for delete_marker in out.delete_markers:
            client.delete_object(bucket_name, delete_marker.key, delete_marker.version_id)
        is_truncated = out.is_truncated
        key_marker = out.next_key_marker
        version_id_marker = out.next_version_id_marker

    # Delete all unmerged objects.
    is_truncated = True
    marker = ''
    while is_truncated:
        out = client.list_multipart_uploads(bucket_name, key_marker=marker)
        for upload in out.uploads:
            client.abort_multipart_upload(bucket_name, upload.key, upload.upload_id)
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
