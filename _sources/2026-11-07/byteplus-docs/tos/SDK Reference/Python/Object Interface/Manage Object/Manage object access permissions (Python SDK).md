---
title: "Manage object access permissions (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-access-to-objects-python-sdk"
---

This article explains how to get and set object access permissions. Object access permissions take precedence over bucket permissions. If an object does not have access permissions set, bucket permissions apply.

<span id=".6K6-572u5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## **Set object read and write permissions**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To set object read and write permissions, you must have <code>tos:PutObjectACL</code> permission or WRITE_ACP object ACL permission. For details, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".5a-56LGhLWFjbC3or7TmmI4="></span>
### Object ACL description

Object ACL permissions include the following types.


|**Access permission** |**Description** |**Access permission value** |
|---|---|---|
|READ |Allow the grantee to read object data and its metadata |tos.PermissionType.Permission_Read |
|READ_ACP |Allow grantees to read object ACL |tos.PermissionType.Permission_Read_Acp |
|WRITE_ACP |Allow the grantee to write ACLs for applicable objects |tos.PermissionType.Permission_Write_Acp |
|FULL_CONTROL |Allow the grantee READ, READ_ACP, and WRITE_ACP permissions on the object |tos.PermissionType.Permission_Full_Control |


You can specify detailed ACL permissions in the request body or set them in the request header.

<span id=".6K-35rGC5L2T5Lit5aGr5YaZ6K-m57uGLWFjbC3mnYPpmZDkv6Hmga8="></span>
### **Specify detailed ACL permissions in the request body**

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
bucket_name = 'bucket-test'
# Object key, for example, if the file is example_object.txt under example_dir, fill in as example_dir/example_object.txt
object_key = 'object-key'
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

    client.put_object_acl(bucket_name, object_key, grants=[grant_1, grant_2],
                          owner=Owner("object owner id", 'object owner name'))
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

There are six categories of read and write permissions for objects set through the `x-tos-acl` request header.


|**Access permission** |**Description** |Access permission value |
|---|---|---|
|Private |Private. The object owner has all permissions; other users have no permission to operate the object. |tos.ACLType.ACL_Private |
|Public Read |Public Read. The object owner has all permissions; other users have read\-only permission for the object. |tos.ACLType.ACL_Public_Read |
|Authenticated user read |The object owner has all permissions; authenticated users have read permission for the object. |tos.ACLType.ACL_Authenticated_Read |
|Bucket owner read |The object owner has all permissions; the bucket owner has read permission for this object. |tos.ACLType.ACL_Bucket_Owner_Read |
|The bucket owner has all permissions |Bucket owners and object owners have all permissions on the object |tos.ACLType.ACL_Bucket_Owner_Full_Control |


The following code sets the object's read and write permissions using `x-tos-acl`.

```python
import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
# Object key, for example, if the file is example_object.txt under example_dir, fill in as example_dir/example_object.txt
object_key = 'object-key'
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Set object ACL to private
    client.put_object_acl(bucket_name, object_key, acl=tos.ACLType.ACL_Private)
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


The following code sets the object's read and write permissions via the `x-tos-grant-*` request header.

```python
import os
import tos


# Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
# Object key, for example, if the file is example_object.txt under example_dir, fill in as example_dir/example_object.txt
object_key = 'object-key'
try:
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Grant user ID 1000000001 FULL_CONTROL permission, and grant READ permission on the bucket to all users.
    client.put_object_acl(bucket_name, object_key, grant_full_control='id="1000000001"', grant_read='canned="AllUsers"')
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
### **Related documentation**

For API documentation on setting object read and write permissions, see [PutObjectAcl](https://docs.byteplus.com/docs/tos/reference-putobjectacl).

<span id=".6I635Y-W5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## Get object read and write permissions

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get an object's access permissions, you must have the <code>tos:GetObjectACL</code> permission or the object's ACL READ_ACP permission. For detailed operations, see the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">permission configuration guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### Example code

The following code retrieves the access permissions for object `object-test` in `bucket-test`.

```python
import os
import tos


# # Retrieve AKSK information from environment variables.
ak = os.getenv('TOS_ACCESS_KEY')
sk = os.getenv('TOS_SECRET_KEY')
endpoint = "your endpoint"
region = "your region"
bucket_name = 'bucket-test'
# Object key, for example, if the file is example_object.txt under example_dir, fill in as example_dir/example_object.txt
object_key = 'object-key'
try:
    # Create a TosClientV2 object to perform operations on buckets and objects
    client = tos.TosClientV2(ak, sk, endpoint, region)
    # Obtain permissions on the object
    out = client.get_object_acl(bucket_name, object_key)
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
### **Related documentation**

For API documentation on obtaining read and write permissions for objects, see [GetObjectAcl](https://docs.byteplus.com/docs/tos/reference-getobjectacl).
