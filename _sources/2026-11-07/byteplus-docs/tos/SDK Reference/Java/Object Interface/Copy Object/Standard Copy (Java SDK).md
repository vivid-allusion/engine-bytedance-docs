---
title: "Standard Copy (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-copy-java-sdk"
---

When the object is smaller than 5 GiB, you can use the `copyObject` interface of the TOS Java SDK to perform a standard copy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* Copying files between buckets across regions is not supported.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can either retain all metadata (the default option) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to copy the `srcObjectKey` object from the `srcBucketName` bucket to the `bucketName` bucket, and set the object name as `objectKey`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.CopyObjectV2Input;
import com.volcengine.tos.model.object.CopyObjectV2Output;

public class CopyObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String srcBucketName = "src-bucket-example";
        String srcObjectKey = "src_example_dir/example_object.txt";
        String bucketName = "bucket-example";
        String objectKey = "dst_example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            CopyObjectV2Input input = new CopyObjectV2Input().setBucket(bucketName).setKey(objectKey)
                    .setSrcBucket(srcBucketName).setSrcKey(srcObjectKey);
            CopyObjectV2Output output = tos.copyObject(input);
            System.out.println("copyObject succeed, object's etag is " + output.getEtag());
            System.out.println("copyObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("copyObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("copyObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("copyObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For API documentation on standard copy operations, see [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
