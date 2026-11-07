---
title: "Manage bucket policy (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-strategy-python-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. In TOS, permission control is realized by IAM policy, bucket policy, bucket and object ACL. Bucket policy and ACL are both rights control policies based on TOS resources. Compared with bucket ACL, bucket policy has more flexible permission configuration. This article describes how to set, obtain, and delete bucket policies.

<span id=".6K6-572u5qG2562W55Wl"></span>
## Set bucket policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To set the bucket policy, you must have the <code>tos: PutBucketPolicy</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">Users with this permission can change the bucket policy arbitrarily, and can obtain other permissions through this permission. It is recommended that you configure it carefully.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the bucket policy for `bucket-test`.

```python
import json

import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Configure Policy permissions for all users to have ListBucket access
    policy = {
        "Statement": [
            {
                "Sid": "internal public",
                "Effect": "Allow",
                "Action": ["tos:ListBucket"],
                "Principal": "*",
                "Resource": [
                    "trn:tos:::{}/*".format(bucket_name),
                    "trn:tos:::{}".format(bucket_name),
                ],
            }
        ]
    }
    client.put_bucket_policy(bucket_name, policy=json.dumps(policy))
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


<span id=".6I635Y-W5qG2562W55Wl"></span>
## Get bucket policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get the bucket policy, you must have the <code>tos: GetBucketPolicy</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the bucket policy for `bucket-test`.

```python
import json

import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)

    resp = client.get_bucket_policy(bucket_name)
    policy_json = json.loads(resp.policy)
    print('Get policy text: {}'.format(policy_json))
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


<span id=".5Yig6Zmk5qG2562W55Wl"></span>
## Delete bucket policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the bucket policy, you must have the <code>tos: DeleteBucketPolicy</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code removes the bucket policy for `bucket-test`.

```python
import json

import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.delete_bucket_policy(bucket_name)
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

For more information on bucket policies, see [Bucket policy management](https://docs.byteplus.com/docs/tos/docs-bucket-authorization-policy-management).
