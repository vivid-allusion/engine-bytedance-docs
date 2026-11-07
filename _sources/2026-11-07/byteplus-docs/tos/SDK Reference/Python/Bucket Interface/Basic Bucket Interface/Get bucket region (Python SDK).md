---
title: "Get bucket region (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-the-bucket-region-python-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. This article describes how to obtain the regional information where the bucket is located.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**

By default, only the owner of the bucket can view the area where the bucket is located.

<span id=".56S65L6L5Luj56CB"></span>
## **Sample code**

The following code is used to get the Region where the `bucket-test`is located.

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
    # Get the location of the bucket.
    out = client.get_bucket_location(bucket_name)
    print('region={}'.format(out.region))
    print('extranet_endpoint={}'.format(out.extranet_endpoint))
    print('intranet_endpoint={}'.format(out.intranet_endpoint))
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
    print('with unknown error: {}'.format(e))
```
