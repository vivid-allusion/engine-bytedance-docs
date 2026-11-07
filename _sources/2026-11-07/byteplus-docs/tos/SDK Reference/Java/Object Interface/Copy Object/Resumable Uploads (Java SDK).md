---
title: "Resumable Uploads (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resumption-java-sdk1"
---

Resumable copy is suitable for scenarios where large objects are copied within a single bucket or between two buckets in the same region using the TOS Java SDK. The TOS Java SDK provides resumable download functionality, utilizing a local checkpoint mechanism to record segments that have been successfully copied. In the event of network exceptions or machine failures that interrupt segment transfers, this interface can be invoked again to resume the download process.

Breakpoint resume copy divides the object to be copied into multiple segments and supports concurrent copying. Once all segments have been copied, they are merged into a complete file. You can configure the segment size for resumable copy, the number of threads used for copying segments, event callback functions, etc. It is also possible to cancel the task during the execution of a resumable copy operation.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* File copying does not support cross\-region inter\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".5pat54K557ut5Lyg5ou36LSd"></span>
## **Resumable Copy**

The following code performs resumable copy of the `srcBucketName` bucket's `srcObjectKey` object to the `dstBucketName` bucket, sets the object name to `dstObjectKey`, and supports resuming the download after failure. If a network timeout error occurs during the copy process, resume the interrupted download by invoking ResumableCopyObject with the same parameters.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.ResumableCopyObjectInput;
import com.volcengine.tos.model.object.ResumableCopyObjectOutput;

public class ResumableCopyObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        String sourceBucketName = "source-bucket";
        String sourceObjectKey = "src_example_dir/src_example_object.txt";
        int taskNum = 5;
        long partSize = 10 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            ResumableCopyObjectInput input = new ResumableCopyObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setSrcBucket(sourceBucketName).setSrcKey(sourceObjectKey).setTaskNum(taskNum).setPartSize(partSize)
                    .setEnableCheckpoint(enableCheckpoint).setCheckpointFile(checkpointFilePath);
            ResumableCopyObjectOutput output = tos.resumableCopyObject(input);
            System.out.println("resumableCopyObject succeed, object's etag is " + output.getEtag());
            System.out.println("resumableCopyObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("resumableCopyObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("resumableCopyObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("resumableCopyObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5aSE55CG5LqL5Lu25Zue6LCD"></span>
## **Handling Event Callbacks**

The following code is used to customize the callback function for resumable copy operations.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.event.CopyEventType;
import com.volcengine.tos.model.object.CopyEvent;
import com.volcengine.tos.model.object.CopyEventListener;
import com.volcengine.tos.model.object.ResumableCopyObjectInput;
import com.volcengine.tos.model.object.ResumableCopyObjectOutput;

public class ResumableCopyObjectWithEventListenerExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        String sourceBucketName = "source-bucket";
        String sourceObjectKey = "src_example_dir/src_example_object.txt";
        int taskNum = 5;
        long partSize = 10 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            CopyEventListener listener = new CopyEventListener() {
                @Override
                public void eventChange(CopyEvent copyEvent) {
                    if (copyEvent.getType() == CopyEventType.CopyEventCreateMultipartUploadSucceed) {
                        System.out.println("event change, createMultipartUpload succeed");
                    }
                    if (copyEvent.getType() == CopyEventType.CopyEventCreateMultipartUploadFailed) {
                        System.out.println("event change, createMultipartUpload failed");
                    }
                    if (copyEvent.getType() == CopyEventType.CopyEventUploadPartCopySucceed) {
                        System.out.println("event change, uploadPartCopy succeed");
                    }
                    if (copyEvent.getType() == CopyEventType.CopyEventUploadPartCopyFailed) {
                        System.out.println("event change, uploadPartCopy failed");
                    }
                    if (copyEvent.getType() == CopyEventType.CopyEventUploadPartCopyAborted) {
                        System.out.println("event change, uploadPartCopy aborted");
                    }
                    if (copyEvent.getType() == CopyEventType.CopyEventCompleteMultipartUploadSucceed) {
                        System.out.println("event change, completeMultipartUpload succeed");
                    }
                    if (copyEvent.getType() == CopyEventType.CopyEventCompleteMultipartUploadFailed) {
                        System.out.println("event change, completeMultipartUpload failed");
                    }
                }
            };
            ResumableCopyObjectInput input = new ResumableCopyObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setSrcBucket(sourceBucketName).setSrcKey(sourceObjectKey).setTaskNum(taskNum).setPartSize(partSize)
                    .setEnableCheckpoint(enableCheckpoint).setCheckpointFile(checkpointFilePath).setCopyEventListener(listener);
            ResumableCopyObjectOutput output = tos.resumableCopyObject(input);
            System.out.println("resumableCopyObject succeed, object's etag is " + output.getEtag());
            System.out.println("resumableCopyObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("resumableCopyObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("resumableCopyObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("resumableCopyObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
## **Cancellation Mechanism**

The following code is used to pause or cancel resumable copy tasks.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.event.CopyEventType;
import com.volcengine.tos.model.object.CopyEvent;
import com.volcengine.tos.model.object.CopyEventListener;
import com.volcengine.tos.model.object.ResumableCopyObjectInput;
import com.volcengine.tos.model.object.ResumableCopyObjectOutput;

public class ResumableCopyObjectWithCancelExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        String sourceBucketName = "source-bucket";
        String sourceObjectKey = "src_example_dir/src_example_object.txt";
        int taskNum = 5;
        long partSize = 10 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            ResumableCopyObjectInput input = new ResumableCopyObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setSrcBucket(sourceBucketName).setSrcKey(sourceObjectKey).setTaskNum(taskNum).setPartSize(partSize)
                    .setEnableCheckpoint(enableCheckpoint).setCheckpointFile(checkpointFilePath);
            boolean isAbort = true;
            CopyEventListener listener = new CopyEventListener() {
                @Override
                public void eventChange(CopyEvent uploadEvent) {
                    if (uploadEvent.getType() == CopyEventType.CopyEventUploadPartCopyFailed) {
                        System.out.println("event change, uploadPartCopy failed");
                        if (input.getCancelHook() != null) {
                            input.getCancelHook().cancel(isAbort);
                        }
                    }
                }
            };
            input.setCancelHook(true).setCopyEventListener(listener);
            ResumableCopyObjectOutput output = tos.resumableCopyObject(input);
            System.out.println("resumableCopyObject succeed, object's etag is " + output.getEtag());
            System.out.println("resumableCopyObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("resumableCopyObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("resumableCopyObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("resumableCopyObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```
