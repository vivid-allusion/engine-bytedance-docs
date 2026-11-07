---
title: "Video Frame Extraction (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-framing-java-sdk"
---

The video frame capture function enables extraction of a single frame from a video stream at a specified time, resizes it to the designated image size, and saves it as an image. This document explains how to perform video frame extraction using the TOS Java SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to capture the video frame at 300 milliseconds and download the resulting image to the local device.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.FileOutputStream;
import java.io.IOException;

public class VideoSnapshotExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";
        String objectKey = "video.mp4";
        String filePath = "temp.jpg";
        String style = "video/snapshot,t_300"; 

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setProcess(style);
            try (FileOutputStream fileOutputStream = new FileOutputStream(filePath);
                 GetObjectV2Output output = tos.getObject(input)) {
                byte[] buffer = new byte[1024];
                int length;
                while ((length = output.getContent().read(buffer)) != -1) {
                    fileOutputStream.write(buffer, 0, length);
                }
                System.out.println("video process succeed, object's metadata is " + output.getGetObjectBasicOutput());
            } catch (IOException e) {
                System.out.println("write data to file failed");
                e.printStackTrace();
            }
        } catch (TosClientException e) {
            System.out.println("video process failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("video process failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("video process failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to video frame extraction, please refer to [Video Frame Extraction](https://docs.byteplus.com/docs/tos/docs-video-frame-capture).
