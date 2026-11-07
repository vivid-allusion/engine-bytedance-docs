---
title: "Manage Bucket Policies (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-policy-java-sdk"
---

A bucket (Bucket) in TOS serves as a globally unique namespace, functioning as a data container for storing object (Object) data. TOS access control for bucket resources includes bucket authorization policies (Bucket Policy) and bucket access control lists (Bucket ACL). This article explains how to manage bucket authorization policies (Policy) using the TOS Java SDK. For information on bucket access control management, please refer to the read/write permission configuration.

<span id=".6K6-572u5qG2562W55Wl"></span>
## **Set Bucket Policy**

You can set the authorization policy for a specified bucket through the `putBucketPolicy` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To set a bucket policy, your account must have the <code>tos:PutBucketPolicy</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/6349/102121">Permission Configuration Overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">Users with the <code>tos:PutBucketPolicy</code> permission can modify bucket policies without restriction and can use this permission to obtain other permissions. It is recommended that you configure this permission with caution.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to configure a bucket policy.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.PutBucketPolicyInput;
import com.volcengine.tos.model.bucket.PutBucketPolicyOutput;

public class PutBucketPolicyExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            String policy = "{\"Statement\":[{\"Sid\":\"test\",\"Effect\":\"Allow\",\"Principal\":\"*\",\"Action\":[\"tos:Get*\",\"tos:List*\",\"tos:HeadBucket\"],\"Resource\":\"trn:tos:::bucketName\"}]}";
            PutBucketPolicyInput input = new PutBucketPolicyInput().setBucket(bucketName).setPolicy(policy);
            PutBucketPolicyOutput output = tos.putBucketPolicy(input);
            System.out.println("putBucketPolicy succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketPolicy failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketPolicy failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketPolicy failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W5qG2562W55Wl"></span>
## **Retrieve Bucket Policy**

You can obtain the current bucket policy configuration for a specified bucket through the `getBucketPolicy` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the bucket policy, your account must have the <code>tos:GetBucketPolicy</code> permission. For details on how to configure permissions, please refer to <a href="https://docs.byteplus.com/docs/6349/102121">Permission Configuration Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to retrieve the bucket policy.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketPolicyInput;
import com.volcengine.tos.model.bucket.GetBucketPolicyOutput;

public class GetBucketPolicyExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketPolicyInput input = new GetBucketPolicyInput().setBucket(bucketName);
            GetBucketPolicyOutput output = tos.getBucketPolicy(input);
            System.out.println("getBucketPolicy succeed, policy is " + output.getPolicy());
        } catch (TosClientException e) {
            System.out.println("getBucketPolicy failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketPolicy failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketPolicy failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk5qG2562W55Wl"></span>
## **Bucket Deletion Policy**

You can delete the current bucket policy configured for a specified bucket by using the `deleteBucketPolicy` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete a policy, your account must have the <code>tos:DeleteBucketPolicy</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/6349/102121">Permission Configuration Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to delete a bucket policy.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketPolicyInput;
import com.volcengine.tos.model.bucket.DeleteBucketPolicyOutput;

public class DeleteBucketPolicyExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketPolicyInput input = new DeleteBucketPolicyInput().setBucket(bucketName);
            DeleteBucketPolicyOutput output = tos.deleteBucketPolicy(input);
            System.out.println("deleteBucketPolicy succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucketPolicy failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucketPolicy failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucketPolicy failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For more information about bucket policies, see [Bucket Authorization Policy Management](https://docs.byteplus.com/docs/tos/docs-bucket-authorization-policy-management).
