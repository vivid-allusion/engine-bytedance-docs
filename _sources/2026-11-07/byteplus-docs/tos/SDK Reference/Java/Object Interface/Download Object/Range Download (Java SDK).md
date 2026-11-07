---
title: "Range Download (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scope-download-java-sdk"
---

If you only need to retrieve a portion of the data within an object, you can use range download to obtain data within the specified range. This article introduces the range download feature of the TOS Java SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Before downloading an object, you must have the `tos:GetObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities simultaneously, your access speed will be limited by TOS bandwidth and regional restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".5oyH5a6aLXN0YXJ0LWVuZC3kuIvovb3lr7nosaE="></span>
## **Specify the Start and End Download Objects**

The following code demonstrates how to specify the rangeStart and rangeEnd parameters to download the `example_object.txt` file located in the `example_dir` directory of the target bucket `bucket-example` to the local system.

The rangeStart and rangeEnd parameters comply with the specification of the HTTP 'Range' header field. For example, rangeStart=1 and rangeEnd=10 indicate downloading data from the first byte to the tenth byte of the object, totaling 11 bytes. For more information, see [HTTP range requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Range_requests).

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;

public class GetObjectRangeExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath = "example_dir/example_file.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        File file = new File(filePath);
        if (file.getParentFile() != null && !file.getParentFile().exists()) {
            file.getParentFile().mkdirs();
        }
        long rangeStart = 0;
        long rangeEnd = 1023;
        ObjectMetaRequestOptions options = new ObjectMetaRequestOptions().setRange(rangeStart, rangeEnd);
        GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setOptions(options);
        try(FileOutputStream fos = new FileOutputStream(file);
            GetObjectV2Output output = tos.getObject(input)) {
            if (output.getContent() != null) {
                byte[] buffer = new byte[4096];
                int length;
                while ((length = output.getContent().read(buffer)) != -1) {
                    fos.write(buffer, 0, length);
                }
            }
            fos.flush();
            System.out.println("getObject succeed, object's contentRange is " + output.getContentRange());
        } catch (IOException e) {
            System.out.println("write data to file failed");
            e.printStackTrace();
        } catch (TosClientException e) {
            System.out.println("getObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
