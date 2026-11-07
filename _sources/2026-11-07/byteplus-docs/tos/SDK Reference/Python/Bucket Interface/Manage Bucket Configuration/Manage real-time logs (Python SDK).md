---
title: "Manage real-time logs (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-real-time-logs-python-sdk"
---

TOS supports log analysis capabilities, allowing you to retrieve and analyze access logs generated during your visit to TOS through log services. With the TOS Python SDK, you can configure the log analysis function.

<span id=".6K6-572u5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## Set up real\-time log configuration rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To use the log analysis feature, you need to have the log service enabled and authorized TOS to access the BytePlus log service TLS.</div>


* <div data-tips="true" data-tips-type="warning">After enabling the log analysis function, the log service will automatically create log items and topics to store the relevant logs of the TOS.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the live log configuration rules for `bucket-test`.

```python
import os
import tos

from tos.models2 import RealTimeLogConfiguration, AccessLogConfiguration

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    config = RealTimeLogConfiguration(
        # Role Name
        role='TOSLogTLSRole',
        # Set to true to use the log topic provided by the server
        configuration=AccessLogConfiguration(use_service_topic=True)
    )
    client.put_bucket_real_time_log(bucket_name, config)

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


<span id=".6I635Y-W5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## Get real\-time log configuration rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the live log configuration rules for a bucket, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the live log configuration rules for `bucket-test`.

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
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    out = client.get_bucket_real_time_log(bucket_name)
    print('role', out.configuration.role)
    print('tls topic id', out.configuration.configuration.tls_topic_id)
    print('tls project id', out.configuration.configuration.tls_project_id)
    print('use service topic', out.configuration.configuration.use_service_topic)

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


<span id=".5Yig6Zmk5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## Delete live log configuration rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To remove a live log configuration rule for a bucket, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code removes the live log configuration rule for `bucket-test`.

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
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    client.delete_bucket_real_time_log(bucket_name)
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
