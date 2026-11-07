---
title: "Delete Object (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-objects-python-sdk"
---

You can delete objects when they are no longer needed to reduce costs. The current TOS Python SDK supports deleting a single object in a bucket and deleting multiple specified objects. For buckets with versioning enabled, you can delete any version of an object by specifying its version ID.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* When deleting objects, you must have the `tos:DeleteObject` permission. For details, see the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When deleting versioned objects, you must have the `tos:DeleteObjectVersion` permission. For details, see the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When a bucket’s versioning status is enabled, deleting an object without specifying a version ID will not delete the object but will generate a new version with a deletion marker (DeleteMarker). When the bucket’s versioning status is `Suspended`, deleting the versioned object`null`and generating a deletion marker with version ID`null`will occur. In a versioning\-enabled bucket, specifying a version ID while deleting an object deletes that particular version.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5Yig6Zmk5oyH5a6a5a-56LGh"></span>
### **Delete specified object**

The following code deletes the `obejct-test` object in the specified bucket `bucket-test`.

```python
import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
object_key = 'object-key'
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Delete specified objects under a specified bucket.
    resp = client.delete_object(bucket_name, object_key)
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


<span id=".5Yig6Zmk5oyH5a6a54mI5pys5a-56LGh"></span>
### **Delete specified version object**

The following code deletes a specified version of the `obejct-test` object in the version\-enabled bucket `bucket-test`.

```python
import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
object_key = 'object-key'
version_id = "your object version"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Delete specified objects under a specified bucket.
    client.delete_object(bucket_name, object_key, version_id=version_id)
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


<span id=".5om56YeP5Yig6Zmk5a-56LGh"></span>
### **Batch delete objects**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In a version\-controlled bucket, when calling the DeleteMultiObjects API to batch delete objects, if the <code>versionId</code> is not specified in the Delete request, a delete marker will be inserted. If the <code>versionId</code> is specified, the specified version of the object will be permanently deleted.</div>


* <div data-tips="true" data-tips-type="tip">The response mode supported by batch deleting objects can be set via <code>quiet</code>:</div>


   * <div data-tips="true" data-tips-type="tip">When <code>quiet</code> is <code>false</code>, all deletion results will be included in the response regardless of whether the objects are deleted successfully.</div>


   * <div data-tips="true" data-tips-type="tip">When <code>quiet</code> is <code>true</code>, only the failed deletion results are returned in the response; no returned results indicate successful deletion.</div>



The following code deletes multiple objects with the specified object name from the bucket `bucket-test`.

```python
import os
import tos

from tos.models2 import ObjectTobeDeleted

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
object_key_1 = "your object key1"
object_key_2 = "your object key2"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Batch delete specified objects under a specified bucket
    objects = []
    objects.append(ObjectToBeDeleted(object_key_1))
    objects.append(ObjectToBeDeleted(object_key_2))
    # If the bucket has versioning enabled and no object version is specified, it will be a delete marker
    # For buckets without versioning enabled, the objects will be directly deleted
    delete_out = client.delete_multi_objects(bucket=bucket_name, objects=objects)

    # deleted contains the objects that have been successfully deleted.
    for deleted in delete_out.deleted:
        # Delete object key
        print('success deleted object key', deleted.key)
        # Delete object version id
        print('success delete object version id', deleted.version_id)
        # delete_marker indicates if it is a delete marker object
        print('is delete marker', deleted.delete_marker)
        # delete_marker_version_id is the version ID corresponding to the delete marker
        print('delete marker version id', deleted.delete_marker_version_id)

    # error contains the object that failed to be deleted.
    for err in delete_out.error:
        print('delete err key', err.key)
        print('delete err key version', err.version_id)
        print('delete err message', err.message)
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


<span id=".5Yig6Zmk5oyH5a6a54mI5pys5ZKM5a-56LGh5ZCN55qE5a-56LGh"></span>
### **Delete objects with specified version and object name**

The following code deletes multiple objects with the specified object name and version number from the bucket `bucket-test`.

```python
import os
import tos

from tos.models2 import ObjectTobeDeleted

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
object_key_1 = "your object key1"
version_id_1 = "your object_key_1 version id"
object_key_2 = "your object key2"
version_id_2 = "your object_key_2 version id"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Delete specified objects under specified bucket in batch.
    objects = []
    objects.append(ObjectTobeDeleted(object_key_1, version_id_1))
    objects.append(ObjectTobeDeleted(object_key_2, version_id_2))
    # If the bucket is enabled with versioning and a specific version number is specified for deleting an object, it is directly marked for deletion.
    delete_out = client.delete_multi_objects(bucket=bucket_name, objects=objects)

    # deleted contains the objects that have been successfully deleted.
    for deleted in delete_out.deleted:
        # Delete object key
        print('success deleted object key', deleted.key)
        # Delete object version id
        print('success delete object version id', deleted.version_id)
        # is_delete_marker indicates if the object is a delete marker
        print('is delete marker', deleted.delete_marker)
        # delete_marker_version_id is the version ID corresponding to the delete marker
        print('delete marker version id', deleted.delete_marker_version_id)

    # error contains the object that failed to be deleted.
    for err in delete_out.error:
        print('delete err key', err.key)
        print('delete err key version', err.version_id)
        print('delete err message', err.message)
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


<span id=".5Yig6Zmk5qG25Lit5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **Delete all objects with the specified prefix in the bucket**

The following code deletes all objects with the prefix `log/` from the bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
prefix = "log/"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    is_truncated = True
    marker = ''
    while is_truncated:
        out = client.list_objects(bucket_name, prefix='log/', marker=marker)
        for obj in out.contents:
            client.delete_object(bucket_name, obj.key)    
        is_truncated = out.is_truncated
        marker = out.next_marker
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


* For the delete object API documentation, see [DeleteObject](https://docs.byteplus.com/docs/tos/Delete-objects-python-sdk).

* For the delete multi\-version object API documentation, see [DeleteMultiObject](https://docs.byteplus.com/docs/tos/reference-deletemultiobjects).
