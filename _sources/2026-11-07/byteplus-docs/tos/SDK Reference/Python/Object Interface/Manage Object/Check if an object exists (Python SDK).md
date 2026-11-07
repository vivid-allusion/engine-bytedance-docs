---
title: "Check if an object exists (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Determine-whether-an-object-exists-python-sdk"
---

You can check if an object exists using the `head_object` interface of the Python SDK.

<span id="ef2e632c"></span>
## Notes

To check if an object exists, your account must have the `tos:GetObject` permission. For details, see the [permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

<span id="6f9443f1"></span>
## Example code

The following code shows how to check if an object exists.

```Python
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
    # Get object metadata
    result = client.head_object(bucket_name, object_key)
except tos.exceptions.TosClientError as e:
    # Operation failed, catch client error, usually caused by invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    if e.status_code == 404:
        print("Object not found.")
    else:
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


<span id="f745ec63"></span>
## **Related documentation**

For API interfaces related to checking if an object exists, see [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
