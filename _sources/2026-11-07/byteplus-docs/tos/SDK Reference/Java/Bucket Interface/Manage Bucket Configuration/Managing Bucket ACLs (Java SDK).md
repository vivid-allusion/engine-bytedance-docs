---
title: "Managing Bucket ACLs (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-acl-java-sdk"
---

A bucket (Bucket) in TOS is a globally unique namespace that serves as a data container for storing object (Object) data. TOS access control for bucket resources includes bucket authorization policies (Bucket Policy) and bucket read/write permission controls (Bucket ACL). This article explains how to manage bucket read and write permissions (ACL) using the TOS Java SDK. For information on bucket authorization policy management, please refer to the authorization policy configuration section.

<span id=".6K6-572u5qG255qE6K6_6Zeu5p2D6ZmQ"></span>
## **Configuring Bucket Access Permissions**

You can set the read and write permissions for a specified bucket through the `putBucketACL` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To set read and write permissions for a bucket, your account must have the <code>tos:PutBucketACL</code> permission or the <code>WRITE_ACP</code> bucket ACL permission. For detailed instructions, see <a href="https://docs.byteplus.com/docs/6349/102121">Permission Configuration Overview</a>.</div>


<span id=".5qG2LWFjbC3or7TmmI4="></span>
### Bucket ACL Description

Bucket ACL permissions include the following five categories.


|**Access permission** |**Description** |**Access Permission Value** |
|---|---|---|
|READ |Allow authorized users to list objects in the storage bucket. |PermissionType.PERMISSION_READ |
|WRITE |Authorized users are permitted to create, overwrite, and delete any object within the bucket. |PermissionType.PERMISSION_WRITE |
|READ_ACP |Allow authorized entities to read the storage bucket ACL. |PermissionType.PERMISSION_READ_ACP |
|WRITE_ACP |Allow authorized users to write to the bucket ACL. |PermissionType.PERMISSION_WRITE_ACP |
|FULL_CONTROL |Authorized users are permitted READ, WRITE, READ_ACP, and WRITE_ACP permissions on the storage bucket. |PermissionType.PERMISSION_FULL_CONTROL |


Bucket access permissions can be configured either by specifying detailed ACL information in the request body or by setting them in the request header.

<span id=".6K-35rGC5L2T5Lit5aGr5YaZ6K-m57uGLWFjbC3mnYPpmZDkv6Hmga8="></span>
### **Provide detailed information in the request body.**  **ACL** **Permission Information**

The following code demonstrates how to set bucket permission information in the request body.

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
import com.volcengine.tos.model.bucket.PutBucketACLInput;
import com.volcengine.tos.model.bucket.PutBucketACLOutput;

import java.util.ArrayList;
import java.util.List;

public class PutBucketACLWithGrantsExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

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
            PutBucketACLInput input = new PutBucketACLInput().setBucket(bucketName).setGrants(grantList)
                    .setOwner(new Owner().setId(ownerId).setDisplayName(ownerDisplayName));
            PutBucketACLOutput output = tos.putBucketACL(input);
            System.out.println("putBucketACL succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketACL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketACL failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketACL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6K-35rGC5aS05Lit6K6-572u6K6_6Zeu5p2D6ZmQ"></span>
### **Configuring access permissions in the request header**

There are four types of bucket read/write permissions that can be configured via the `x-tos-acl` request header.


|**Access permission** |**Description** |**Access Permission Value** |
|---|---|---|
|Private |Private. The bucket owner has FULL_CONTROL permissions, while other users are not authorized to operate on this object. |ACLType.ACL_PRIVATE |
|Public Read |Public reading. The owner of the bucket has FULL_CONTROL permissions, while other users have only READ permissions for that bucket. |ACLType.ACL_PUBLIC_READ |
|Public Read and Write |Public read/write. All users have the FULL_CONTROL permission. |ACLType.ACL_PUBLIC_READ_WRITE |
|Read Access for Certified Users |The bucket owner has FULL_CONTROL permission, while authenticated users have READ permission on the bucket. |ACLType.ACL_AUTHENTICATED_READ |


The following code demonstrates how to set bucket read/write permissions using `x-tos-acl`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.model.bucket.PutBucketACLInput;
import com.volcengine.tos.model.bucket.PutBucketACLOutput;

public class PutBucketACLWithAclHeaderExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            ACLType aclType = ACLType.ACL_PRIVATE;
            PutBucketACLInput input = new PutBucketACLInput().setBucket(bucketName).setAcl(aclType);
            PutBucketACLOutput output = tos.putBucketACL(input);
            System.out.println("putBucketACL succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketACL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketACL failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketACL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


The following code demonstrates how to set bucket read and write permissions via the `x-tos-grant-*` request header.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.PutBucketACLInput;
import com.volcengine.tos.model.bucket.PutBucketACLOutput;

public class PutBucketACLWithGrantHeaderExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            String grantFullControlRule = "id=\"1000000001\"";
            String grantReadRule = "canned=\"AllUsers\"";
            PutBucketACLInput input = new PutBucketACLInput().setBucket(bucketName)
                    .setGrantFullControl(grantFullControlRule).setGrantRead(grantReadRule);
            PutBucketACLOutput output = tos.putBucketACL(input);
            System.out.println("putBucketACL succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketACL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketACL failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketACL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W5qG255qE6K6_6Zeu5p2D6ZmQ"></span>
## **Obtaining Access Permissions for Buckets**

You can obtain the current read and write permissions configured for a specified bucket through the TOS Java SDK's `getBucketACL` interface.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain access to a bucket, your account must have the <code>tos:GetBucketACL</code> permission or the bucket ACL permission <code>READ_ACP</code>. For detailed procedures, refer to <a href="https://docs.byteplus.com/docs/6349/102121">Permission Configuration Overview</a>.</div>


<SOURCE_TEXT\>The following code demonstrates how to obtain bucket access permissions.</SOURCE_TEXT\>

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.acl.GrantV2;
import com.volcengine.tos.model.bucket.GetBucketACLInput;
import com.volcengine.tos.model.bucket.GetBucketACLOutput;

public class GetBucketACLExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketACLInput input = new GetBucketACLInput().setBucket(bucketName);
            GetBucketACLOutput output = tos.getBucketACL(input);
            System.out.println("getBucketACL succeed");
            if (output.getOwner() != null) {
                System.out.println("owner id is " + output.getOwner().getId());
                System.out.println("owner display name is " + output.getOwner().getDisplayName());
            }
            if (output.getGrants() != null) {
                System.out.println("this bucket has " + output.getGrants().size() + " grants");
                for (int i = 0; i < output.getGrants().size(); i++){
                    GrantV2 grant = output.getGrants().get(i);
                    if (grant.getGrantee() != null) {
                        System.out.printf("bucket acl grantee, id is %s, displayName is %s, type is %s, uri is %s.\n",
                                grant.getGrantee().getId(), grant.getGrantee().getDisplayName(),
                                grant.getGrantee().getType(), grant.getGrantee().getCanned());
                    }
                    System.out.println("bucket acl grant permission is " + grant.getPermission() + ".");
                }
            }
        } catch (TosClientException e) {
            System.out.println("getBucketACL failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketACL failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketACL failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

To manage bucket permissions, see [Bucket ACLs](https://docs.byteplus.com/docs/tos/docs-bucket-acls).
