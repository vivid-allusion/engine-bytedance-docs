---
title: "Creating a Bucket (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-bucket-java-sdk"
---

A bucket (Bucket) in TOS serves as a globally unique namespace, functioning as a data container used to store object (Object) data. This document describes how to create a new bucket using the `createBucket` interface of the TOS Java SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Category


* A bucket name should conform to the following conventions:

   * Can only contain lowercase letters (a\-z), numbers, and hyphens (\-).

   * Must start and end with a number or letter.

   * Length must be between 3 and 63 characters.

* When accessing TOS through other Volcengine products located in the same region as TOS, it is recommended to use the internal network Endpoint. For more information about regions and Endpoints, see [Regions and Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a storage bucket, you must ensure that your account has the `tos:CreateBucket` permission. You can grant the corresponding permissions through IAM policies. For detailed steps, see [ IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.bucket.CreateBucketV2Input;
import com.volcengine.tos.model.bucket.CreateBucketV2Output;

public class CreateBucketFullExample {
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


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For API documentation on bucket creation, refer to [CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket).
