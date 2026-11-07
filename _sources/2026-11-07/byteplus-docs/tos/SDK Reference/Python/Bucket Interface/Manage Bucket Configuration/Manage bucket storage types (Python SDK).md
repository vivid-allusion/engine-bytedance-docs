---
title: "Manage bucket storage types (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-storage-types-python-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. TOS provides a variety of bucket storage types, which can be applied to various application scenarios. This article describes how to set the storage type of a bucket.

<span id=".5a2Y5YKo57G75Z6L6K-05piO"></span>
## Storage type description

Bucket storage types include the following categories. For more information on storage types, see [Storage Type](https://docs.byteplus.com/docs/tos/docs-storage-type) .


|**storage type** |**describe** |storage type enumeration value |
|---|---|---|
|Standard storage |The default storage type of the bucket is suitable for various business scenarios such as social networking, sharing pictures, audio & video applications, large websites, and big data analytics, such as program downloads, mobile applications, etc. |tos.StorageClassType.Storage_Class_Standard |
|Low Frequency Storage |It is suitable for business scenarios with low access frequency (average access frequency 1 to 2 times per month), such as hot standby data, surveillance video data, etc. |tos.StorageClassType.Storage_Class_Ia |
|archive flashback storage |Business scenarios that require long\-term preservation and are less accessible, such as archives. |tos.StorageClassType.Storage_Class_Archive_Fr |
|Intelligent Tiered Storage |It is suitable for data with uncertain access frequency, and the access layer can be switched according to the access frequency to reduce storage costs. |tos.StorageClassType.Storage_Class_INTELLIGENT_TIERING |
|cold archive storage |It is a cold data type and is suitable for business scenarios that require minimal access and long\-term storage of data. A minimum of 180 days of storage is required; data needs to be restored before accessing cold archived data. |tos.StorageClassType.Storage_Class_Cold_Archive |


<span id=".6K6-572u5a2Y5YKo57G75Z6L"></span>
## Set storage type

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Set the bucket storage type. By default, only the bucket owner has this permission.</div>


* <div data-tips="true" data-tips-type="warning">After setting the bucket storage type, if the object storage type is not specified when uploading objects, copying objects, and initializing the shard upload task, the object inherits the bucket storage type.</div>


* <div data-tips="true" data-tips-type="warning">When creating a bucket, if the bucket storage type is not specified, the default storage type is standard storage.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the storage type of the `bucket-test`bucket.

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
    # Set the bucket type to IA
    client.put_bucket_storage_class(bucket_name, tos.StorageClassType.Storage_Class_Ia)
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


<span id=".6I635Y-W5qG25a2Y5YKo57G75Z6L"></span>
## Get bucket storage type

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Gets the bucket storage type. By default, only the bucket owner has this permission.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to get the storage type of the `bucket-test`.

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
    # Use the head_bucket method to retrieve the storage type of a bucket
    resp = client.head_bucket(bucket_name)
    print('bucket storage class {}'.format(resp.storage_class.value))
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

For more information on storage types, see [Storage Type](https://docs.byteplus.com/docs/tos/docs-storage-type) .
