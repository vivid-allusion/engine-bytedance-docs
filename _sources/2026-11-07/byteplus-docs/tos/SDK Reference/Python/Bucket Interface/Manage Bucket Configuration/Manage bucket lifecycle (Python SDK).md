---
title: "Manage bucket lifecycle (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-the-bucket-lifecycle-python-sdk"
---

TOS supports setting bucket lifecycle rules, automatically deleting expired objects and unmerged sharding data, or converting expired objects to low\-frequency or archived storage types, thus saving users storage costs. This article describes how to manage bucket lifecycle rules.

<span id=".6K6-572u55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## Set lifecycle rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To set lifecycle rules for buckets, you must have <code>tos: PutLifecycleConfiguration</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">If a bucket has been configured with a lifecycle rule, performing this operation will overwrite the original configuration. To append a lifecycle rule, use GetLifecycleConfiguration to get the current rule, append and write a new rule, and finally call PutLifecycleConfiguration update rule.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets lifecycle rules for the bucket `bucket-test`.

```python
import datetime

import os
import tos
from tos import StatusType, StorageClassType
from tos.models2 import BucketLifeCycleRule, BucketLifeCycleExpiration, BucketLifeCycleAbortInCompleteMultipartUpload, \
    BucketLifeCycleTransition, Tag, BucketLifeCycleNonCurrentVersionTransition, \
    BucketLifeCycleNoCurrentVersionExpiration

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    # Create a TosClientV2 object to perform operations on buckets and objects.
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Set to expire after 70 days of creation.
    rule1 = BucketLifeCycleRule(id='rule1', prefix='test1/',
                                status=StatusType.Status_Enable,
                                expiration=BucketLifeCycleExpiration(days=70))

    # Set the expiration time for the date object.
    rule2 = BucketLifeCycleRule(id='rule2', prefix='test2/',
                                status=StatusType.Status_Enable,
                                expiration=BucketLifeCycleExpiration(date=datetime.datetime(2022, 11, 30)))

    # Set shard expiration rules, with an expiration time of 10 days after creation.
    rule3 = BucketLifeCycleRule(id='rule3', prefix='test3/',
                                status=StatusType.Status_Enable,
                                abort_in_complete_multipart_upload=BucketLifeCycleAbortInCompleteMultipartUpload(
                                    days_after_init=10))

    # Set conversion rules for the object, specifying that the object will be converted to low frequency after 30 days.
    rule4 = BucketLifeCycleRule(id='rule4', prefix='test4/',
                                status=StatusType.Status_Enable,
                                transitions=[BucketLifeCycleTransition(days=30,
                                                                       storage_class=StorageClassType.Storage_Class_Ia)])

    # Set matching tags, different from rule 4, this rule requires the object to have the corresponding tag set in addition to matching the prefix in order to be matched.
    rule5 = BucketLifeCycleRule(id='rule5', prefix='test5/',
                                status=StatusType.Status_Enable,
                                transitions=[BucketLifeCycleTransition(days=30,
                                                                       storage_class=StorageClassType.Storage_Class_Ia)],
                                tags=[Tag('key1', 'value1')])

    # rule6 for buckets with multiple versions enabled
    # Set the latest version to expire after 70 days
    # Convert historical versions to infrequent access storage after 30 days
    # Expire historical versions after 40 days
    rule6 = BucketLifeCycleRule(id='rule6', prefix='test6/',
                                status=StatusType.Status_Enable,
                                expiration=BucketLifeCycleExpiration(days=70),
                                non_current_version_transitions=[
                                    BucketLifeCycleNonCurrentVersionTransition(non_current_days=30,
                                                                               storage_class=StorageClassType.Storage_Class_Ia)],
                                no_current_version_expiration=BucketLifeCycleNoCurrentVersionExpiration(
                                    no_current_days=40))

    lifecycle = [rule1, rule2, rule3, rule4, rule5, rule6]
    out = client.put_bucket_lifecycle(bucket_name, lifecycle)
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


<span id=".6I635Y-W55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## Get lifecycle rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get the bucket setup lifecycle rule, you must have <code>tos: GetLifecycleConfiguration</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the lifecycle rules for `bucket-test`.

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
    rules = client.get_bucket_lifecycle(bucket_name)
    for rule in rules.rules:
        print('id:', rule.id)
        print('prefix', rule.prefix)
        print('status', rule.status.value)

        if rule.tags is not None:
            for tag in rule.tags:
                print('tag key:{}, value:{}'.format(tag.key, tag.value))

        if rule.abort_in_complete_multipart_upload is not None:
            if rule.abort_in_complete_multipart_upload.days_after_init is not None:
                print('abort_in_complete_multipart_upload:', rule.abort_in_complete_multipart_upload.days_after_init)

        if rule.expiration is not None:
            if rule.expiration.date is not None:
                print('expiration_date', rule.expiration.date)
            else:
                print('expiration_days', rule.expiration.days)

        if rule.transitions is not None:
            if len(rule.transitions) > 0:
                for transition in rule.transitions:
                    if transition.days is not None:
                        print('transition_days', transition.days)
                    else:
                        print('transition_date', transition.date)
                    print('transition_storage_class', transition.storage_class.value)

        if rule.no_current_version_expiration is not None:
            if rule.no_current_version_expiration.no_current_days is not None:
                print('no_current_version_expiration.no_current_days',
                      rule.no_current_version_expiration.no_current_days)

        if rule.non_current_version_transitions is not None:
            if len(rule.non_current_version_transitions) > 0:
                for non_current_version_transition in rule.non_current_version_transitions:
                    print('non_current_version_transition_days', non_current_version_transition.non_current_days)
                    print('non_current_version_transition_storage_class',
                          non_current_version_transition.storage_class.value)
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


<span id=".5Yig6Zmk55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## Delete lifecycle rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the bucket lifecycle rule, you must have <code>tos: PutLifecycleConfiguration</code> permission, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code removes the lifecycle rules for `bucket-test`.

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
    # Delete the lifecycle rules of a bucket
    client.delete_bucket_lifecycle(bucket_name)
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

For more information on lifecycle rules, please refer to [Setting lifecycle rules](https://docs.byteplus.com/docs/tos/Lifecycle-rules-based-on-last-accesstime).
