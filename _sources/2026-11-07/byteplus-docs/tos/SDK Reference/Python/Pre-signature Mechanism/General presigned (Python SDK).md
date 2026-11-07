---
title: "General presigned (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-pre-signature-python-sdk"
---

TosClient includes signatures in the request headers by default when sending requests to the server. The SDK also supports generating presigned URLs, which you can use directly to send HTTP requests or share with third parties to authorize access. The examples below show how to upload and download objects using presigned URLs. Other interfaces follow a similar approach.

<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIrkvKDlr7nosaE="></span>
## **Upload an object using a presigned URL**

The following code uses a presigned URL to upload the object `object-test` to the bucket `bucket-test`.

```python
import requests
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
content = b'test pre_signed_url put_object'
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Generate a signed URL for uploading a file with a validity of 3600s
    out = client.pre_signed_url(tos.HttpMethodType.Http_Method_Put, bucket=bucket_name, key=object_key, expires=3600)
    print('签名URL的地址为', out.signed_url)
    # Upload the object using the pre-signed URL, using requests as an example.
    out = requests.put(out.signed_url, content)
    out.close()
    # Download the object
    get_out = client.get_object(bucket_name, object_key)
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


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIvovb3lr7nosaE="></span>
## **Download an object using a presigned URL**

The following code uses a presigned URL to download the object `object-test` from the bucket `bucket-test`.

```python
import requests
import os
import tos
from tos import HttpMethodType

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
content = b'test pre_signed_url get_object'
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Generate a pre-signed URL with signature
    pre_signed_url_output = client.pre_signed_url(HttpMethodType.Http_Method_Get, bucket_name, object_key)
    # Download the object using the pre-signed URL, using requests as an example.
    out = requests.get(pre_signed_url_output.signed_url)
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


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3liKDpmaTlr7nosaE="></span>
## **Delete an object using a presigned URL**

```python
import requests
import os
import tos

# 从环境变量获取 AK 和 SK 信息。
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
object_key = "object-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.create_bucket(bucket_name)
    # Generate a signed URL for deleting a file, with a validity period of 3600 seconds.
    out = client.pre_signed_url(tos.HttpMethodType.Http_Method_Delete, bucket=bucket_name, key=object_key, expires=3600)
    print('签名URL的地址为', out.signed_url)
     # Use pre-signed deletion objects as an example to illustrate with requests.
    out = requests.delete(out.signed_url)
    out.close()
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
## **Related documentation**

For detailed information about URLs containing signatures, see [URL containing signatures](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url).
