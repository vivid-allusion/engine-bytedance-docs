---
title: "Multipart Copy (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-copy-java-sdk"
---

When an object exceeds 5GiB in size, you can use the `uploadPartCopy` interface of the TOS Java SDK to perform multipart copy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Copying files between buckets across regions is not supported.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to multipart copy the `srcObjectKey` object in the `srcBucketName` bucket to the `bucketName` bucket, and set the object name to `objectKey`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

import java.util.ArrayList;
import java.util.List;

public class UploadPartCopyExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String srcBucketName = "src-bucket-example";
        String srcObjectKey = "src_example_dir/example_object.txt";
        String bucketName = "bucket-example";
        String objectKey = "dst_example_dir/example_object.txt";

        long partSize = 10 * 1024 * 1024;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            HeadObjectV2Output headInfo = tos.headObject(new HeadObjectV2Input().setBucket(srcBucketName).setKey(srcObjectKey));
            long contentLength = headInfo.getContentLength();

            CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);
            CreateMultipartUploadOutput created = tos.createMultipartUpload(create);
            String uploadID = created.getUploadID();

            List<UploadedPartV2> partList = new ArrayList<>();
            long rangeStart = 0, rangeEnd = 0;
            int partNumber = 1;
            while (rangeStart < contentLength) {
                rangeEnd = Math.min(rangeStart + partSize - 1, contentLength - 1);
                UploadPartCopyV2Input input = new UploadPartCopyV2Input().setBucket(bucketName).setKey(objectKey)
                        .setUploadID(uploadID).setSourceBucket(srcBucketName).setSourceKey(srcObjectKey)
                        .setPartNumber(partNumber).setCopySourceRange(rangeStart, rangeEnd);
                UploadPartCopyV2Output output = tos.uploadPartCopy(input);
                System.out.println("uploadPartCopy succeed, part's etag is " + output.getEtag());
                System.out.println("uploadPartCopy succeed, part's partNumber is " + output.getPartNumber());
                partList.add(new UploadedPartV2().setEtag(output.getEtag()).setPartNumber(output.getPartNumber()));
                rangeStart = rangeEnd + 1;
                partNumber++;
            }

            CompleteMultipartUploadV2Input complete = new CompleteMultipartUploadV2Input().setBucket(bucketName)
                    .setKey(objectKey).setUploadID(uploadID).setUploadedParts(partList);
            CompleteMultipartUploadV2Output output = tos.completeMultipartUpload(complete);
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


* For the API documentation on creating multipart upload tasks, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on part copy, see [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy).

* For API documentation on merging parts, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).
