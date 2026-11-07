---
title: "Get video information (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-video-information-python-sdk"
---

The get video information feature retrieves metadata of a specified video resource. This article explains how to get video information using the TOS Python SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code shows how to get video information.

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
video_key = "video.mp4"
style = "video/info"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.put_object_from_file(bucket=bucket_name, key=video_key, file_path=video_key)
    object_stream = client.get_object(bucket=bucket_name, key=video_key, process=style)
    video_info = json.load(object_stream)
    print(video_info)
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

For detailed information about getting video information, see [View video information](https://docs.byteplus.com/docs/tos/docs-viewing-video-information).
