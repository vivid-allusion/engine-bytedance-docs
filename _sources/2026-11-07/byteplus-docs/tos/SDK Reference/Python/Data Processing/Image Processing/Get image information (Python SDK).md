---
title: "Get image information (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-image-information-python-sdk"
---

The get image information feature retrieves basic image details, including width, height, size, and format. If the image contains Exif information, it will be returned in JSON format. This article explains how to get image information through the TOS Python SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Example code

The following code demonstrates how to get image information.

```python
import json
import os
import tos
from tos.enum import TierType
from tos.models2 import RestoreJobParameters

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
image_key = "image.png"
style = "image/info"

try:
     # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.put_object_from_file(bucket=bucket_name, key=image_key, file_path=image_key)
    object_stream = client.get_object(bucket=bucket_name, key=image_key, process=style)
    image_info = json.load(object_stream)
    print(image_info)
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
## Related documentation

For detailed information on getting image data, see [Get information](https://docs.byteplus.com/docs/tos/docs-information-query).
