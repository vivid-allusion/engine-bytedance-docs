---
title: "Basic Image Processing (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Basic-image-processing-java-sdk"
---

TOS supports processing of stored images, including image resizing, image cropping, image watermarking, format conversion, and other image processing operations. This article introduces how to perform basic image processing using the TOS Java SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The original image must be in the JPG, PNG, BMP, GIF, WEBP, or TIFF format.

* The original image size must be 20 MB or smaller.

* The original image can have a width and height of up to 30,000 pixels, for a total of up to 250 million pixels. However, the width and height cannot exceed 4,096 pixels for the rotate operation.

* The resized image can have a width and height of up to 16,384 pixels, for a total of 16,777,216 pixels.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to fix the image height at 100px, convert the image format to JPG, and then download the image locally.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.FileOutputStream;
import java.io.IOException;

public class ImageProcessExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";
        String objectKey = "image.png";
        String filePath = "example_dir/image.jpg";
        String style = "image/resize,h_100/format,jpg"; 

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
                System.out.println("image process succeed, object's metadata is " + output.getGetObjectBasicOutput());
            } catch (IOException e) {
                System.out.println("write data to file failed");
                e.printStackTrace();
            }
        } catch (TosClientException e) {
            System.out.println("image process failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("image process failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("image process failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to image processing, please refer to the [Image Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_2).
