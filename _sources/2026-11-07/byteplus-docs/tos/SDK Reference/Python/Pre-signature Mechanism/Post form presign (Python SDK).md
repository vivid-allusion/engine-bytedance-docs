---
title: "Post form presign (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Post-form-pre-signature-python-sdk"
---

This article introduces example code for POST form presign.

<span id=".56S65L6L5Luj56CB"></span>
## Example code

The following code uses POST form presign to upload to the bucket Adds object `object-test` to `bucket-test`.

```Python
import os
import tos
from tos.models2 import PostSignatureCondition

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Signature
    out = client.pre_signed_post_signature(bucket=bucket_name, key=object_key,
                                            # # Additional information can be added through the optional parameter conditions.
                                           conditions=[PostSignatureCondition(key='x-tos-acl', value='private')])

    print("Algorithm:", out.algorithm)
    print("Date:", out.date)
    print("Policy:", out.policy)
    print("Signature:", out.signature)
    print("Credential:", out.credential)
    print("OriginPolicy:", out.origin_policy)
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

For details on POST form presign, see [Form Signing in Browser-Based Uploads](https://docs.byteplus.com/docs/tos/reference-browser-based-upload-forms-include-signatures).
