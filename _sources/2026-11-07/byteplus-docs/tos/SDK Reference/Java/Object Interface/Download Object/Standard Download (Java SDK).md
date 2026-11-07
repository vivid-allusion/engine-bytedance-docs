---
title: "Standard Download (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-download-java-sdk"
---

Standard download refers to downloading a single object via the `getObject` interface. The TOS Java SDK supports downloading objects either into memory or to a local file, and allows overriding HTTP response headers during object download.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Before downloading an object, you must have the `tos:GetObject` permission. For specific instructions, refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads multiple copies of the same object at the same time, your access speed will be limited by TOS bandwidth and regional restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".5LiL6L295Yiw5YaF5a2Y"></span>
## **Download to memory**

The Java SDK's `getObject` interface returns an InputStream object, which can be read directly from memory.

The following code demonstrates how to download the `example_object.txt` file located in the `example_dir` directory of the target bucket `bucket-example`, and directly read and print its string content from memory.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class GetObjectInStringExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey);
        try(GetObjectV2Output output = tos.getObject(input);
            BufferedReader reader = new BufferedReader(new InputStreamReader(output.getContent()))) {
            System.out.println("begin to read content in object.");
            String line = reader.readLine();
            while (line != null) {
                System.out.println(line);
                line = reader.readLine();
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


<span id=".5LiL6L295Yiw5pys5Zyw5paH5Lu2"></span>
## **Download to a local file**

The `getObject` interface of the Java SDK returns an InputStream object, from which you can read data and write it to a local file. You can also directly download to a local file via the `getObjectToFile` API.

<span id=".6YCa6L-HLWdldG9iamVjdC3mjqXlj6PkuIvovb3liLDmnKzlnLDmlofku7Y="></span>
### Download to a local file via the `getObject` interface.

The following code demonstrates how to download the `example_object.txt` file located in the `example_dir` directory of the target bucket `bucket-example` to the local system.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.*;
import java.util.Map;

public class GetObjectToFileWithInputStreamExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath = "example_dir/example_file.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey);
        File file = new File(filePath);
        if (file.getParentFile() != null && !file.getParentFile().exists()) {
            file.getParentFile().mkdirs();
        }
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


<span id=".6YCa6L-HLWdldG9iamVjdHRvZmlsZS3mjqXlj6PkuIvovb3liLDmnKzlnLDmlofku7Y="></span>
### Download to a local file via the `getObjectToFile` interface.

The following code demonstrates how to download the `example_object.txt` file located in the `example_dir` directory in the target bucket bucket\-example to the local machine.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectToFileInput;
import com.volcengine.tos.model.object.GetObjectToFileOutput;
import com.volcengine.tos.model.object.GetObjectV2Input;

import java.util.Map;

public class GetObjectToFileExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath = "example_dir/example_file.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey);
            GetObjectToFileInput fileInput = new GetObjectToFileInput().setFilePath(filePath).setBucket(bucketName).setKey(objectKey);
            GetObjectToFileOutput fileOutput = tos.getObjectToFile(fileInput);
            System.out.println("getObjectToFile succeed.");
            System.out.println("object's etag is " + fileOutput.getEtag());
            System.out.println("object's lastModified is " + fileOutput.getLastModified());
            System.out.println("object's crc64 value is " + fileOutput.getHashCrc64ecma());
            System.out.println("object's storageClass is " + fileOutput.getStorageClass());
            System.out.println("object's cacheControl is " + fileOutput.getCacheControl());
            System.out.println("object's contentDisposition is " + fileOutput.getContentDisposition());
            System.out.println("object's contentEncoding is " + fileOutput.getContentEncoding());
            System.out.println("object's contentLanguage is " + fileOutput.getContentLanguage());
            System.out.println("object's contentType is " + fileOutput.getContentType());
            if (fileOutput.getCustomMetadata() != null) {
                System.out.println("object has custom meta data.");
                for (Map.Entry<String, String> entry : fileOutput.getCustomMetadata().entrySet()) {
                    System.out.println("custom meta key: " + entry.getKey() + ", value: " + entry.getValue());
                }
            }
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


<span id=".5LiL6L295pe26YeN5YaZLWh0dHAt5ZON5bqU5aS0"></span>
## **Rewrite HTTP Response Headers During Download**

The Java SDK allows you to specify particular HTTP response headers returned by the server when downloading objects.

The following code demonstrates how to download the `example_object.txt` file from the `example_dir` directory in the target bucket `bucket-example` to the local machine, and rewrite the HTTP response headers.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class GetObjectWithResponseHeaderExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey)
                .setResponseContentType("application/json");
        try(GetObjectV2Output output = tos.getObject(input);
            BufferedReader reader = new BufferedReader(new InputStreamReader(output.getContent()))) {
            System.out.println("begin to read content in object.");
            String line = reader.readLine();
            while (line != null) {
                System.out.println(line);
                line = reader.readLine();
            }
            System.out.println("getObject succeed, object's content-type is " + output.getContentType());
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


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For the API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
