---
title: "Video frame capture (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-framing-python-sdk"
---

The video frame capture feature extracts a single frame at a specified moment from a video stream and scales it to the specified size as an image. This article explains how to capture video frames using the TOS Python SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Example Code

The following code demonstrates how to capture the video frame at 300 ms and download the resulting image locally.

```python
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
file_name = "temp.jpg"
style = "video/snapshot,t_300"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.put_object_from_file(bucket=bucket_name, key=video_key, file_path=video_key)
    client.get_object_to_file(bucket=bucket_name, key=video_key, process=style, file_path=file_name)
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

For detailed information about video frame capture, see [Video Frame Capture](https://docs.byteplus.com/docs/tos/docs-video-frame-capture).
