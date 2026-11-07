---
title: "Resumable Uploads (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resumption-java-sdk"
---

The `uploadFile` interface of the Java SDK supports uploading large local files to TOS using resumable multipart upload. When using this interface, you can configure parameters such as chunk size, the number of concurrent threads for uploading chunks, client\-side upload rate limiting, progress bar display, and event callback functions. It also supports canceling the upload task during the resumable upload process. If a network exception or similar issue causes a file upload to fail, you may invoke this interface again to resume uploading the unfinished portion from the breakpoint.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Category


* To upload objects, your account must have the `tos:PutObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must comply with specific requirements. For detailed information, please refer to [Object Naming Specifications](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* `uploadFile` interface supports a maximum of 1,000 concurrent threads, with a default chunk size of 20 MiB.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When multi\-versioning is enabled for a bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.

* TOS is a distributed object storage product designed for massive storage. Its internal partitions store object index data. To horizontally scale the maximum throughput when uploading and downloading objects, and to reduce the likelihood of hot partitions, please avoid using lexicographically incremental object naming. For more details, refer to [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).


<span id=".5Z-65pys56S65L6L"></span>
## **Basic Example**

The following code demonstrates the basic usage of the `uploadFile` interface.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.UploadFileV2Input;
import com.volcengine.tos.model.object.UploadFileV2Output;

public class UploadFileExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String uploadFilePath = "example_dir/example_file.txt";
        int taskNum = 5;
        long partSize = 20 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            UploadFileV2Input input = new UploadFileV2Input().setBucket(bucketName).setKey(objectKey)
                    .setFilePath(uploadFilePath).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
            UploadFileV2Output output = tos.uploadFile(input);
            System.out.println("uploadFile succeed, object's etag is " + output.getEtag());
            System.out.println("uploadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("uploadFile failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("uploadFile failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("uploadFile failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LqL5Lu25Zue6LCD"></span>
## **Event Callback**

The following code demonstrates how to customize a listener callback function during the resumable upload process.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.event.UploadEventType;
import com.volcengine.tos.model.object.*;

public class UploadFileWithEventListenerExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String uploadFilePath = "example_dir/example_file.txt";
        int taskNum = 5;
        long partSize = 20 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            UploadEventListener listener = new UploadEventListener() {
                @Override
                public void eventChange(UploadEvent uploadEvent) {
                    if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventCreateMultipartUploadSucceed) {
                        System.out.println("event change, createMultipartUpload succeed");
                    }
                    if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventCreateMultipartUploadFailed) {
                        System.out.println("event change, createMultipartUpload failed");
                    }
                    if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventUploadPartSucceed) {
                        System.out.println("event change, uploadPart succeed");
                    }
                    if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventUploadPartFailed) {
                        System.out.println("event change, uploadPart failed");
                    }
                    if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventUploadPartAborted) {
                        System.out.println("event change, uploadPart aborted");
                    }
                    if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventCompleteMultipartUploadSucceed) {
                        System.out.println("event change, completeMultipartUpload succeed");
                    }
                    if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventCompleteMultipartUploadFailed) {
                        System.out.println("event change, completeMultipartUpload failed");
                    }
                }
            };
            UploadFileV2Input input = new UploadFileV2Input().setBucket(bucketName).setKey(objectKey)
                    .setFilePath(uploadFilePath).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum)
                    .setUploadEventListener(listener);
            UploadFileV2Output output = tos.uploadFile(input);
            System.out.println("uploadFile succeed, object's etag is " + output.getEtag());
            System.out.println("uploadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("uploadFile failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("uploadFile failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("uploadFile failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
## **Cancellation Mechanism**

During the resumable upload process, the SDK supports canceling upload tasks. The following code demonstrates how to cancel an ongoing resumable upload task.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.event.UploadEventType;
import com.volcengine.tos.model.object.*;

public class UploadFileWithCancelExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String uploadFilePath = "example_dir/example_file.txt";
        int taskNum = 5;
        long partSize = 20 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            UploadFileV2Input input = new UploadFileV2Input().setBucket(bucketName).setKey(objectKey)
                    .setFilePath(uploadFilePath).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);。
            boolean isAbort = true;
            UploadEventListener listener = new UploadEventListener() {
                @Override
                public void eventChange(UploadEvent uploadEvent) {
                    if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventUploadPartFailed) {
                        System.out.println("event change, uploadPart failed");
                        if (input.getCancelHook() != null) {
                            input.getCancelHook().cancel(isAbort);
                        }
                    }
                }
            };
            input.setCancelHook(true).setUploadEventListener(listener);
            UploadFileV2Output output = tos.uploadFile(input);
            System.out.println("uploadFile succeed, object's etag is " + output.getEtag());
            System.out.println("uploadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("uploadFile failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("uploadFile failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("uploadFile failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LiK5Lyg5pe25aSE55CG6L-b5bqm5p2h5ZKM6K6-572u5a6i5oi356uv6ZmQ6YCf"></span>
## **Handling the progress bar during upload and configuring client\-side rate limiting**

The following code demonstrates how to utilize the progress bar functionality and configure upload client rate limiting.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.event.DataTransferListener;
import com.volcengine.tos.comm.event.DataTransferStatus;
import com.volcengine.tos.comm.event.DataTransferType;
import com.volcengine.tos.comm.ratelimit.RateLimiter;
import com.volcengine.tos.internal.util.ratelimit.DefaultRateLimiter;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;
import com.volcengine.tos.model.object.UploadFileV2Input;
import com.volcengine.tos.model.object.UploadFileV2Output;

import java.io.File;

public class UploadFileWithProgressAndRateLimiterExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String uploadFilePath = "example_dir/example_file.txt";
        int taskNum = 5;
        long partSize = 20 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            UploadFileV2Input input = new UploadFileV2Input().setBucket(bucketName).setKey(objectKey)
                    .setFilePath(uploadFilePath).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
            
            ObjectMetaRequestOptions options = new ObjectMetaRequestOptions().setContentLength(new File(uploadFilePath).length());
            input.setOptions(options);
            DataTransferListener listener = getDataTransferListener();
            input.setDataTransferListener(listener);

            RateLimiter limiter = new DefaultRateLimiter(20 * 1024 * 1024, 5 * 1024 * 1024);
            input.setRateLimiter(limiter);

            UploadFileV2Output output = tos.uploadFile(input);
            System.out.println("uploadFile succeed, object's etag is " + output.getEtag());
            System.out.println("uploadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("uploadFile failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("uploadFile failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("uploadFile failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static DataTransferListener getDataTransferListener() {
        return new DataTransferListener() {
            @Override
            public void dataTransferStatusChange(DataTransferStatus dataTransferStatus) {
                if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_STARTED) {
                    System.out.println("uploadFile started.");
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_RW) {
                    System.out.printf("uploadFile, send %d bytes once, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getRwOnceBytes(), dataTransferStatus.getConsumedBytes(),
                            dataTransferStatus.getTotalBytes());
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_FAILED) {
                    System.out.printf("uploadFile failed, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getConsumedBytes(), dataTransferStatus.getTotalBytes());
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_SUCCEED) {
                    System.out.printf("uploadFile succeed, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getConsumedBytes(), dataTransferStatus.getTotalBytes());
                }
            }
        };
    }
}
```
