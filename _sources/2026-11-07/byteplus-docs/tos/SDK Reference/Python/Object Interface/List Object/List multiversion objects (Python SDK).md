---
title: "List multiversion objects (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multi-version-objects-python-sdk"
---

This API is used to list multiversion objects in a bucket. This API returns a maximum of 1,000 multiversion objects in the bucket for each request. You can use request parameters to define the selection criteria for the objects to list.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**

To list multiversion objects, you need the `tos:ListBucketVersions` permission for the bucket. For details, see [IAM policy overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


|**parameter** |**description** |
|---|---|
|prefix |The prefix for this query result. |
|delimiter |The character for grouping object names. |
|max_keys |The maximum number of objects to list, default is 1000.<br><br>Value range: greater than 0 and less than or equal to 1000 |
|key_marker |The starting point for listing multiple versions of objects. Objects are listed in alphabetical order after the specified start. Usually the next_marker value returned by the previous request. |
|version_id_marker |used with key_marker to return the list of versioned objects sorted lexicographically after this value. retrieved from next_version_id_marker of the last listing result. |


<span id=".56S65L6L5Luj56CB"></span>
## Example code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Simple listing**

The following code lists up to 10 multiversion objects in the specified bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
prefix = "your prefix"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    out = client.list_object_versions(bucket_name, max_keys=10)
    # The version contains information about multiple version objects.
    for version in out.versions:
        print('object key', version.key)
        print('version id', version.version_id)
        print('last modified', version.last_modified)
        print('is latest version', version.is_latest)
        # Delete Markup Information
    for delete_marker in out.delete_markers:
        print('delete marker key', delete_marker.key)
        print('delete marker version id', delete_marker.version_id)
        print('delete marker last modified', delete_marker.last_modified)
        print('delete marker is latest version', delete_marker.is_latest)
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


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with a specified prefix**

The following code lists all the versioned objects and delete markers under the prefix `example/` in the bucket `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
prefix = "your prefix"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    is_truncated = True
    key_marker = ''
    version_id_marker = ''
    while is_truncated:
        out = client.list_object_versions(bucket_name, prefix=prefix, key_marker=key_marker, version_id_marker=version_id_marker)
        # version contains information about multiple versions of an object.
        for version in out.versions:
            print('object key', version.key)
            print('version id', version.version_id)
            print('last modified', version.last_modified)
            print('is latest version', version.is_latest)
            # Delete Markup Information
        for delete_marker in out.delete_markers:
            print('delete marker key', delete_marker.key)
            print('delete marker version id', delete_marker.version_id)
            print('delete marker last modified', delete_marker.last_modified)
            print('delete marker is latest version', delete_marker.is_latest)
        is_truncated = out.is_truncated
        key_marker = out.next_key_marker
        version_id_marker = out.next_version_id_marker
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


<span id=".5YiX5Li-5omA5pyJ5a-56LGh"></span>
### **List all objects**

The following code lists all the versioned objects and delete markers in the bucket `bucket-test`.

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
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    is_truncated = True
    key_marker = ''
    version_id_marker = ''
    while is_truncated:
        out = client.list_object_versions(bucket_name, key_marker=key_marker, version_id_marker=version_id_marker)
        # version contains information about multiple versions of an object.
        for version in out.versions:
            print('object key', version.key)
            print('version id', version.version_id)
            print('last modified', version.last_modified)
            print('is latest version', version.is_latest)
            # Delete Markup Information
        for delete_marker in out.delete_markers:
            print('delete marker key', delete_marker.key)
            print('delete marker version id', delete_marker.version_id)
            print('delete marker last modified', delete_marker.last_modified)
            print('delete marker is latest version', delete_marker.is_latest)
        is_truncated = out.is_truncated
        key_marker = out.next_key_marker
        version_id_marker = out.next_version_id_marker
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


<span id=".6YCS5b2S5YiX5Li-55uu5b2V5LiL55qE5a-56LGh5ZKM5a2Q55uu5b2V"></span>
### **Recursively list objects and subdirectories in the directory**

TOS only has the concept of objects, which can simulate directory functionality by creating an object with size 0 and ending with a slash`/`to simulate directory functionality.

The directory function can be simulated through the two parameters `delimiter` and `prefix`:


* First set `delimiter` to`/`and set `prefix` to empty to return objects and subdirectory information under the root directory.

* Set `delimiter` to`/`set `prefix` as a subdirectory to return objects and subdirectories within it.


the following code lists objects and subdirectories under the directory.

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
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # List the files and subfolders in the root directory.
    is_truncated = True
    next_key_marker = ''
    next_version_id_marker = ''
    while is_truncated:
        out = client.list_object_versions(bucket_name, delimiter="/", key_marker=next_key_marker, version_id_marker=next_version_id_marker)
        for prefix in out.common_prefixes:
            print("subDir", prefix.prefix)
        for version in out.versions:
            print('object key', version.key)
            print('version id', version.version_id)
            print('last modified', version.last_modified)
            print('is latest version', version.is_latest)
        is_truncated = out.is_truncated
        next_key_marker = out.next_key_marker
        next_version_id_marker = out.next_version_id_marker

    # List the files and subfolders in the root directory.
    is_truncated = True
    next_key_marker = ''
    next_version_id_marker = ''
    while is_truncated:
        out = client.list_object_versions(bucket_name, prefix="CLion.app/", delimiter="/", key_marker=next_key_marker, version_id_marker=next_version_id_marker)
        for prefix in out.common_prefixes:
            print("subDir", prefix.prefix)
        for version in out.versions:
            print('object key', version.key)
            print('version id', version.version_id)
            print('last modified', version.last_modified)
            print('is latest version', version.is_latest)
        is_truncated = out.is_truncated
        next_key_marker = out.next_key_marker
        next_version_id_marker = out.next_version_id_marker

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
## **related documentation**

for the API documentation on listing multiple versions of objects, see [ListObjectsVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
