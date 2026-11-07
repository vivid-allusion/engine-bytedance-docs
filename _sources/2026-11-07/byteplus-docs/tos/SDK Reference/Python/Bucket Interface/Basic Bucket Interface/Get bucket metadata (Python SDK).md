---
title: "Get bucket metadata (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-metadata-python-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. This article describes how to obtain bucket metadata and determine whether a bucket exists.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before you can get the bucket metadata, you must have the `tos: HeadBucket`permission. For specific operations, please refer to [Overview](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If the bucket does not exist, the interface returns a 404, which is also commonly used to determine whether a bucket exists.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample code**

The following code is used to obtain bucket\-test metadata.

```python
import http

import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    head_bucket_out = client.head_bucket(bucket_name)
    print('region: ', head_bucket_out.region)
    print('storageClass: ', head_bucket_out.storage_class)
    print('azRedundancy: ', head_bucket_out.az_redundancy)
except tos.exceptions.TosClientError as e:
    # Operation failed, catch client error, usually caused by invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    if e.status_code == http.HTTPStatus.NOT_FOUND:
        # The HTTP status code 404 indicates that the bucket does not exist.
        print('bucket not exist')
    elif e.status_code == http.HTTPStatus.FORBIDDEN:
        # The HTTP status code 403 indicates that the user does not have the HeadBucket permission.
        print('do not have head bucket policy')
    else:
        # # Operation failed, catch server error, detailed error information can be obtained from the response
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

For the metadata API documentation for getting buckets, see [HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket).
