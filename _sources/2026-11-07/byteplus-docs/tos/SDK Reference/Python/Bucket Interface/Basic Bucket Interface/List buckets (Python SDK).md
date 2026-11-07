---
title: "List buckets (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-python-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. You can list the buckets of all regions under your current account.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before enumerating buckets, you must have `tos: ListBuckets`permission. For specific operations, please refer to [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* This interface returns buckets for all regions of the current account.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample code**

The following code enumerates the buckets in all areas of the current account.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # List all buckets.
    resp = client.list_buckets()
    for bucket in resp.buckets:
        print("name:{}".format(bucket.name))
        print("location:{}".format(bucket.location))
        print("extranet_endpoint:{}".format(bucket.extranet_endpoint))
        print("intranet_endpoint:{}".format(bucket.intranet_endpoint))
        print("creation_date:{}".format(bucket.creation_date))
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

For API documentation on enumerating buckets, see [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
