---
title: "Resumable Download (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-download-java-sdk"
---

When downloading large objects, network fluctuations and similar issues may result in download failure. The TOS Java SDK incorporates a retry mechanism to enhance the stability of object downloads; however, it is still possible that the download may not be completed after multiple retry attempts. To address the aforementioned issue, the Java SDK provides a resumable download feature. If a download of a large object fails, the interface can be invoked again to continue downloading from the previous progress point. When using the resumable download interface of the Java SDK, you can customize settings such as chunk size, the number of concurrent download threads, client\-side download rate limiting, and event callback functions. Additionally, the interface supports canceling the resumable download task during its execution.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities at the same time, your access speed will be limited by TOS bandwidth and regional restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".5Z-65pys56S65L6L"></span>
## **Basic Example**

The following code demonstrates the basic usage of the SDK's resumable download interface `downloadFile`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.DownloadFileInput;
import com.volcengine.tos.model.object.DownloadFileOutput;

public class DownloadFileExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        
        String downloadFilePath = "example_dir/example_file.txt";
        int taskNum = 5;
        long partSize = 10 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DownloadFileInput input = new DownloadFileInput().setBucket(bucketName).setKey(objectKey)
                    .setFilePath(downloadFilePath).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
            DownloadFileOutput output = tos.downloadFile(input);
            System.out.println("downloadFile succeed, object's etag is " + output.getEtag());
            System.out.println("downloadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("downloadFile failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("downloadFile failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("downloadFile failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LqL5Lu25Zue6LCD"></span>
## **Event Callback**

The following code demonstrates how to customize the listener callback function during the resumable download process.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.event.DownloadEventType;
import com.volcengine.tos.model.object.*;

public class DownloadFileWithEventListenerExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        String downloadFilePath = "example_dir/example_file.txt";
        int taskNum = 5;
        long partSize = 10 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            HeadObjectV2Input head = new HeadObjectV2Input().setBucket(bucketName).setKey(objectKey);
            DownloadEventListener listener = new DownloadEventListener() {
                @Override
                public void eventChange(DownloadEvent downloadEvent) {
                    if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventCreateTempFileSucceed) {
                        System.out.println("event change, createTempFile succeed");
                    }
                    if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventCreateTempFileFailed) {
                        System.out.println("event change, createTempFile failed");
                    }
                    if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventDownloadPartSucceed) {
                        System.out.println("event change, downloadPart succeed");
                    }
                    if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventDownloadPartFailed) {
                        System.out.println("event change, downloadPart failed");
                    }
                    if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventDownloadPartAborted) {
                        System.out.println("event change, downloadPart aborted");
                    }
                    if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventRenameTempFileSucceed) {
                        System.out.println("event change, renameTempFile succeed");
                    }
                    if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventRenameTempFileFailed) {
                        System.out.println("event change, renameTempFile failed");
                    }
                }
            };
            DownloadFileInput input = new DownloadFileInput().setHeadObjectV2Input(head)
                    .setFilePath(downloadFilePath).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum)
                    .setDownloadEventListener(listener);
            DownloadFileOutput output = tos.downloadFile(input);
            System.out.println("downloadFile succeed, object's etag is " + output.getEtag());
            System.out.println("downloadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("downloadFile failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("downloadFile failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("downloadFile failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Y-W5raI5py65Yi2"></span>
## **Cancellation Mechanism**

During the resumable download process, the SDK supports canceling download tasks. The following code demonstrates how to cancel an ongoing resumable download task.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.event.DownloadEventType;
import com.volcengine.tos.model.object.*;

public class DownloadFileWithCancelExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        String downloadFilePath = "example_dir/example_file.txt";
        int taskNum = 5;
        long partSize = 10 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            HeadObjectV2Input head = new HeadObjectV2Input().setBucket(bucketName).setKey(objectKey);
            DownloadFileInput input = new DownloadFileInput().setHeadObjectV2Input(head)
                    .setFilePath(downloadFilePath).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
            boolean isAbort = true;
            DownloadEventListener listener = new DownloadEventListener() {
                @Override
                public void eventChange(DownloadEvent downloadEvent) {
                    if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventDownloadPartFailed) {
                        System.out.println("event change, uploadPart failed");
                        if (input.getCancelHook() != null) {
                            input.getCancelHook().cancel(isAbort);
                        }
                    }
                }
            };
            input.setCancelHook(true).setDownloadEventListener(listener);
            DownloadFileOutput output = tos.downloadFile(input);
            System.out.println("downloadFile succeed, object's etag is " + output.getEtag());
            System.out.println("downloadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("downloadFile failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("downloadFile failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("downloadFile failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```
