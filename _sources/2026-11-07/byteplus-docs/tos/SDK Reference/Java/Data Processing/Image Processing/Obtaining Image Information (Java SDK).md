---
title: "Obtaining Image Information (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-image-information-java-sdk"
---

The image information retrieval function can obtain the basic attributes of an image, including its height, width, size, and format. If the image contains Exif information, the content will be returned in JSON format. This document describes how to obtain image information using the TOS Java SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to obtain image information.

```java
import com.fasterxml.jackson.core.JacksonException;
import com.fasterxml.jackson.databind.JsonNode;
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.internal.util.TosUtils;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.ByteArrayOutputStream;
import java.io.IOException;

public class ImageInfoExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";
        String objectKey = "image.png";
        String style = "image/info"; 

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
                System.out.println("Get image info succeed, image info is " + respBody);
                JsonNode jsonNode = TosUtils.getJsonMapper().readTree(respBody);
                String height = jsonNode.get("ImageHeight").get("value").asText();
                String width = jsonNode.get("ImageWidth").get("value").asText();
                String fileSize = jsonNode.get("FileSize").get("value").asText();
                String format = jsonNode.get("Format").get("value").asText();
                System.out.println("Image info height:" + height + ", width:" + width + ", size:" + fileSize + ", format:" + format);
            } catch (JacksonException e) {
                System.out.println("parse response data failed");
                e.printStackTrace();
            } catch (IOException e) {
                System.out.println("read response data failed");
                e.printStackTrace();
            }
        } catch (TosClientException e) {
            System.out.println("get image info failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("get image info failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("get image info failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to obtaining image information, please refer to [Obtaining Image Information](https://docs.byteplus.com/docs/tos/docs-information-query).
