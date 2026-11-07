---
title: "Retrieving Bucket Metadata (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-metadata-java-sdk"
---

A bucket (Bucket) is the globally unique namespace in TOS, functioning as a data container used to store object (Object) data. This article describes how to use the TOS Java SDK `headBucket` interface to obtain bucket metadata, including the bucket's region and storage class, as well as to determine whether the bucket exists.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Before you can obtain bucket metadata, you must have the `tos:HeadBucket` permission. For detailed instructions, please refer to the [Permission Configuration Overview](https://docs.byteplus.com/docs/6349/102121).

* If the bucket does not exist, this interface will return a 404 error code. This interface is also commonly used to verify the existence of a bucket.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code demonstrates how to retrieve bucket metadata and determine whether a bucket exists.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.HeadBucketV2Input;
import com.volcengine.tos.model.bucket.HeadBucketV2Output;

public class HeadBucketExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            HeadBucketV2Input input = new HeadBucketV2Input().setBucket(bucketName);
            HeadBucketV2Output output = tos.headBucket(input);
            System.out.println("bucket's region is " + output.getRegion());
            System.out.println("bucket's storage class is " + output.getStorageClass());
        } catch (TosClientException e) {
            System.out.println("headBucket failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("headBucket failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("headBucket failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For documentation on the API to obtain bucket metadata, see [HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket).
