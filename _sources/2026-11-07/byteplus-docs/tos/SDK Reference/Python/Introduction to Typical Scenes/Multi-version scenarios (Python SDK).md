---
title: "Multi-version scenarios (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multi-version-python-sdk"
---

Version control applies to all objects in the bucket. By enabling version control for the bucket, you can restore objects to any previous version after accidental deletion or overwriting. Currently, multi\-version support includes interfaces such as GetObject, GetObjectACL, CopyObject, UploadPartCopy, and DeleteObject. When calling these interfaces, you can specify the target object's specific version through the optional parameter version_id.

<span id=".5qG25aSa54mI5pys566h55CG"></span>
## **Bucket multi\-version management**

In TOS, a bucket's version status includes three states: disabled, versioning enabled, and versioning suspended.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To enable or suspend multi\-version status for a bucket, your account must have the <code>tos:PutBucketVersioning</code> permission.</div>


* <div data-tips="true" data-tips-type="warning">To query the multi\-version status of a bucket, your account must have the <code>tos:GetBucketVersioning</code> permission.</div>



<span id=".6K6-572u5qG254mI5pys5o6n5Yi254q25oCB"></span>
### **Set bucket version control status**

The following code sets the bucket status to enable versioning or suspend version control.

```python
import os
import tos
from tos import VersioningStatusType

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
     # Enable bucket versioning
    client.put_bucket_versioning(bucket_name, VersioningStatusType.Versioning_Status_Enabled)
    # Pause bucket multi-version.
    client.put_bucket_versioning(bucket_name, VersioningStatusType.Versioning_Status_Suspended)
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


<span id=".6I635Y-W5qG255qE54mI5pys5o6n5Yi254q25oCB"></span>
### **Get the bucket version control status**

The following code retrieves the version control status of the bucket `bucket-test`.

```python
import os
import tos
from tos import VersioningStatusType

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
    # Enable bucket versioning
    version_info = client.get_bucket_version(bucket_name)
    print('bucket version state:', version_info.status)
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


<span id=".5LiL6L295aSa54mI5pys5a-56LGh"></span>
## Download versioned object

The following code downloads a specified version of the object `object-test` from the bucket `bucket-test` into memory.

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
version_id = "your version id"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # get_object returns an iterable object.
    object_stream = client.get_object(bucket_name, object_key, version_id=version_id)
    # Iteratively read object content.
    for content in object_stream:
        print(content)
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


<span id=".5Yig6Zmk5aSa54mI5pys5a-56LGh"></span>
## Delete versioned object

The following code deletes a specified version of the object `object-test` in the specified bucket `bucket-test`.

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
version_id = "your version id"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Delete specified objects under a specified bucket.
    resp = client.delete_object(bucket_name, object_key, version_id=version_id)
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


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
## Empty a bucket with versioning enabled

The following code example empties an entire bucket with versioning enabled, including deleting multiple versions of objects, delete marker objects, and all uncommitted objects.

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

    # Delete all versions of all objects, delete all versions with deletion markers.
    is_truncated = True
    key_marker = ''
    version_id_marker = ''
    while is_truncated:
        out = client.list_object_versions(bucket_name, key_marker=key_marker, version_id_marker=version_id_marker)
        # The version contains information about multiple versions of objects.
        for version in out.versions:
            client.delete_object(bucket_name, version.key, version.version_id)
        # Delete tag information.
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
