---
title: "Manage bucket ACL (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-acl-python-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. This article describes how to set and obtain read and write permissions (ACLs) for buckets.

<span id=".6K6-572u5qG255qE6K6_6Zeu5p2D6ZmQ"></span>
## **Set bucket access**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To set the read and write permissions of the bucket, you must have the tos: PutBucketACL permission, or have the WRITE_ACP bucket ACL permission. For details, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Overview</a>.</div>


<span id=".5qG2LWFjbC3or7TmmI4="></span>
### Bucket ACL permissions

Bucket ACL permissions include the following five categories.


|**Permission** |**Description** |**Value** |
|---|---|---|
|READ |Allows authorized parties to list objects in a bucket |tos.PermissionType.Permission_Read |
|WRITE |Allows authorized parties to create, overwrite, and delete arbitrary objects in the bucket |tos.PermissionType.Permission_Write |
|READ_ACP |Allows authorized parties to read bucket ACLs |tos.PermissionType.Permission_Read_Acp |
|WRITE_ACP |Allows authorized parties to write to bucket ACLs |tos.PermissionType.Permission_Write_Acp |
|FULL_CONTROL |Assigns READ, WRITE, READ_ACP and WRITE_ACP permissions on buckets to authorized parties |tos.PermissionType.Permission_Full_Control |


It can be set by filling in the detailed ACL permission information in the request body or in the request header.

<span id=".6K-35rGC5L2T5Lit5aGr5YaZ6K-m57uGLWFjbC3mnYPpmZDkv6Hmga8="></span>
### **Fill in the detailed ACL permission information in the request body**

The following code is used to set permission information for `bucket-test` in the request body.

```python
import os
import tos

from tos import GranteeType, CannedType, PermissionType
from tos.models2 import Grantee, Grant, Owner

# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = "bucket-test"

try:
    client = tos.TosClientV2(ak, sk, endpoint, region)

    # Grantee is the account ID
    grantee1 = Grantee(GranteeType.Grantee_User, id='account id', display_name='account display name')
    # Grantee is all users in a predefined group
    grantee2 = Grantee(GranteeType.Grantee_Group, canned=CannedType.Canned_All_Users)

    # Grant Permission_Full_Control to the specified account ID
    grant_1 = Grant(grantee1, PermissionType.Permission_Full_Control)
    # Grant Permission_Read to all users
    grant_2 = Grant(grantee2, PermissionType.Permission_Read)

    client.put_bucket_acl(bucket_name, grants=[grant_1, grant_2], owner=Owner("object owner id", 'object owner name'))
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


<span id=".6K-35rGC5aS05Lit6K6-572u6K6_6Zeu5p2D6ZmQ"></span>
### **Set access permissions in the request header**

The read and write permissions of the bucket set through the `x-tos-acl` request header have the following four categories.


|Permission |**Description** |**Value** |
|---|---|---|
|private |Private. The bucket owner has FULL_CONTROL permissions, other users do not have permissions to operate on the object. |tos.ACLType.ACL_Private |
|public reading |Public reading. The owner of the bucket has FULL_CONTROL privileges, other users only have READ privileges on the bucket. |tos.ACLType.ACL_Public_Read |
|public reading and writing |Public reading and writing. All users have FULL_CONTROL permissions. |tos.ACLType.ACL_Public_Read_Write |
|authenticated user read |The bucket owner has FULL_CONTROL privileges, and the authenticated user has READ privileges on the bucket. |tos.ACLType.ACL_Authenticated_Read |


The following code sets the read and write permissions for `bucket-test` using `x-tos-acl`.

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
    # Set the bucket permission to private
    client.put_bucket_acl(bucket_name, acl=tos.ACLType.ACL_Private)
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


The following code uses `x-tos-grant- *` to request read and write permissions to `bucket-test`.

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
    # Set user ID 1000000001 with FULL_CONTROL access, allowing all users to have READ permission on the bucket.
    client.put_bucket_acl(bucket_name, grant_full_control='id="1000000001"', grant_read='canned="AllUsers"')
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


<span id=".6I635Y-W5qG255qE6K6_6Zeu5p2D6ZmQ"></span>
## Gain access to the bucket

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To gain access to the bucket, you must have <code>tos: GetBucketACL</code> permission, or have READ_ACP bucket ACL permission, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


The following code is used to gain access to `bucket-test`.

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
    # Get bucket permissions
    out = client.get_bucket_acl(bucket_name)
    print('owner_id={}'.format(out.owner.id))
    for grant in out.grants:
        print('permission={}'.format(grant.permission.value))
        print('id={}'.format(grant.grantee.id))
        print('type={}'.format(grant.grantee.type))
        print('canned={}'.format(grant.grantee.canned))
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

To manage the permissions of buckets, see [Bucket ACLs](https://docs.byteplus.com/docs/tos/docs-bucket-acls).
