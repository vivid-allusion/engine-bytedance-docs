---
title: "Video frame capture image Persistence (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-capture-image-persistence-python-sdk"
---

TOS supports saving images captured from video frames to a specified bucket. This article explains how to save images captured from video frames to a specified bucket using the TOS Python SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Example Code

The following code shows how to capture the video frame at 300 ms, name the captured image temp.jpg, and save it to the target bucket.

```python
import base64
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
style = "video/snapshot,t_300" # Extract video frame at 300ms.
save_bucket = "your destination bucket name"
save_object = "temp.jpg"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    object_stream = client.get_object(
        bucket=bucket_name,
        key=video_key,
        process=style,
        save_bucket=base64.b64encode(save_bucket.encode("utf-8")).decode("utf-8"),
        save_object=base64.b64encode(save_object.encode("utf-8")).decode("utf-8")
    )
    print(object_stream.read())
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

For detailed information on video frame capture image persistence, see [image persistence](https://docs.byteplus.com/docs/tos/docs-image-storage).
