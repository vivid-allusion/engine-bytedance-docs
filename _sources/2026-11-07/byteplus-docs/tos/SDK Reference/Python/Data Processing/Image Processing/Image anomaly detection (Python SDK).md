---
title: "Image anomaly detection (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Abnormal-image-detection-python-sdk"
---

Image anomaly detection identifies suspicious files other than images in the image file, such as MPEG\-TS files. If suspicious files are detected in the image, you can process the image file to prevent illegal use of storage space by image hosting services. This document explains how to perform image anomaly detection using the TOS Python SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The original image size for detection must not exceed 20 MB.

* Image anomaly detection supports only JPG, JPEG, PNG, BMP, GIF, and pure TS video stream formats.

* The image anomaly detection service charges by the number of operations. For details, see [Data processing](https://docs.byteplus.com/docs/tos/docs-data-processing-fee).


<span id=".56S65L6L5Luj56CB"></span>
## Example code

The following code demonstrates how to detect abnormal images.

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
image_key = "image.png"
style = "image/inspect"

try:
     # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.put_object_from_file(bucket=bucket_name, key=image_key, file_path=image_key)
    object_stream = client.get_object(bucket=bucket_name, key=image_key, process=style)
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
##
