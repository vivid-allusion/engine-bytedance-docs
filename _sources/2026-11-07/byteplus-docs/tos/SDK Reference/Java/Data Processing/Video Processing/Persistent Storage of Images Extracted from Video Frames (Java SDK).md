---
title: "Persistent Storage of Images Extracted from Video Frames (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-capture-image-persistence-java-sdk"
---

TOS supports saving images extracted from video frames to a specified storage bucket. This article explains how to use the TOS Java SDK to save images captured from video frames to a specified storage bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Category

Only Java SDK version 2.6.2 supports the persistent storage of video frame capture images.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to extract the video frame at 300 milliseconds, name the resulting image temp.jpg, and save it to the bucket\-example storage bucket.

```java
import com.fasterxml.jackson.core.JacksonException;
import com.fasterxml.jackson.core.type.TypeReference;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.internal.util.TosUtils;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.util.Base64;

public class VideoSnapshotSaveAsExample {
    static class SaveAsResult {
        String bucket;
        String fileSize;
        String object;
        String status;

        @Override
        public String toString() {
            return "SaveAsResult{" +
                    "bucket='" + bucket + '\'' +
                    ", fileSize='" + fileSize + '\'' +
                    ", object='" + object + '\'' +
                    ", status='" + status + '\'' +
                    '}';
        }
    }

    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";
        String objectKey = "video.mp4";
        String style = "video/snapshot,t_300"; 
        String saveBucket = "bucket-example";
        String saveObject = "temp.jpg";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setProcess(style)
                    .setSaveBucket(Base64.getUrlEncoder().encodeToString(saveBucket.getBytes(StandardCharsets.UTF_8)))
                    .setSaveObject(Base64.getUrlEncoder().encodeToString(saveObject.getBytes(StandardCharsets.UTF_8)));
            try (ByteArrayOutputStream stream = new ByteArrayOutputStream();
                 GetObjectV2Output output = tos.getObject(input)) {
                byte[] buffer = new byte[1024];
                int length;
                while ((length = output.getContent().read(buffer)) != -1) {
                    stream.write(buffer, 0, length);
                }
                String respBody = stream.toString("UTF-8");
                System.out.println("Image inspect success, inspect info is " + respBody);
                SaveAsResult result = TosUtils.getJsonMapper().readValue(respBody, new TypeReference<SaveAsResult>() {
                });
                System.out.println(result.toString());
            } catch (JacksonException e) {
                System.out.println("parse response data failed");
                e.printStackTrace();
            } catch (IOException e) {
                System.out.println("read response data failed");
                e.printStackTrace();
            }
        } catch (TosClientException e) {
            System.out.println("Image saveAs failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("Image saveAs failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("Image saveAs failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to video frame image persistence, please refer to [Image Persistence](https://docs.byteplus.com/docs/tos/docs-image-storage).
