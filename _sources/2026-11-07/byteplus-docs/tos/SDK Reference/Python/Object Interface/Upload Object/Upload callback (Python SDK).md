---
title: "Upload callback (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-callback-python-sdk"
---

Upload callback means that the client side carries the callback (Callback) parameter when the request is made. After the upload is completed, the server level sends a synchronized POST callback request to the third\-party app server specified in CallBack. After the server confirms acceptance and returns the result, all the results are returned to the client side.

<span id="0fc39842"></span>
## Sample code

<span id="76b5479a"></span>
### Normal upload realizes upload callback

```Python
import os
from io import StringIO
import base64
import json
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
content = StringIO('Hello TOS')
callback_url = "*** Provide your callback url ***"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    callback_param = {
        "callbackUrl": callback_url,
        "callbackBody": "{\"bucket\": ${bucket}, \"object\": ${object}, \"key1\": ${x:key1}}",
        "callbackBodyType": "application/json",
    }
    callback = json.dumps(callback_param)
    callback_var_param = {"x:key1": "ceshi"}
    callback_var = json.dumps(callback_var_param)
    result = client.put_object(bucket_name, object_key, content=content,
                      callback=base64.b64encode(callback.encode('utf-8')).decode('utf-8'),
                      callback_var=base64.b64encode(callback_var.encode('utf-8')).decode('utf-8'))
    # HTTP Status Code
    print('http status code:{}'.format(result.status_code))
    # Request ID. The request ID is a unique identifier for this request. It is recommended to include this parameter in the logs.
    print('request_id: {}'.format(result.request_id))            
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


<span id="a9de9059"></span>
### Shard upload to achieve upload callback

```Python
import os
import base64
import json
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
upload_id = "*** Provide your upload id ***"
callback_url = "*** Provide your callback url ***"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    callback_param = {
        "callbackUrl": callback_url,
        "callbackBody": "{\"bucket\": ${bucket}, \"object\": ${object}, \"key1\": ${x:key1}}",
        "callbackBodyType": "application/json",
    }
    callback = json.dumps(callback_param)
    callback_var_param = {"x:key1": "ceshi"}
    callback_var = json.dumps(callback_var_param)
    result = client.complete_multipart_upload(bucket_name, object_key,
                                 upload_id=upload_id,
                                 callback=base64.b64encode(callback.encode('utf-8')).decode('utf-8'),
                                 callback_var=base64.b64encode(callback_var.encode('utf-8')).decode('utf-8'))
    # HTTP Status Code
    print('http status code:{}'.format(result.status_code))
    # Request ID. The request ID is a unique identifier for this request. It is recommended to include this parameter in the log.
    print('request_id: {}'.format(result.request_id))            
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
