---
title: "Exception handling (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-python-sdk"
---

This article introduces exception handling when using the TOS SDK.

<span id=".dG9zLeacjeWKoeerr-mUmeivrw=="></span>
## TOS Server Errors

The TOS server follows HTTP standards and defines detailed HTTP status codes and business error codes for failed request scenarios. For details, refer to [TOS Server Status Codes and Error Code Definitions](https://docs.byteplus.com/docs/6349/74874).

<span id=".c2RrLeiHquWumuS5ieW8guW4uC3plJnor68="></span>
## SDK Custom Exceptions/Errors

<span id=".5a6i5oi356uv5byC5bi4LemUmeivry10b3NjbGllbnRlcnJvcg=="></span>
### Client Exceptions/Errors \- TosClientError

TosClientError occurs due to client input errors, connection timeouts, or special operations such as client cancellation of breakpoint resume uploads. For example, when creating a bucket using create_bucket, an exception is thrown if the bucket name exceeds 63 characters.

<span id=".5pyN5Yqh56uv5byC5bi4LemUmeivry10b3NzZXJ2ZXJlcnJvcg=="></span>
### Server Exceptions/Errors \- TosServerError

Send requests to the TOS server using the TOS Python SDK interface. The response includes HTTP\-compliant status codes and business error codes that indicate the current request's response status.

<span id=".5byC5bi4LemUmeivr-WkhOeQhuekuuS-iw=="></span>
### Example of exception/error handling

The following code demonstrates exception handling when downloading a nonexistent object. If a TosServerError occurs, it prints the HTTP request status code and request ID; if a TosClientError occurs, it prints the error message.

```python
import os
import tos

# Get AK and SK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Download object
    resp = client.get_object(bucket_name, object_key)
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
