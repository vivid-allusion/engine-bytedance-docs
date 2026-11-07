---
title: "Deletion Scenarios (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-scenes-java-sdk"
---

This article introduces code examples for common object deletion scenarios.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To delete an object, your account must have the `tos:DeleteObject` permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete multi\-version objects, your account must have the `tos:DeleteObjectVersion` permission. For specific instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Please exercise caution when performing delete operations, as files cannot be restored once deleted.


<span id=".5Yig6Zmk5Y2V5Liq5a-56LGh"></span>
## **Delete an object**

For an example of how to delete a single regular object, see [Delete an object](https://docs.byteplus.com/docs/tos/Delete-object-java-sdk#.5Yig6Zmk5oyH5a6a5a-56LGh).

<span id=".5Yig6Zmk5oyH5a6a54mI5pys5a-56LGh"></span>
## **Delete an object version**

For an example of how to delete a single multi\-version object, refer to [Delete an object version](https://docs.byteplus.com/docs/tos/Delete-object-java-sdk#.5Yig6Zmk5oyH5a6a54mI5pys5a-56LGh).

<span id=".5Yig6Zmk5oyH5a6a55uu5b2V5LiL55qE5omA5pyJ5a-56LGh"></span>
## **Delete all objects in the specified directory**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This operation will delete all objects in the specified directory. Please use with caution.</div>


For an example of how to delete all objects within a specified directory, refer to [Delete objects with a specified prefix in a bucket](https://docs.byteplus.com/docs/tos/Delete-object-java-sdk#.5Yig6Zmk5qG25Lit5oyH5a6a5YmN57yA55qE5a-56LGh).

<span id=".5Yig6Zmk5oyH5a6a55uu5b2V5LiL55qE5omA5pyJ5aSa54mI5pys5a-56LGh"></span>
## **Delete all multi\-version objects in the specified directory**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This operation will delete all multi\-version objects in the specified directory. Please proceed with caution.</div>


For an example of how to delete all versions of all objects with a specified prefix, refer to [Delete object versions—Delete all objects with a specified prefix](https://docs.byteplus.com/docs/tos/Delete-object-java-sdk#.5Yig6Zmk5oyH5a6a54mI5pys5a-56LGh).

<span id=".5riF56m65qG25YaF5oyH5a6a5YmN57yA5LiL5omA5pyJ5a-56LGh55qE5pyq5ZCI5bm255qE5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
## **Clear all incomplete multipart uploads for objects under the specified prefix in the bucket**

The following code demonstrates how to delete all incomplete multipart uploads for objects under a specified prefix in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class AbortMultipartUploadWithPrefixExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String prefix = "example_dir/";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            boolean isTruncated = true;
            String keyMarker = null;
            String uploadIdMarker = null;
            while (isTruncated) {
                ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input().setBucket(bucketName)
                        .setKeyMarker(keyMarker).setUploadIDMarker(uploadIdMarker).setPrefix(prefix);
                ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
                System.out.printf("listMultipartUploads succeed, is truncated? %b, next uploadIDMarker is %s, " +
                        "next keyMarker is %s.\n", output.isTruncated(), output.getNextUploadIdMarker(), output.getNextKeyMarker());
                if (output.getUploads() != null) {
                    for (int i = 0; i < output.getUploads().size(); i++) {
                        ListedUpload upload = output.getUploads().get(i);
                        AbortMultipartUploadInput abort = new AbortMultipartUploadInput().setBucket(bucketName)
                                .setKey(upload.getKey()).setUploadID(upload.getUploadID());
                        tos.abortMultipartUpload(abort);
                        System.out.println("Aborted upload is " + upload);
                    }
                }
                isTruncated = output.isTruncated();
                keyMarker = output.getNextKeyMarker();
                uploadIdMarker = output.getNextUploadIdMarker();
            }
        } catch (TosClientException e) {
            System.out.println("abortMultipartUpload failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("abortMultipartUpload failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("abortMultipartUpload failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```
