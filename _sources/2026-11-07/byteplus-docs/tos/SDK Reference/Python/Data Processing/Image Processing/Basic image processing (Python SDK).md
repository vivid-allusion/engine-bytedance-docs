---
title: "Basic image processing (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Basic-image-processing-python-sdk"
---

TOS supports image processing operations on stored images, including resizing, cropping, watermarking, and format conversion. This article explains how to perform basic image processing using the TOS Python SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The original image can be only in the JPG, PNG, BMP, GIF, WEBP, or TIFF format.

* The source image can be up to 20 MB.

* The source image can have up to 30,000 pixels (width/height) and 250 million pixels in total (the width and height cannot exceed 4,096 pixels for the rotate operation).

* The resized image can have up to 16,384 pixels (both width and height) and 16,777,216 pixels in total.


<span id=".56S65L6L5Luj56CB"></span>
## Example code

The following code shows how to fix the image height at 100 px, convert the image format to JPG, name the image temp.jpg, and download it locally.

```python
import os
import tos
from tos.enum import TierType
from tos.models2 import RestoreJobParameters

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
region = "your region"
bucket_name = "bucket-test"
image_key = "image.png"
file_name = "temp.jpg"
style = "image/resize,h_100/format,jpg"  # Keep the image height fixed at 100px and convert it to JPG format.

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.get_object_to_file(bucket=bucket_name, key=image_key, process=style, file_path=file_name)
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

For detailed information on image processing, see [Image processing overview](https://docs.byteplus.com/docs/tos/docs-overview_2).
