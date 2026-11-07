---
title: "Standard Upload (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-java-sdk"
---

Standard upload refers to uploading a single object via the TOS Java SDK `putObject` interface. The SDK consistently uses the InputStream class as the parameter for data streams to be uploaded. Depending on your business requirements, you may input data streams in various formats. For example, to upload strings or byte arrays, use ByteArrayInputStream; to upload files, use FileInputStream, etc. This document will provide usage instructions and sample code for uploading various data streams for your reference.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Before uploading an object, you must have the `tos:PutObject` permission. For detailed steps, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific requirements. For detailed information, please refer to [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage, with internal partitions that store object index data. To horizontally scale the maximum throughput for uploading and downloading objects and to reduce the probability of hotspot partitions, please avoid using lexicographically incremental object naming schemes. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.


<span id=".5LiK5Lyg5a2X56ym5LiyLWJ5dGUt5pWw57uE"></span>
## Upload String / Byte Array

The following code demonstrates how to upload a string to the file `example_object.txt` located in the `example_dir` directory of the target bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.ByteArrayInputStream;

public class PutObjectWithByteArrayInputStreamExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            String data = "1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'";
            byte[] dataInBytes = data.getBytes();
            ByteArrayInputStream stream = new ByteArrayInputStream(dataInBytes);
            PutObjectInput putObjectInput = new PutObjectInput()
                    .setBucket(bucketName).setKey(objectKey).setContent(stream);
            PutObjectOutput output = tos.putObject(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu2"></span>
## Upload Local File

There are two methods for uploading local files using the Java SDK. The first method is to pass an open FileInputStream object as a parameter to the `putObject` interface. The second method is to pass the path of the file to be uploaded or a File object as a parameter to the `putObjectFromFile` interface.

The following code demonstrates how to use the `putObject` interface to upload a local file, `example_dir/example_file.txt`, to the target bucket `bucket-example`, where it will be stored as `example_object.txt` in the `example_dir` directory.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;

public class PutObjectWithFileInputStreamExample {
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
        try(FileInputStream inputStream = new FileInputStream(file)){
            PutObjectInput putObjectInput = new PutObjectInput().setBucket(bucketName)
                    .setKey(objectKey).setContent(inputStream).setContentLength(file.length());
            PutObjectOutput output = tos.putObject(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (IOException e) {
            System.out.println("putObject read file failed");
            e.printStackTrace();
        } catch (TosClientException e) { 
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


The following code demonstrates how to use the `putObjectFromFile` interface to upload a local file `example_file.txt` to the `example_object.txt` file in the `example_dir` directory of the target bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectFromFileInput;
import com.volcengine.tos.model.object.PutObjectFromFileOutput;

public class PutObjectFromFileExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath = "example_dir/example_file.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            PutObjectFromFileInput putObjectInput = new PutObjectFromFileInput()
                    .setBucket(bucketName).setKey(objectKey).setFilePath(filePath);
            PutObjectFromFileOutput output = tos.putObjectFromFile(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LiK5Lyg572R57uc5rWB"></span>
## Upload Network Stream

The `putObject` interface of the Java SDK supports uploading resources from the network to TOS. The following code demonstrates how to upload a network stream to the file `example_object.txt` located in the `example_dir` directory of the target bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.BufferedInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.URL;

public class PutObjectWithUrlExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String url = "https://www.byteplus.com/en/";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try(InputStream inputStream = new BufferedInputStream(new URL(url).openStream())){
            PutObjectInput putObjectInput = new PutObjectInput().setBucket(bucketName).setKey(objectKey).setContent(inputStream);
            PutObjectOutput output = tos.putObject(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (IOException e) {
            System.out.println("putObject read data from url failed");
            e.printStackTrace();
        } catch (TosClientException e) {
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LiK5Lyg5pe26K6-572u5a-56LGh5YWD5pWw5o2u"></span>
## Setting Object Metadata During Upload

When uploading object data using the `putObject` or `putObjectFromFile` interfaces, the SDK also supports configuring object metadata, such as specifying the object's access control ACL, storage class StorageClass, custom object metadata, etc.

The following code demonstrates how to set object metadata when using `putObject`. Note that this setting is optional; please make a selection according to your actual business requirements.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.ByteArrayInputStream;
import java.util.HashMap;
import java.util.Map;

public class PutObjectWithMetaOptionsExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            String data = "1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'";
            ByteArrayInputStream stream = new ByteArrayInputStream(data.getBytes());
            ObjectMetaRequestOptions options = new ObjectMetaRequestOptions();
            options.setAclType(ACLType.ACL_PRIVATE);
            options.setStorageClass(StorageClassType.STORAGE_CLASS_STANDARD);
            options.setContentType("text/plain");
            options.setContentMD5("yjtlyPoGKxvDj+QOPocqjg==");
            Map<String, String> custom = new HashMap<>();
            custom.put("name", "volc_user");
            options.setCustomMetadata(custom);

            PutObjectInput putObjectInput = new PutObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setOptions(options).setContent(stream);
            PutObjectOutput output = tos.putObject(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LiK5Lyg5pe25aSE55CG6L-b5bqm5p2h"></span>
## Processing Progress Bar During Upload

The following code demonstrates how to utilize the progress bar feature, using local file upload as an example.

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
import com.volcengine.tos.model.object.*;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;

public class PutObjectWithProgressAndRateLimiterExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath = "example_dir/example_file.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try(FileInputStream inputStream = new FileInputStream(filePath)){
            PutObjectInput putObjectInput = new PutObjectInput().setBucket(bucketName).setKey(objectKey).setContent(inputStream);

            ObjectMetaRequestOptions options = new ObjectMetaRequestOptions().setContentLength(new File(filePath).length());
            putObjectInput.setOptions(options);
            DataTransferListener listener = getDataTransferListener();
            putObjectInput.setDataTransferListener(listener);

            PutObjectOutput output = tos.putObject(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (IOException e) {
            System.out.println("putObject read file failed");
            e.printStackTrace();
        } catch (TosClientException e) {
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static DataTransferListener getDataTransferListener() {
        return new DataTransferListener() {
            @Override
            public void dataTransferStatusChange(DataTransferStatus dataTransferStatus) {
                if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_STARTED) {
                    System.out.println("putObject started.");
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_RW) {
                    System.out.printf("putObject, send %d bytes once, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getRwOnceBytes(), dataTransferStatus.getConsumedBytes(),
                            dataTransferStatus.getTotalBytes());
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_FAILED) {
                    System.out.printf("putObject failed, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getConsumedBytes(), dataTransferStatus.getTotalBytes());
                } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_SUCCEED) {
                    System.out.printf("putObject succeed, has sent %d bytes, total %d bytes.\n",
                            dataTransferStatus.getConsumedBytes(), dataTransferStatus.getTotalBytes());
                }
            }
        };
    }
}
```


<span id=".6YGN5Y6G5pys5Zyw5paH5Lu25aS55LiK5Lyg"></span>
## Traverse Local Folder to Upload Files

The TOS Java SDK does not currently support batch uploading of files from a specified folder. You may manually traverse the local folder to upload files individually.

The following code demonstrates how to iterate through and upload a batch of files from a specified folder. To improve upload efficiency, the code sets a threshold of 100 MiB. Files smaller than 100 MiB are uploaded directly via the `putObjectFromFile` interface, while files equal to or larger than 100 MiB are uploaded using the `uploadFile` interface with resumable upload. 100MiB is provided as a reference value only; you may adjust it according to the client’s network bandwidth and other resource conditions.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

public class UploadFileWithDirectoryExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String uploadFileDirectory = "example_dir";

        long threshold = 100 * 1024 * 1024;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        List<String> fileList = getFileListFromPath(uploadFileDirectory);
        if (fileList == null || fileList.size() == 0) {
            System.out.println("uploadFile done, there are no files under " + uploadFileDirectory);
            return;
        }

        for (String file : fileList) {
            if (new File(file).length() >= threshold) {
                uploadLargeFile(tos, bucketName, file);
            } else {
                uploadSmallFile(tos, bucketName, file);
            }
        }
    }

    private static void uploadSmallFile(TOSV2 tos, String bucketName, String file) {
        try {
            PutObjectFromFileInput putObjectInput = new PutObjectFromFileInput().setBucket(bucketName).setKey(file).setFilePath(file);
            PutObjectFromFileOutput output = tos.putObjectFromFile(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("putObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static void uploadLargeFile(TOSV2 tos, String bucketName, String file) {
        int taskNum = 5;
        long partSize = 20 * 1024 * 1024;
        boolean enableCheckpoint = true;
        String checkpointFilePath = "the checkpoint file path";
        try{
            UploadFileV2Input input = new UploadFileV2Input().setBucket(bucketName).setKey(file)
                    .setFilePath(file).setEnableCheckpoint(enableCheckpoint)
                    .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
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

    private static List<String> getFileListFromPath(String filePath) {
        List<String> fileList = new ArrayList<>();
        File file = new File(filePath);
        if (!file.exists()) {
            return fileList;
        }
        File[] files = file.listFiles();
        if (files == null || files.length == 0) {
            return fileList;
        }
        for (File f : files) {
            if (f.isDirectory()) {
                fileList.addAll(getFileListFromPath(f.getPath()));
            } else {
                fileList.add(f.getPath());
            }
        }
        return fileList;
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For API documentation on uploading objects, see [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).
