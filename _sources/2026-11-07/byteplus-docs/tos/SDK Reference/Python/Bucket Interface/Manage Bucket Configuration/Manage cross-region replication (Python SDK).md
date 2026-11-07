---
title: "Manage cross-region replication (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-region-replication-python-sdk"
---

TOS supports cross\-region replication, allowing you to copy objects from one region to buckets in different regions. When cross\-region replication rules are enabled, when you upload a new file in the source bucket, TOS automatically syncs the file to the destination bucket. This function is used to meet the requirements of off\-site disaster recovery and data replication.

<span id=".6K6-572u6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Set cross\-regional replication rules

<span id=".5rOo5oSP5LqL6aG5"></span>
### Precautions


* After cross\-region rules are turned on, the corresponding files will be synchronized.

* Cross\-region replication uses an asynchronous replication mechanism that can take anywhere from a few minutes to a few hours, depending on the size of your file.

* A single bucket can create up to 100 cross\-region replication rules.

* Cross\-region replication can only be enabled if the source and destination buckets have the same versioning state.

* To set cross\-regional replication rules for buckets, you must be the bucket owner by default.

* When the CRR task is executed, when both `StorageClassType`and `StorageClassInheritDirectiveType`are set, the configuration of `StorageClassType`shall prevail.

* When only `StorageClassInheritDirectiveType`is set, the configuration value is consistent with the source object when it is `Storage_Class_ID_Source_Object`, and the configuration item value is consistent with the target bucket when it is `Storage_Class_ID_Destination_Bucket`.

* `When neither StorageClassType`nor `StorageClassInheritDirectiveType`is set, the default policy is used to match the storage type of the target bucket.


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the cross\-region replication rules for `bucket-test`.

```python
import os
import tos
from tos import StatusType, StorageClassInheritDirectiveType, StorageClassType
from tos.models2 import ReplicationRule, Destination


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
dest_region = "your crr dest region"
bucket_name = "bucket-test"
dest_bucket_name = "bucket-crr"

try:
    # Create TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Set cross-region public rules
    rule = ReplicationRule(
        # Rule ID
        id='1',
        # Specify whether to enable cross-region replication rule
        status=StatusType.Status_Enable,
        # Specify the destination where the data should be replicated to
        destination=Destination(
            # Specify the target Bucket where the data should be copied to
            bucket=dest_bucket_name,
            # Specify the Region where the target Bucket is located
            location=dest_region),
        historical_object_replication=StatusType.Status_Enable
    )
    # Specify the prefix of the matching objects for cross-region replication. Only objects that match this prefix will be copied to the destination bucket.
    # prefix_set = ['prefix1', 'prefix2']
    # Set up the cross-region replication rule.
    # replica_config = ReplicationRule(
    #     # Rule ID
    #     id='1',
    #     # Specify whether to enable the cross-region replication rule (Status_Enable) or disable it (Disabled)
    #     status=StatusType.Status_Enable,
    #     # Specify the destination where the data should be replicated to
    #     destination=Destination(
    #         # Specify the destination bucket where the data should be replicated to
    #         bucket=dest_bucket_name,
    #         # Specify the region where the destination bucket is located
    #         location=dest_region,
    #         # Specify the storage class
    #         storage_class=StorageClassType.Storage_Class_Ia,
    #         # Specify the storage class of the replicated objects, inherit the storage class of the source object (Storage_Class_ID_Source_Object) or the destination bucket (Storage_Class_ID_Destination_Bucket)
    #         storage_class_inherit_directive=StorageClassInheritDirectiveType.Storage_Class_ID_Source_Object
    #     ),
    #     # Specify the object prefix for the matching rule
    #     prefix_set=prefix_set,
    #     # Specify whether to enable replication of historical objects
    #     historical_object_replication=StatusType.Status_Enable,
    # )
    # Set up the cross-region replication rule
    # When configuring the cross-region replication rule, you must create the corresponding role in the access configuration and grant access permissions to TOS resources
    # The role_name is the name of the role created above.
    client.put_bucket_replication(bucket_name, 'your role', [rule])
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


<span id=".5p-l55yL6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## View cross\-region replication rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain cross\-regional replication rules for buckets, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain cross\-region replication rules for `bucket-test`.

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
    # Retrieve the replication rules for all objects in the bucket (when rule_id is not specified)
    out = client.get_bucket_replication(bucket_name)
    # Retrieve the replication rule with the specified rule_id
    # out = client.get_bucket_replication(bucket_name, rule_id='your rule id')
    # Output all the replication rules configured for the bucket
    for rule in out.rules:
        # Output the current rule ID's cross-region replication rule configuration information.
        print('rule id', rule.id)
        print('prefix set', rule.prefix_set)
        print('status', rule.status)
        print('historical object replication', rule.historical_object_replication)
        print('location', rule.destination.location)
        print('targe bucket', rule.destination.bucket)
        print('storage_class', rule.destination.storage_class)
        print('storage class inherit directive', rule.destination.storage_class_inherit_directive)
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


<span id=".5p-l55yL6Leo5Yy65Z-f5aSN5Yi26L-b5bqm"></span>
## View cross\-region replication progress

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To get the cross\-regional replication progress of a bucket, you must be the bucket owner by default.</div>


* <div data-tips="true" data-tips-type="warning">Historical data replication progress is expressed as a percentage and is only valid for storage spaces where historical data replication is enabled.</div>


* <div data-tips="true" data-tips-type="warning">The new write data replication progress is represented by the point in time of the new write data.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to get the cross\-region replication progress for `bucket-test`.

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
    # Return the replication progress of all objects without specifying a rule_id
    out = client.get_bucket_replication(bucket_name)
    # Query the replication progress of a specific rule_id by specifying rule_id='your rule id'
    # out = client.get_bucket_replication(bucket_name, rule_id='your rule id')

    # Output the replication progress of all objects currently configured for the bucket
    for rule in out.rules:
        # Output the cross-region replication progress for the current rule id.
        print('rule id', rule.id)
        print('new object progress', rule.progress.new_object)
        print('historical object progress', rule.progress.historical_object)

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


<span id=".5Yig6Zmk6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Delete cross\-region replication rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Remove the cross\-region replication rule for buckets. By default, you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code removes the cross\-region replication rule for `bucket-test`.

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
    # Create TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Delete cross-region replication rule
    client.delete_bucket_replication(bucket_name)
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
