---
title: "Manage event notifications (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Managing-event-notifications-python-sdk"
---

TOS supports delivering partial event changes to function services. If you want to keep track of resource changes in TOS in real time, you can set up event notification rules. This article describes sample code for event notification.

<span id=".6K6-572u5LqL5Lu26YCa55-l6KeE5YiZ"></span>
## Set up event notification rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A bucket can only create a maximum of 10 event notification rules.</div>


* <div data-tips="true" data-tips-type="warning">An event notification rule can only choose one push target, a function service.</div>


* <div data-tips="true" data-tips-type="warning">An object cannot match multiple rules containing the same event type, that is, in the same bucket, the combined range of <strong>type + prefix + suffix</strong> between different rules is not allowed to overlap.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets event notification rules for `bucket-test`.

```python
import os
import tos
from tos.models2 import CloudFunctionConfiguration, Filter, FilterKey, FilterRule

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"
cloudFunction = 'your cloud function'
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    config = CloudFunctionConfiguration(
        # Event Notification ID
        id='1',
        # Event Type
        events=['tos:ObjectCreated:Put', 'tos:ObjectCreated:Post'],
        # Filter Rules
        filter=Filter(
            key=FilterKey(
                rules=[
                    # Set up the prefix information for the matching object.
                    FilterRule(name='prefix', value='your prefix'),
                    # Set up the suffix information to be matched with the target objects.
                    FilterRule(name='suffix', value='your suffix'),
                ]
            )),
        # Function Service Name
        cloud_function=cloudFunction
    )
    out = client.put_bucket_notification(bucket_name, [config])
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


<span id=".6I635Y-W5LqL5Lu26YCa55-l6KeE5YiZ"></span>
## Get event notification rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain event notification rules for a bucket, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain event notification rules for `bucket-test`.

```python
import os
import tos

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
region = "your region"
bucket_name = "bucket-test"
try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    out = client.get_bucket_notification(bucket_name)
    for n in out.cloud_function_configurations:
        print('id', n.id)
        print('events', n.events)
        print('cloud function', n.cloud_function)
        if n.filter and n.filter.key and n.filter.key.rules:
            for rule in n.filter.key.rules:
                print('filter name', rule.name)
                print('filter value', rule.value)
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
