---
title: "Managing Object Read and Write Permissions (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-read-and-write-permissions-java-sdk"
---

This article describes how to obtain and configure access permissions for objects. Object access permissions take precedence over bucket access permissions. If no access permissions are set for the object, the bucket's access permissions will apply.

<span id=".6K6-572u5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## **Configuring object read and write permissions**

You can set the read and write permissions for a specified object using the `putObjectAcl` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To set read and write permissions for an object, your account must have the <code>tos:PutObjectAcl</code> permission. For specific instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


<span id=".5a-56LGhLWFjbC3or7TmmI4="></span>
### Object ACL overview

Object ACL permissions include the following types.


|**Access permission** |**Description** |**Access permission value** |
|---|---|---|
|READ |Authorized users are permitted to read object data and its metadata. |PermissionType.PERMISSION_READ |
|READ_ACP |Allow authorized users to read the object's ACL. |PermissionType.PERMISSION_READ_ACP |
|WRITE_ACP |Allow authorized entities to write to the object ACL. |PermissionType.PERMISSION_WRITE_ACP |
|FULL_CONTROL |Authorized users are permitted READ, READ_ACP, and WRITE_ACP permissions on the object. |PermissionType.PERMISSION_FULL_CONTROL |


You may refer to the following code to specify detailed Access Control List (ACL) permissions either in the request body or by setting ACL permissions in the request header.

<span id=".6K-35rGC5L2T5Lit5aGr5YaZ6K-m57uGLWFjbC3mnYPpmZDkv6Hmga8="></span>
### **Provide detailed ACL permission information in the request body**

The following code demonstrates how to set object permission information in the request body.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.CannedType;
import com.volcengine.tos.comm.common.GranteeType;
import com.volcengine.tos.comm.common.PermissionType;
import com.volcengine.tos.model.acl.GrantV2;
import com.volcengine.tos.model.acl.GranteeV2;
import com.volcengine.tos.model.acl.Owner;
import com.volcengine.tos.model.object.ObjectAclRulesV2;
import com.volcengine.tos.model.object.PutObjectACLInput;
import com.volcengine.tos.model.object.PutObjectACLOutput;

import java.util.ArrayList;
import java.util.List;

public class PutObjectAclWithGrantsExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            String accountId = "the granted account id";
            String accountDisplayName = "the granted account display name";
            GranteeV2 grantee1 = new GranteeV2().setType(GranteeType.GRANTEE_USER)
                    .setId(accountId).setDisplayName(accountDisplayName);
            GrantV2 grant1 = new GrantV2().setGrantee(grantee1).setPermission(PermissionType.PERMISSION_FULL_CONTROL);

            GranteeV2 grantee2 = new GranteeV2().setType(GranteeType.GRANTEE_GROUP)
                    .setCanned(CannedType.CANNED_ALL_USERS);
            GrantV2 grant2 = new GrantV2().setGrantee(grantee2).setPermission(PermissionType.PERMISSION_READ);

            List<GrantV2> grantList = new ArrayList<>();
            grantList.add(grant1);
            grantList.add(grant2);

            String ownerId = "your owner id";
            String ownerDisplayName = "your owner display name";
            Owner owner = new Owner().setId(ownerId).setDisplayName(ownerDisplayName);
            PutObjectACLInput input = new PutObjectACLInput().setBucket(bucketName).setKey(objectKey)
                    .setObjectAclRules(new ObjectAclRulesV2().setGrants(grantList).setOwner(owner));
            PutObjectACLOutput output = tos.putObjectAcl(input);
            System.out.println("putObjectAcl succeed.");
        } catch (TosClientException e) {
            System.out.println("putObjectAcl failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObjectAcl failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObjectAcl failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6K-35rGC5aS05Lit6K6-572u6K6_6Zeu5p2D6ZmQ"></span>
### **Configure access permissions in the request header**

There are six categories of object read/write permissions that can be configured via the `x-tos-acl` header.


|**Access permission** |**Description** |Access permission value |
|---|---|---|
|Private |Private. The owner of the object possesses full permissions, while other users are not authorized to operate the object. |ACLType.ACL_PRIVATE |
|Public Read |Public reading. The owner of an object possesses all permissions, while other users have only read permission for that object. |ACLType.ACL_PUBLIC_READ |
|Public Read and Write |Public Read/Write All users have read and write permissions for this object. |ACLType.ACL_PUBLIC_READ_WRITE |
|Authenticated User Read Access |The owner of the object possesses all permissions, while authenticated users are granted read permission for the object. |ACLType.ACL_AUTHENTICATED_READ |
|Bucket Owner Read |The owner of the object has full permissions, while the owner of the bucket has read permission for this object. |ACLType.ACL_BUCKET_OWNER_READ |
|Bucket Owner Full Control |Both the bucket owner and the object owner have full operation permissions on the object. |ACLType.ACL_BUCKET_OWNER_FULL_CONTROL |


The following code demonstrates how to set object read and write permissions using `x-tos-acl`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.model.object.PutObjectACLInput;
import com.volcengine.tos.model.object.PutObjectACLOutput;

public class PutObjectAclWithAclHeaderExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            PutObjectACLInput input = new PutObjectACLInput().setAcl(ACLType.ACL_PUBLIC_READ)
                    .setBucket(bucketName).setKey(objectKey);
            PutObjectACLOutput output = tos.putObjectAcl(input);
            System.out.println("putObjectAcl succeed.");
        } catch (TosClientException e) {
            System.out.println("putObjectAcl failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObjectAcl failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObjectAcl failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


The following code demonstrates how to set object read and write permissions using the `x-tos-grant-*` header.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectACLInput;
import com.volcengine.tos.model.object.PutObjectACLOutput;

public class PutObjectAclWithGrantHeaderExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            String grantFullControlRule = "id=\"1000000001\"";
            String grantReadRule = "canned=\"AllUsers\"";
            PutObjectACLInput input = new PutObjectACLInput().setBucket(bucketName).setKey(objectKey)
                    .setGrantFullControl(grantFullControlRule).setGrantRead(grantReadRule);
            PutObjectACLOutput output = tos.putObjectAcl(input);
            System.out.println("putObjectAcl succeed.");
        } catch (TosClientException e) {
            System.out.println("putObjectAcl failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObjectAcl failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObjectAcl failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Related documentation**

For detailed configuration of object read and write permissions, refer to [PutObjectACL](https://docs.byteplus.com/docs/tos/reference-putobjectacl).

<span id=".6I635Y-W5a-56LGh55qE6K6_6Zeu5p2D6ZmQ"></span>
## **Obtaining access permissions for objects**

You can obtain the current read and write permissions configured for a specified object through the TOS Java SDK's `getObjectAcl` interface.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain access permissions for an object, your account must have the <code>tos:GetObjectACL</code> permission. For specific instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


The following code demonstrates how to obtain access permissions for an object.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.acl.GrantV2;
import com.volcengine.tos.model.object.GetObjectACLV2Input;
import com.volcengine.tos.model.object.GetObjectACLV2Output;

public class GetObjectAclExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetObjectACLV2Input input = new GetObjectACLV2Input().setBucket(bucketName).setKey(objectKey);
            GetObjectACLV2Output output = tos.getObjectAcl(input);
            System.out.println("getObjectAcl succeed.");
            System.out.println("object owner is " + output.getOwner());
            if (output.getGrants() != null && output.getGrants().size() > 0) {
                for (GrantV2 grant : output.getGrants()) {
                    System.out.println("object grant is " + grant);
                }
            }
        } catch (TosClientException e) {
            System.out.println("getObjectAcl failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getObjectAcl failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getObjectAcl failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Related documentation**

For detailed information on obtaining object read/write permissions, refer to [GetObjectACL](https://docs.byteplus.com/docs/tos/reference-getobjectacl).
