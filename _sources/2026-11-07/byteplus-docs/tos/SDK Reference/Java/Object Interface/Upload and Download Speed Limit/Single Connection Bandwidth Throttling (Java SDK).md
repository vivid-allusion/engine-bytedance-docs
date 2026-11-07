---
title: "Single Connection Bandwidth Throttling (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Single-link-speed-limit-java-sdk"
---

The Java SDK upload and download series interfaces, including getObject, getObjectToFile, putObject, etc., all support single\-connection rate limiting. This document describes how to use the single connection rate limiting feature.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

Starting from version 2.6.0, the Java SDK supports server\-side rate limiting for single\-connection upload and download requests.

<span id=".5pSv5oyB5Y2V6ZO-5o6l6ZmQ6YCf55qELXNkay3mjqXlj6M="></span>
## SDK interface supporting single\-connection rate limiting


* putObject

* putObjectFromFile

* appendObject

* uploadPart

* uploadFile

* getObject

* getObjectToFile

* downloadFile

* copyObject

* uploadPartCopy

* resumableCopyObject


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code uses the getObject API as an example to demonstrate how to use client\-side rate limiting. The usage of other upload and download interfaces is similar.

```Java
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
import java.util.Map;

public class GetObjectWithTrafficLimitExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath = "example_dir/example_file.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        long trafficLimit = 5 * 8 * 1024 * 1024;
        ObjectMetaRequestOptions options = new ObjectMetaRequestOptions();
        options.setTrafficLimit(trafficLimit);
        GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName)
                .setKey(objectKey).setOptions(options);
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


The configuration of the trafficLimit rate\-limiting parameter differs for the uploadFile, downloadFile, and resumableCopyObject interfaces.

The following code uses the uploadFile interface as an example to demonstrate how to use the single\-link rate limiting feature. The usage of the downloadFile and resumableCopyObject interfaces is similar.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.UploadFileV2Input;
import com.volcengine.tos.model.object.UploadFileV2Output;

public class UploadFileWithTrafficLimitExample {
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
        long trafficLimit = 10 * 1024 * 1024;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            UploadFileV2Input input = new UploadFileV2Input().setBucket(bucketName).setKey(objectKey)
                    .setFilePath(uploadFilePath).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum)
                    .setTrafficLimit(trafficLimit);
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
