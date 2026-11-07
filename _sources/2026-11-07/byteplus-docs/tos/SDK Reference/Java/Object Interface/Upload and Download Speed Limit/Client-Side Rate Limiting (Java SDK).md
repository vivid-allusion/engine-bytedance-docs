---
title: "Client-Side Rate Limiting (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Client-side-speed-limit-java-sdk"
---

The series of upload and download interfaces in the Java SDK, including getObject, getObjectToFile, and downloadFile, all support client\-side rate limiting for individual requests. This article describes how to use the client\-side rate limiting feature.

<span id=".5pSv5oyB5a6i5oi356uv6ZmQ6YCf55qELXNkay3mjqXlj6M="></span>
## SDK interface supporting client\-side rate limiting


* putObject

* putObjectFromFile

* appendObject

* uploadPart

* uploadFile

* getObject

* getObjectToFile

* downloadFile


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code uses the getObject API as an example to demonstrate how to use the client\-side rate limiting feature. The usage of other download interfaces is similar.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.ratelimit.RateLimiter;
import com.volcengine.tos.internal.util.ratelimit.DefaultRateLimiter;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Map;

public class GetObjectWithRateLimiterExample {
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
        RateLimiter limiter = new DefaultRateLimiter(20 * 1024 * 1024, 5 * 1024 * 1024);
        GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setRateLimiter(limiter);
        try(GetObjectV2Output output = tos.getObject(input);
            FileOutputStream fos = new FileOutputStream(file)) {
            System.out.println("begin to read content in object to file.");
            if (output.getContent() != null) {
                byte[] buffer = new byte[4096];
                int length;
                while ((length = output.getContent().read(buffer)) != -1) {
                    fos.write(buffer, 0, length);
                }
            }
            fos.flush();
            System.out.println("getObject succeed.");
            System.out.println("object's etag is " + output.getEtag());
            System.out.println("object's lastModified is " + output.getLastModified());
            System.out.println("object's crc64 value is " + output.getHashCrc64ecma());
            System.out.println("object's storageClass is " + output.getStorageClass());
            System.out.println("object's cacheControl is " + output.getCacheControl());
            System.out.println("object's contentDisposition is " + output.getContentDisposition());
            System.out.println("object's contentEncoding is " + output.getContentEncoding());
            System.out.println("object's contentLanguage is " + output.getContentLanguage());
            System.out.println("object's contentType is " + output.getContentType());
            if (output.getCustomMetadata() != null) {
                System.out.println("object has custom meta data.");
                for (Map.Entry<String, String> entry : output.getCustomMetadata().entrySet()) {
                    System.out.println("custom meta key: " + entry.getKey() + ", value: " + entry.getValue());
                }
            }
        } catch (IOException e) {
            System.out.println("read data in object failed");
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
