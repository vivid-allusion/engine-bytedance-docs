---
title: "Abnormal Image Detection (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Abnormal-image-detection-java-sdk"
---

Abnormal image detection is used to determine whether an image contains suspicious files other than the image itself, such as MPEG\-TS files. If an image is detected to contain suspicious files, you may process the image file to prevent your storage space from being illicitly used by image hosting services. This article introduces how to use the TOS Java SDK for anomaly image detection.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Category


* The size of the original image for detection must not exceed 20MB.

* Abnormal image detection is supported only for files in JPG, JPEG, PNG, BMP, GIF, and pure TS video stream formats.

* The abnormal image detection function is billed according to the number of processing instances. For a detailed explanation, please refer to [Data Processing Fees](https://docs.byteplus.com/docs/tos/docs-data-processing-fee).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to detect abnormal images.

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

public class ImageInspectExample {
    static class ImageInspectResult {
        int picSize;
        String picType;
        boolean suspicious;
        int suspiciousBeginByte;
        int suspiciousEndByte;
        int suspiciousSize;
        String suspiciousType;

        public String toString() {
            return "[picSize:" + this.picSize + ",picType:" + this.picType + ",suspicious:" + this.suspicious +
                    ",suspiciousBeginByte:" + this.suspiciousBeginByte + ",suspiciousEndByte:" + this.suspiciousEndByte
                    + ",suspiciousSize:" + this.suspiciousSize + ",suspiciousType:" + this.suspiciousType + "]";
        }
    }

    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";
        String objectKey = "image.png";
        String style = "image/inspect";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try {
            GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setProcess(style);
            try (ByteArrayOutputStream stream = new ByteArrayOutputStream();
                 GetObjectV2Output output = tos.getObject(input)) {
                byte[] buffer = new byte[1024];
                int length;
                while ((length = output.getContent().read(buffer)) != -1) {
                    stream.write(buffer, 0, length);
                }
                String respBody = stream.toString("UTF-8");
                System.out.println("Image inspect success, inspect info is " + respBody);
                ImageInspectResult result = TosUtils.getJsonMapper().readValue(respBody, new TypeReference<ImageInspectResult>() {
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
            System.out.println("Image inspect failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("Image inspect failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("Image inspect failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to abnormal image detection, please refer to [Abnormal Image Detection](https://docs.byteplus.com/docs/6349/1140988).
