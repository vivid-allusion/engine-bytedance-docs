---
title: "Manage object tags (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-tags-python-sdk"
---

TOS supports object tagging and tag\-based object lifecycle management. This article explains how to manage object tags.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* To set object tags, you must have `tos:PutObjectTagging` permission. For detailed steps, see [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To get object tags, you must have `tos:GetObjectTagging` permission. For detailed steps, see [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete object tags, you must have `tos:DeleteObjectTagging` permission. For detailed steps, see [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Each object can have up to 10 tags, and tag keys must be unique on the same object. For tag restrictions, see [Object tag restrictions](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).


<span id=".6K6-572u5a-56LGh5qCH562-"></span>
## Setting tags for an object

TOS supports classifying bucket files using object tags. You can set lifecycle rules for objects with the same tags.

<span id=".56S65L6L5Luj56CB"></span>
### Sample code

The following code sets tags for bucket `bucket-test` and object `object-test`.

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
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Set tags
    # If the bucket has versioning enabled, you can specify the corresponding version object using version_id = 'your object version id'
    tag1 = tos.models2.Tag('key1', 'value1')
    tag2 = tos.models2.Tag('key2', 'value2')
    client.put_object_tagging(bucket_name, object_key, [tag1, tag2])
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


<span id=".6I635Y-W5a-56LGh5qCH562-"></span>
## Getting tags of an object

After setting object tags, you can retrieve the tags of the object. When versioning is enabled for the bucket, TOS returns tags of the object's current version by default. You can specify the object's version to get tags for that particular version.

<span id=".56S65L6L5Luj56CB"></span>
### Sample code

The following code retrieves tag information for object `object-test` in bucket `bucket-test`.

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
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Get object tags
    # If the bucket has versioning enabled, you can specify the corresponding version object by version_id = 'your object version id'
    tags = client.get_object_tagging(bucket_name, object_key)
    for tag in tags.tag_set:
        print('tag_key', tag.key)
        print('tag_value', tag.value)
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


<span id=".5Yig6Zmk5a-56LGh5qCH562-"></span>
## Deleting tags from an object

You can delete unwanted tag information as needed. When versioning is enabled for the bucket, TOS deletes tags only from the object's current version by default. You can specify the version ID to delete tags from a specific version.

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
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Remove object tags
    # If the bucket has versioning enabled, you can specify the corresponding version object by using version_id = 'your object version id'.
    client.delete_object_tagging(bucket_name, object_key)
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

For more information about object tags, see [Managing object tags](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).
