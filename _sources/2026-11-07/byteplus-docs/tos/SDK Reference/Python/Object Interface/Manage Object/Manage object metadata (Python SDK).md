---
title: "Manage object metadata (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-metadata-python-sdk"
---

Object metadata describes the properties of an object, including standard HTTP properties (HTTP Header) and user\-defined metadata (User Meta).

<span id=".6K6-572u6Ieq5a6a5LmJ5YWD5pWw5o2u"></span>
## Set custom metadata

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To set object metadata, you must have <code>tos:PutObject</code> permission. See the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">permission configuration guide</a> for details.</div>


* <div data-tips="true" data-tips-type="warning">When setting user\-defined metadata, custom metadata keys in English letters support lowercase only and do not allow spaces or special characters.</div>



<span id=".56S65L6L5Luj56CB"></span>
### Example code

You can set object metadata to identify the object's purpose or attributes. The following code sets the object's metadata.

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
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Set object metadata during regular upload.
    client.put_object(bucket_name, object_key,
                      # Setting user-defined metadata through optional meta fields
                      meta={'author': 'test1', 'name': 'Bob'},
                      # Setting HTTP standard attribute through content_disposition
                      content_disposition='attachment; filename=123.txt',
                      # Setting object type through content_type
                      content_type="text/plain")
    # Set object metadata during multipart upload.
    client.create_multipart_upload(bucket_name, object_key,
                                   # Setting user-defined metadata through the optional fields in the meta section.
                                   meta={'author': 'test2', 'name': 'Bob'},
                                   # Setting HTTP standard attributes through content_disposition
                                   content_disposition='attachment; filename=123.txt',
                                   # Set the object type through the content_type.
                                   content_type="text/plain")
    # Set object metadata through the set_object_meta interface.
    client.set_object_meta(bucket_name, object_key, meta={'author': 'test3', 'name': 'Bob'},
                           # Set HTTP standard properties through content_disposition
                           content_disposition='attachment; filename=123.txt',
                           # Set object type through content_type
                           content_type="text/plain")
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
### **Related documentation**

For API documentation on setting object metadata, see [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta).

<span id=".6I635Y-W5a-56LGh5YWD5pWw5o2u"></span>
## Retrieve object metadata

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get object metadata, you must have <code>tos:GetObject</code> permission. For details, see <a href="https://docs.byteplus.com/docs/tos/docs-overview_6">IAM Policy Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### Sample code

You can use head_object to obtain object metadata. The following code retrieves the object's metadata.

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
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Get object metadata.
    result = client.head_object(bucket_name, object_key)
    for key, value in result.meta.items():
        print('meta key', key)
        print('meta value', value)
    print('content-disposition', result.content_disposition)
    print('content-type', result.content_type)
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
### **Related documentation**

For API documentation on getting object metadata, see [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
