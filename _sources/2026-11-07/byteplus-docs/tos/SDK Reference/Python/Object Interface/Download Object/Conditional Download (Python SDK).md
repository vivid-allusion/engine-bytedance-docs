---
title: "Conditional Download (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-python-sdk"
---

If you want to set restrictions on downloading objects (object ETag or object modification time) when downloading objects, you can use the restricted download function provided by the TOS Python SDK to download objects only when the object information meets the conditions you specify. This article describes how to download objects by qualifying them.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before downloading an object, you must have `tos: GetObject`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* To open multiple versions of a bucket, you must have the `tos: GetObjectVersion`permission when downloading the specified version object. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* If an application downloads a large number of the same object at the same time, your access speed will be limited by TOS bandwidth and geography. It is recommended that you use CDN products to improve performance while also reducing your costs.


<span id=".6ZmQ5a6a5p2h5Lu26K-05piO"></span>
## **Qualification statement**

The qualifications supported by TOS are as follows.


|**parameter** |**describe** |**How to set up** |
|---|---|---|
|If\-Match |The object is returned only if the incoming `ETag`is equal to the object's `ETag`, otherwise 412 Precondition Failed is returned. |if_match |
|If\-Modified\-Since |The object is returned only if it has been modified since the specified time, otherwise 304 Not Modified is returned. |if_modified_since |
|If\-None\-Match |The object is returned only if the incoming `ETag`is not equal to the object's `ETag`, otherwise 304 Not Modified is returned. |if_none_match |
|If\-Unmodified\-Since |The object is returned only if it has not been modified since the specified time, otherwise 412 Precondition Failed is returned. |if_unmodified_since |


<span id=".56S65L6L5Luj56CB"></span>
## **Sample code**

The following code qualifies the download `bucket-test`object `object-test`.

```python
import datetime

import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"

# Create a TosClientV2 object to perform operations on buckets and objects.
client = tos.TosClientV2(ak, sk, endpoint, region)

try:
    # If the time specified by if_modified_since=date is earlier than the actual modification time of the Object, download the Object normally. Otherwise, return error 304 Not modified.
    date = datetime.datetime(2020, 12, 20)
    client.get_object(bucket_name, object_key, if_modified_since=date)

    # If the time specified by if_unmodified_since is equal to or later than the actual modification time of the Object, then the Object is downloaded normally. Otherwise, an error 412 Precondition failed is returned.
    date = datetime.datetime(2100, 12, 20)
    client.get_object(bucket_name, object_key, if_unmodified_since=date)

    # If the provided ETag matches the ETag of the object, download the object normally. Otherwise, return error 412 Precondition Failed.
    etag = client.head_object(bucket_name, object_key).etag
    client.get_object(bucket_name, object_key, if_match=etag)

    # If the ETag passed in if_none_match does not match the ETag of the Object, download the Object normally. Otherwise, return the error 304 Not modified.
    etag = 'DC21493F505BA3739562D8CC452C****'
    client.get_object(bucket_name, object_key, if_none_match=etag)
except tos.exceptions.TosServerError as e:
    # When the query does not meet the specified conditions, directly throw TosServerError. You can check the HTTP status code through e.status_code.
    print('http err code', e.status_code)
    print('message', e.message)
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print(e)
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
