---
title: "Creating Hierarchical Namespaces (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-a-hierarchical-namespace-java-sdk"
---

The Hierarchical NameSpace (HNS), abbreviated as the hierarchical bucket, is a new bucket type introduced by object storage TOS. It is based on hierarchical metadata management. Besides its hierarchical namespace features, a HNS bucket can scale as much as a FNS bucket. It also delivers seamless interoperability between object and file semantics. This allows **data to be accessed through multiple protocols**, so you can process data more efficiently.

Compared to the original Flat NameSpace (FNS, also known as flat bucket), FNS provides robust support for directory\-level mv and rename operations. It also optimizes common read operations such as List and directory Head, thereby enhancing data processing efficiency and performance. FNS can effectively meet the application requirements in big data, data lake, and AI domains.

This document describes how to create a hierarchical namespace using the TOS Java SDK `createBucket` interface.

<span id="bcd91b7f"></span>
## Category


* A bucket name should conform to the following conventions:

   * Can only contain lowercase letters (a\-z), numbers, and hyphens (\-).

   * Must start and end with a number or letter.

   * Length must be between 3 and 63 characters.

* When accessing TOS from other BytePlus products that are in the same region as TOS, it is recommended to use the internal network Endpoint. For more information about regions and Endpoints, see [Regions and Access Domains](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a storage bucket, you must ensure that your account has the `tos:CreateBucket` permission. You can grant the appropriate permissions through IAM policies. For detailed steps, please refer to the [ IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6).

* This feature is currently in invitation\-only testing and is available in North China 2 (Beijing) and East China 2 (Shanghai) regions. If you wish to participate in the trial, please contact your account manager.

   After creating a hierarchical namespace, it cannot be used immediately. You must wait 12 hours before normal operation; otherwise, uploading data will result in errors such as 405. If you wish to access this feature as soon as possible, you may submit a support ticket to contact technical support.


Sample Code

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.bucket.CreateBucketV2Input;
import com.volcengine.tos.model.bucket.CreateBucketV2Output;

public class CreateDirectoryBucketExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        ACLType aclType = ACLType.ACL_PRIVATE;
        StorageClassType storageClassType = StorageClassType.STORAGE_CLASS_STANDARD;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            CreateBucketV2Input input = new CreateBucketV2Input().setBucket(bucketName)
                    .setAcl(aclType).setStorageClass(storageClassType);
            CreateBucketV2Output output = tos.createBucket(input);
            System.out.println("bucket created: " + output.getLocation());
        } catch (TosClientException e) {
            System.out.println("createBucket failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("createBucket failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("createBucket failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="09c99c37"></span>
## Related documentation

For API documentation on bucket creation, refer to [CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket).
