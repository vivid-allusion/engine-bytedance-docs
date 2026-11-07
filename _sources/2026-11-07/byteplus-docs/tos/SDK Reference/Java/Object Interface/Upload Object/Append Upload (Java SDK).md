---
title: "Append Upload (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-java-sdk"
---

Append upload refers to appending new data to the end of existing object data. The object type created by append upload is an Appendable Object, which allows data to be appended to the end of the object. Objects created through normal upload and multipart upload are of the Normal Object type and do not support data append operations.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before appending to an object, you must have the `tos:PutObject` permission. For details, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must comply with specific conventions. For detailed information, please refer to [Object naming conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale data storage. Its internal partitions store object index data. To horizontally scale the maximum throughput for uploading and downloading objects, and to reduce the likelihood of hotspot partitions, please avoid using lexicographically incremental object naming. For more details, see [Performance optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When versioning is enabled for a bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.

* Append upload operations for objects do not support requests using Chunk\-Encoded transfer encoding. When performing append uploads with network streams, please retrieve data iteratively and append the data to the upload.


<span id=".6ZmQ5Yi26K-05piO"></span>
## Limitations

The following restrictions apply when using append upload:


* The size of an appendable object must not exceed 5 GiB.

* When a normal upload is performed on an appendable object, the object will be overwritten, and its type will change from "Appendable" to "Normal".

* Append upload is not supported for normal objects.

* Appendable objects do not support copying (CopyObject).

* Append upload does not support requests using Chunk\-Encoded transfer encoding. When using this interface, ensure that the length of the uploaded data is specified.

* If your bucket is in a state where versioning is enabled or suspended, the append upload interface cannot be used for that bucket.

* If your bucket is configured with Infrequent Access Storage, the append upload interface cannot be used for that bucket.


<span id=".6L-95Yqg5LiK5Lyg5a2X56ym5LiyLWJ5dGUt5pWw57uE"></span>
## **Append string/byte array**

The following code demonstrates how to repeatedly append a string to the `example_object.txt` file located in the `example_dir` directory of the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.AppendObjectInput;
import com.volcengine.tos.model.object.AppendObjectOutput;

import java.io.ByteArrayInputStream;
import java.util.Arrays;

public class AppendObjectWithByteArrayInputStreamExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            byte[] data1 = new byte[128 * 1024];
            Arrays.fill(data1, (byte) 'A');
            ByteArrayInputStream stream = new ByteArrayInputStream(data1);
            long contentLength = data1.length;
            long offset = 0;
            AppendObjectInput input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setContent(stream).setContentLength(contentLength).setOffset(offset);
            
            AppendObjectOutput output = tos.appendObject(input);
            System.out.println("appendObject first time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
            System.out.println("appendObject first time succeed, object's crc64 is " + output.getHashCrc64ecma());

            byte[] data2 = new byte[128 * 1024 + 1024];
            Arrays.fill(data2, (byte) 'B');
            contentLength = data2.length;
            offset = output.getNextAppendOffset();
            String preHashCrc64 = output.getHashCrc64ecma();
            input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey).setContent(new ByteArrayInputStream(data2))
                    .setOffset(offset).setContentLength(contentLength).setPreHashCrc64ecma(preHashCrc64);
            output = tos.appendObject(input);
            System.out.println("appendObject second time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
            System.out.println("appendObject second time succeed, object's crc64 is " + output.getHashCrc64ecma());

            byte[] data3 = new byte[256 * 1024 + 1024];
            Arrays.fill(data3, (byte) 'C');
            contentLength = data3.length;
            offset = output.getNextAppendOffset();
            preHashCrc64 = output.getHashCrc64ecma();
            input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey).setContent(new ByteArrayInputStream(data3))
                    .setOffset(offset).setContentLength(contentLength).setPreHashCrc64ecma(preHashCrc64);
            output = tos.appendObject(input);
            System.out.println("appendObject third time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
            System.out.println("appendObject third time succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("appendObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("appendObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("appendObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6L-95Yqg5LiK5Lyg5pys5Zyw5paH5Lu2"></span>
## **Append local files**

The following code demonstrates how to append a local file `example_file.txt` to the file `example_object.txt` located in the `example_dir` directory of the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.AppendObjectInput;
import com.volcengine.tos.model.object.AppendObjectOutput;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;

public class AppendObjectWithFileInputStreamExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath1 = "example_dir/example_file_1.txt";
        String filePath2 = "example_dir/example_file_2.txt";
        String filePath3 = "example_dir/example_file_3.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            AppendObjectOutput output = null;
            try(FileInputStream stream = new FileInputStream(filePath1)) {
                long contentLength = new File(filePath1).length();
                long offset = 0;
                AppendObjectInput input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey)
                        .setContent(stream).setContentLength(contentLength).setOffset(offset);
                
                output = tos.appendObject(input);
                System.out.println("appendObject first time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
                System.out.println("appendObject first time succeed, object's crc64 is " + output.getHashCrc64ecma());
            } catch (IOException e) {
                System.out.println("appendObject read file failed");
                e.printStackTrace();
            }


            try(FileInputStream stream = new FileInputStream(filePath2)) {
                long contentLength = new File(filePath2).length();
                long offset = output.getNextAppendOffset();
                String preHashCrc64 = output.getHashCrc64ecma();
                AppendObjectInput input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey).setContent(stream)
                        .setOffset(offset).setContentLength(contentLength).setPreHashCrc64ecma(preHashCrc64);
                output = tos.appendObject(input);
                System.out.println("appendObject second time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
                System.out.println("appendObject second time succeed, object's crc64 is " + output.getHashCrc64ecma());
            } catch (IOException e) {
                System.out.println("appendObject read file failed");
                e.printStackTrace();
            }

            try(FileInputStream stream = new FileInputStream(filePath3)) {
                long contentLength = new File(filePath3).length();
                long offset = output.getNextAppendOffset();
                String preHashCrc64 = output.getHashCrc64ecma();
                AppendObjectInput input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey).setContent(stream)
                        .setOffset(offset).setContentLength(contentLength).setPreHashCrc64ecma(preHashCrc64);
                output = tos.appendObject(input);
                System.out.println("appendObject second time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
                System.out.println("appendObject second time succeed, object's crc64 is " + output.getHashCrc64ecma());
            } catch (IOException e) {
                System.out.println("appendObject read file failed");
                e.printStackTrace();
            }
        } catch (TosClientException e) {
            System.out.println("appendObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("appendObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("appendObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LiK5Lyg5pe25aSE55CG6L-b5bqm5p2h5ZKM6K6-572u5a6i5oi356uv6ZmQ6YCf"></span>
## **Handle the progress bar and configure client\-side rate limiting during upload**

The following code demonstrates how to use the progress bar functionality and configure client\-side upload rate limiting, using the example of appending upload of a string or byte array.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.event.DataTransferListener;
import com.volcengine.tos.comm.event.DataTransferStatus;
import com.volcengine.tos.comm.event.DataTransferType;
import com.volcengine.tos.comm.ratelimit.RateLimiter;
import com.volcengine.tos.internal.util.ratelimit.DefaultRateLimiter;
import com.volcengine.tos.model.object.AppendObjectInput;
import com.volcengine.tos.model.object.AppendObjectOutput;

import java.io.ByteArrayInputStream;
import java.util.Arrays;

public class AppendObjectWithProgressAndRateLimiterExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt.12123123";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            byte[] data1 = new byte[128 * 1024];
            Arrays.fill(data1, (byte) 'A');
            ByteArrayInputStream stream = new ByteArrayInputStream(data1);
            long contentLength = data1.length;
            long offset = 0;
            AppendObjectInput input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setContent(stream).setContentLength(contentLength).setOffset(offset);

            input.setContentLength(contentLength);
            DataTransferListener listener = getDataTransferListener();
            input.setDataTransferListener(listener);

            RateLimiter limiter = new DefaultRateLimiter(20 * 1024 * 1024, 5 * 1024 * 1024);
            input.setRateLimiter(limiter);

            AppendObjectOutput output = tos.appendObject(input);
            System.out.println("appendObject first time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
            System.out.println("appendObject first time succeed, object's crc64 is " + output.getHashCrc64ecma());

            byte[] data2 = new byte[128 * 1024 + 1024];
            Arrays.fill(data2, (byte) 'B');
            contentLength = data2.length;
            offset = output.getNextAppendOffset();
            String preHashCrc64 = output.getHashCrc64ecma();
            input.setContent(new ByteArrayInputStream(data2)).setOffset(offset).setContentLength(contentLength).setPreHashCrc64ecma(preHashCrc64);
            output = tos.appendObject(input);
            System.out.println("appendObject second time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
            System.out.println("appendObject second time succeed, object's crc64 is " + output.getHashCrc64ecma());

            byte[] data3 = new byte[256 * 1024 + 1024];
            Arrays.fill(data3, (byte) 'C');
            contentLength = data3.length;
            offset = output.getNextAppendOffset();
            preHashCrc64 = output.getHashCrc64ecma();
            input.setContent(new ByteArrayInputStream(data3)).setOffset(offset).setContentLength(contentLength).setPreHashCrc64ecma(preHashCrc64);
            output = tos.appendObject(input);
            System.out.println("appendObject third time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
            System.out.println("appendObject third time succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("appendObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("appendObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("appendObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static DataTransferListener getDataTransferListener() {
        return new DataTransferListener() {
            @Override
            public void dataTransferStatusChange(DataTransferStatus dataTransferStatus) {
                if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_STARTED) {
                    System.out.println("appendObject started.");
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_RW) {
                    System.out.printf("appendObject, send %d bytes once, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getRwOnceBytes(), dataTransferStatus.getConsumedBytes(),
                            dataTransferStatus.getTotalBytes());
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_FAILED) {
                    System.out.printf("appendObject failed, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getConsumedBytes(), dataTransferStatus.getTotalBytes());
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_SUCCEED) {
                    System.out.printf("appendObject succeed, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getConsumedBytes(), dataTransferStatus.getTotalBytes());
                }
            }
        };
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For the API documentation on append upload, please refer to [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject).
