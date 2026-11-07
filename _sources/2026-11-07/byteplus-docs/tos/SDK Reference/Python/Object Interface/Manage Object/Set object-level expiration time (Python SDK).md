---
title: "Set object-level expiration time (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-object-level-expiration-time-python-sdk"
---

You can set the expiration time of an uploaded object through the `set_object_expires` interface of the TOS Python SDK. After expiration, TOS will automatically delete the object.

<span id="ab21f5da"></span>
## **Notes**


* To set object\-level expiration time, you must have the `tos:SetObjectExpires` permission. For detailed operations, see the [permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Using the Python SDK to set object\-level expiration time requires Python SDK version 2.8.5 or higher.


<span id="6f833653"></span>
## Example code

```Python
import os
import tos

#  Retrieve AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
# Object name; for example, if the object is the file example_object.txt under example_dir, enter example_dir/example_object.txt
object_key = "object-test"
try:
    # Create a TosClientV2 object; operations on buckets and objects are performed through TosClientV2
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Set object-level expiration time; value must be a positive integer or 0; a value of 0 means never expire.
    object_expires = 1
    client.set_object_expires(bucket_name, object_key, object_expires)
except tos.exceptions.TosClientError as e:
    # Operation failed, client exception caught; usually due to invalid request parameters or network issues
    print('fail with client error, message:{}, cause: {}'.format(e.message, e.cause))
except tos.exceptions.TosServerError as e:
    # Operation failed, server exception caught; detailed error information can be obtained from the response
    print('fail with server error, code: {}'.format(e.code))
    # The request ID can be used to pinpoint specific issues; it is highly recommended to log this ID
    print('error with request id: {}'.format(e.request_id))
    print('error with message: {}'.format(e.message))
    print('error with http code: {}'.format(e.status_code))
    print('error with ec: {}'.format(e.ec))
    print('error with request url: {}'.format(e.request_url))
except Exception as e:
    print('fail with unknown error: {}'.format(e))
```


<span id="c9101722"></span>
## **Related documentation**

For API documentation on setting object\-level expiration time, see [SetObjectExpires](https://docs.byteplus.com/docs/tos/SetObjectExpires).
