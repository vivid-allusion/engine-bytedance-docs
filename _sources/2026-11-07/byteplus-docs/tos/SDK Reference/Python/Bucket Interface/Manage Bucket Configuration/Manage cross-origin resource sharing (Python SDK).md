---
title: "Manage cross-origin resource sharing (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-origin-resource-sharing-python-sdk"
---

Set Cross\-Origin Resource Sharing (CORS) rules. When TOS receives a cross\-origin request or OPTIONS request, it will read the CORS rules corresponding to the bucket, perform corresponding permission checks and return corresponding headers to ensure the security of cross\-origin data transmission. This article describes how to configure CORS for buckets.

<span id=".6K6-572u6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## Set CORS rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To set CORS rules for buckets, you must have the <code>tos: PutBucketCORS</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the CORS rules for `bucket-test`.

```python
import os
import tos

from tos.models2 import CORSRule

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    rule = CORSRule(allowed_origins=['*'],
                    allowed_methods=['GET', 'HEAD'],
                    allowed_headers=['*'],
                    max_age_seconds=1000)

    # The existing rules will be overridden.
    client.put_bucket_cors(bucket_name, [rule])
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


<span id=".6I635Y-W6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## Get CORS rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain CORS rules for buckets, you must have the <code>tos: GetBucketCORS</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the CORS rules for `bucket-test`.

```python
import os
import tos

from tos.models2 import CORSRule

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # If no CORS rules are set, a tos.exceptions.TosServerError will be thrown.
    cors = client.get_bucket_cors(bucket_name)
    for rule in cors.cors_rules:
        print('AllowedOrigins={}'.format(rule.allowed_origins))
        print('AllowedMethods={}'.format(rule.allowed_methods))
        print('AllowedHeaders={}'.format(rule.allowed_headers))
        print('ExposeHeaders={}'.format(rule.expose_headers))
        print('MaxAgeSeconds={}'.format(rule.max_age_seconds))
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


<span id=".5Yig6Zmk6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## Delete CORS rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To remove a CORS rule for a bucket, you must have the <code>tos: PutBucketCORS</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code deletes the CORS rule for the specified bucket.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Delete the CORS configuration for a bucket
    client.delete_bucket_cors(bucket_name)
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

For more information on cross\-origin resource sharing, see [CORS rules](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).
