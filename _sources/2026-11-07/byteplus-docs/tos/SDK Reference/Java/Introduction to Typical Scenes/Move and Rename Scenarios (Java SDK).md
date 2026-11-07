---
title: "Move and Rename Scenarios (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Move-and-rename-scenes-java-sdk"
---

If you need to rename a file within a bucket, you can use the Java SDK's `copyObject` interface to copy the source object to the target object, and then use the `deleteObject` interface to delete the source object.

<span id=".6YeN5ZG95ZCN5Y2V5Liq5a-56LGh"></span>
## **Rename a single object**

The following code demonstrates how to rename the object `src-object` in the bucket `bucket-example` to `dest-object`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.CopyObjectV2Input;
import com.volcengine.tos.model.object.CopyObjectV2Output;
import com.volcengine.tos.model.object.DeleteObjectInput;

public class RenameObjectExample {
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

            tos.deleteObject(new DeleteObjectInput().setBucket(srcBucketName).setKey(srcObjectKey));
        } catch (TosClientException e) {
            System.out.println("rename Object failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("rename Object failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("rename Object failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6YeN5ZG95ZCN55uu5b2V"></span>
## **Rename Directory**

The following code demonstrates how to rename the directory `example_dir1/` to `example_dir2/` in the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class RenameDirExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String srcBucketName = "src-bucket-example";
        String srcDir = "src_example_dir/";
        String bucketName = "bucket-example";
        String dstDir = "dst_example_dir/";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            boolean isTruncated = true;
            String continuationToken = null;
            while (isTruncated) {
                ListObjectsType2Input input = new ListObjectsType2Input().setBucket(bucketName)
                        .setContinuationToken(continuationToken).setPrefix(srcDir);
                ListObjectsType2Output output = tos.listObjectsType2(input);
                System.out.printf("listObjectsType2 succeed, is truncated? %b, next continuation token is %s.\n",
                        output.isTruncated(), output.getNextContinuationToken());
                if (output.getContents() != null) {
                    for (int i = 0; i < output.getContents().size(); i++) {
                        ListedObjectV2 object = output.getContents().get(i);
                        String dstKey = dstDir + object.getKey().substring(srcDir.length());
                        CopyObjectV2Input copy = new CopyObjectV2Input().setBucket(bucketName).setKey(dstKey)
                                .setSrcBucket(srcBucketName).setSrcKey(object.getKey());
                        CopyObjectV2Output copyOutput = tos.copyObject(copy);
                        System.out.println("copyObject succeed, object's etag is " + copyOutput.getEtag());
                        System.out.println("copyObject succeed, object's crc64 is " + copyOutput.getHashCrc64ecma());

                        tos.deleteObject(new DeleteObjectInput().setBucket(srcBucketName).setKey(object.getKey()));
                        System.out.println("rename object in " + srcDir + ", from " + object.getKey() + " to " + dstKey);
                    }
                }
                isTruncated = output.isTruncated();
                continuationToken = output.getNextContinuationToken();
            }

        } catch (TosClientException e) {
            System.out.println("rename Object failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("rename Object failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("rename Object failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**


* For documentation on the Copy Object API, see [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).

* For documentation on the Delete Object API, see [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).
