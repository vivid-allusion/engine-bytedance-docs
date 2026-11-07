---
title: "Obtaining Bucket Region (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-the-bucket-region-java-sdk"
---

A Bucket is the globally unique namespace in TOS, equivalent to a data container used for storing object (Object) data. This article explains how to obtain the region information of a bucket using the TOS Java SDK `getBucketLocation` interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**

Only the bucket owner (Owner) can view the region (Region) where the bucket is located.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to obtain the region (Region) information of a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketLocationInput;
import com.volcengine.tos.model.bucket.GetBucketLocationOutput;

public class GetBucketLocationExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketLocationInput input = new GetBucketLocationInput().setBucket(bucketName);
            GetBucketLocationOutput output = tos.getBucketLocation(input);
            System.out.println("bucket's region is " + output.getRegion());
            System.out.println("bucket's extranet endpoint is " + output.getExtranetEndpoint());
            System.out.println("bucket's intranet endpoint is " + output.getIntranetEndpoint());
        } catch (TosClientException e) {
            System.out.println("getBucketLocation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketLocation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketLocation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```
