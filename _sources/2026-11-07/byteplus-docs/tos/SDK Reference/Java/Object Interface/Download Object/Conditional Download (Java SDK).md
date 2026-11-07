---
title: "Conditional Download (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-java-sdk"
---

The TOS Java SDK supports configuring constraints for object downloads. When downloading an object, you can specify constraints such as the object's ETag or last modified time. The server will return the object data only if the object's information meets the specified conditions; otherwise, an appropriate error will be returned. This article describes how to download objects by specifying limiting conditions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Before downloading an object, you must have the `tos:GetObject` permission. For specific instructions, refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For specific operations, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads a large number of the same object simultaneously, your access speed will be limited by TOS bandwidth and regional restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".6ZmQ5a6a5p2h5Lu26K-05piO"></span>
## **Description of Limiting Conditions**

The following are the limitations supported by TOS.


|Parameter |Description |
|---|---|
|If\-Modified\-Since |If the specified time precedes the object's last modification time, the download proceeds as normal; otherwise, a 304 error (Not Modified) is returned. |
|If\-Unmodified\-Since |If the specified time is equal to or later than the object's last modification time, the download will proceed normally; otherwise, a 412 error (Precondition Failed) will be returned. |
|If\-Match |If the specified ETag matches the ETag of the object to be downloaded, the download proceeds normally; otherwise, a 412 error (Precondition Failed) is returned. |
|If\-None\-Match |If the specified ETag does not match the ETag of the object to be downloaded, the download proceeds normally; otherwise, a 304 error (Not Modified) is returned. |


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code demonstrates how to set constraints. When the conditions are met, the `example_object.txt` file in the `example_dir` directory of the target bucket `bucket-example` is downloaded to the local machine.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Map;

public class GetObjectWithIfConditionExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath = "example_dir/example_file.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        ObjectMetaRequestOptions options = new ObjectMetaRequestOptions();

        try{
            DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
            Date date = dateFormat.parse("2022-09-13 14:36:01");
            options.setIfModifiedSince(date);
        } catch (ParseException e) {
            System.out.println("date parse failed");
            e.printStackTrace();
        }

        try{
            DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
            Date date = dateFormat.parse("2222-12-31 14:36:01");
            options.setIfUnmodifiedSince(date);
        } catch (ParseException e) {
            System.out.println("date parse failed");
            e.printStackTrace();
        }

        HeadObjectV2Input head = new HeadObjectV2Input().setBucket(bucketName).setKey(objectKey);
        HeadObjectV2Output headOutput = tos.headObject(head);
        String etag = headOutput.getEtag();
        options.setIfMatch(etag);

        String wrongEtag = "XXXYYYZZZ";
        options.setIfNoneMatch(wrongEtag);

        GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setOptions(options);
        File file = new File(filePath);
        if (file.getParentFile() != null && !file.getParentFile().exists()) {
            file.getParentFile().mkdirs();
        }
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

For API documentation on downloading objects, refer to [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
