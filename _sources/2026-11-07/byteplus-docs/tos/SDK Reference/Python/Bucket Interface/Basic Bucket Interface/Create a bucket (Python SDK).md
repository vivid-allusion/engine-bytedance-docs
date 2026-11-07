---
title: "Create a bucket (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-a-bucket-python-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. Provided to the user to create a new bucket with the specified bucket name, the newly created bucket name must be unique in TOS. This article describes how to create a bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Bucket [Naming Convention](https://docs.byteplus.com/docs/tos/docs-common-concepts) As follows:

   * Only lowercase letters a to z, numbers, and dashes (\-) can be included.

   * The beginning and end can only be numbers or letters.

   * The length must be between 3 and 63 characters.

* When accessing TOS through other BytePlus products in the same region as TOS, it is recommended that you use the intranet endpoint. For more information on regions and endpoints, see [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a bucket, you need to ensure that your account has `tos: CreateBucket`permission. You can grant appropriate permissions through IAM policies. For specific steps, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".56S65L6L5Luj56CB"></span>
## **Sample code**

The following code is used to create a `bucket-test`.

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
    # Specify the storage class when creating a storage space, optional parameter storage_class
    # Specify the bucket access permission when creating a storage space, optional parameter acl
    # Specify the bucket AZ redundancy when creating a storage space, optional parameter az_redundancy
    # Use the configuration of bucket as standard storage type, private access permission, and 3AZ data redundancy as an example.
    client.create_bucket(bucket_name, acl=tos.ACLType.ACL_Private,
                         storage_class=tos.StorageClassType.Storage_Class_Standard,
                         az_redundancy=tos.AzRedundancyType.Az_Redundancy_Multi_Az)
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

For API documentation on creating buckets, see [CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket).
