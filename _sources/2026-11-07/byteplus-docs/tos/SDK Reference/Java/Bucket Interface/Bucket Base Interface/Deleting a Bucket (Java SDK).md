---
title: "Deleting a Bucket (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-java-sdk"
---

A Bucket is the globally unique namespace in TOS, functioning as a data container used to store Object data. When you no longer need to retain a bucket (Bucket), you may delete it to avoid incurring additional charges. This document describes how to delete a specified bucket using the TOS Java SDK `deleteBucket` interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Once a bucket is deleted, it cannot be recovered. Please proceed with caution.

* Before deleting a bucket, you must have the `tos:DeleteBucket` permission. For detailed instructions, please refer to [Permission Configuration Overview](https://docs.byteplus.com/docs/6349/102121).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before deleting a bucket, ensure that all data within the bucket has been removed.


* If versioning is enabled for the bucket, please ensure that all current and previous version objects within the bucket have been deleted. For detailed instructions, see [Delete Object](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#%E5%BD%BB%E5%BA%95%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6).

* If there are unmerged shards in the bucket, ensure that all shard data is deleted. For detailed instructions, see [Delete Shard](https://docs.byteplus.com/docs/tos/docs-managing-parts#%E5%88%A0%E9%99%A4%E5%88%86%E7%89%87).

* If there are a large number of objects in the bucket, you can configure lifecycle rules to enable batch deletion of objects. For specific steps, see [Configuring Lifecycle Rules](https://docs.byteplus.com/docs/6349/75028).


<span id=".5Luj56CB56S65L6L"></span>
## **Code Example**

The following code demonstrates how to delete an empty bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketInput;
import com.volcengine.tos.model.bucket.DeleteBucketOutput;

public class DeleteBucketExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketInput input = new DeleteBucketInput().setBucket(bucketName);
            DeleteBucketOutput output = tos.deleteBucket(input);
            System.out.println("deleteBucket succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucket failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucket failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucket failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For API documentation on deleting a bucket, see [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
