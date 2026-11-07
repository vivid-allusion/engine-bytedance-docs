---
title: "Multipart Upload (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-upload-java-sdk"
---

If you need to upload a large object, it is recommended to divide it into multiple parts and upload each part separately. Finally, invoke the merge parts operation to combine the uploaded parts into a single object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* Before initiating multipart upload, you must have the `tos:PutObject` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Before canceling a multipart upload task, you must have the `tos:AbortMultipartUpload` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Shard numbers start from 1, with a maximum value of 10,000. Except for the last fragment, the minimum size of all other fragments is 4 MiB.

* When uploading an object, the object name must comply with specific requirements. For more information, see [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale data storage. Its internal partitions store object index data. To horizontally scale the maximum throughput for uploading and downloading objects, and to reduce the probability of hotspot partitions, please avoid using object names that increase in lexicographical order. For more details, refer to [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.


<span id=".5YiG54mH5LiK5Lyg5q2l6aqk"></span>
## Chunked Upload Procedure

Multipart upload using the TOS Java SDK consists of the following three steps.


1. Initialize the multipart upload task: call `createMultipartUpload` API returns the globally unique `uploadId` created by TOS.

2. Call the `uploadPart` API to upload part data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the same multipart upload task (identified by <code>uploadId</code>), the part number (<code>partNumber</code>) specifies the relative position of the part within the entire object. If data is uploaded multiple times using the same shard number, TOS will overwrite the existing data, and only the most recent upload will be retained.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>uploadPart</code> API returns the MD5 value of the part data, which can be obtained through the ETag field. When merging parts, you must specify all part information (part number and ETag value) that has already been uploaded in the current multipart upload task.   </div>
   

3. Completing multipart upload: After all parts have been uploaded, call the `completeMultipartUpload` API to merge all parts into a single object.


<span id=".5YiG54mH5LiK5Lyg5a6M5pW06L-H56iL"></span>
## **The Complete Process of Multipart Upload**

The following code demonstrates three methods for uploading a local file in parts to the example_object.txt file located in the example_dir directory of the target bucket bucket\-example using the Java SDK.


1. Encapsulate the local file as a FileInputStream for multipart upload.


```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.io.TosRepeatableBoundedFileInputStream;
import com.volcengine.tos.model.object.*;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.*;

public class MultipartUploadWithFileInputStreamFullExample {
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
            String uploadId = null;
            CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);

            CreateMultipartUploadOutput createOutput = tos.createMultipartUpload(create);
            System.out.println("createMultipartUpload succeed, uploadId is " + createOutput.getUploadID());

            uploadId = createOutput.getUploadID();

            long partSize = 5 * 1024 * 1024;

            List<UploadedPartV2> uploadedParts = new ArrayList<>();

            long fileSize = new File(filePath).length();
            long offset = 0;
            for (int i = 1; offset < fileSize; ++i) {
                try(FileInputStream content = new FileInputStream(filePath);){
                    content.skip(offset);
                    InputStream wrappedContent = new TosRepeatableBoundedFileInputStream(content, partSize);
                    int partNumber = i;
                    if (fileSize-offset < partSize) {
                        partSize = fileSize-offset;
                    }
                    UploadPartV2Input input = new UploadPartV2Input().setBucket(bucketName)
                            .setKey(objectKey).setUploadID(uploadId).setPartNumber(partNumber)
                            .setContentLength(partSize).setContent(wrappedContent);
                    UploadPartV2Output output = tos.uploadPart(input);
                    uploadedParts.add(new UploadedPartV2().setPartNumber(i).setEtag(output.getEtag()));
                    System.out.printf("uploadPart succeed, partNumber is %d, etag is %s, crc64 value is %s\n",
                            output.getPartNumber(), output.getEtag(), output.getHashCrc64ecma());

                    offset += partSize;
                } catch (IOException e) {
                    System.out.println("uploadPart read file failed");
                    e.printStackTrace();
                }
            }

            CompleteMultipartUploadV2Input complete = new CompleteMultipartUploadV2Input().setBucket(bucketName)
                    .setKey(objectKey).setUploadID(uploadId);
            complete.setUploadedParts(uploadedParts);
            CompleteMultipartUploadV2Output completedOutput = tos.completeMultipartUpload(complete);
            System.out.printf("completeMultipartUpload succeed, etag is %s, crc64 value is %s, location is %s.\n",
                    completedOutput.getEtag(), completedOutput.getHashCrc64ecma(), completedOutput.getLocation());
        } catch (TosClientException e) {
            System.out.println("uploadPart failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("uploadPart failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("uploadPart failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```



2. Upload the local file in parts using the `uploadPartFromFile` interface. If the data to be uploaded is a local file, it is recommended to use this interface.


```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

import java.io.File;
import java.util.ArrayList;
import java.util.List;

public class MultipartUploadWithFileFullExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String filePath = "example_dir/example_file.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        String uploadId = null;
        try{
            CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);

            CreateMultipartUploadOutput createOutput = tos.createMultipartUpload(create);
            System.out.println("createMultipartUpload succeed, uploadId is " + createOutput.getUploadID());

            uploadId = createOutput.getUploadID();

            long partSize = 5 * 1024 * 1024;

            List<UploadedPartV2> uploadedParts = new ArrayList<>();

            long fileSize = new File(filePath).length();
            long offset = 0;
            for (int i = 1; offset < fileSize; ++i) {
                int partNumber = i;
                if (fileSize-offset < partSize) {
                    partSize = fileSize-offset;
                }
                UploadPartFromFileInput input = new UploadPartFromFileInput().setBucket(bucketName)
                        .setKey(objectKey).setUploadID(uploadId).setPartNumber(partNumber)
                        .setFilePath(filePath).setPartSize(partSize).setOffset(offset);
                UploadPartFromFileOutput output = tos.uploadPartFromFile(input);
                uploadedParts.add(new UploadedPartV2().setPartNumber(partNumber).setEtag(output.getEtag()));
                System.out.printf("uploadPart succeed, partNumber is %d, etag is %s, crc64 value is %s\n",
                        output.getPartNumber(), output.getEtag(),
                        output.getHashCrc64ecma());

                offset += partSize;
            }

            CompleteMultipartUploadV2Input complete = new CompleteMultipartUploadV2Input().setBucket(bucketName)
                    .setKey(objectKey).setUploadID(uploadId);
            complete.setUploadedParts(uploadedParts);
            CompleteMultipartUploadV2Output completedOutput = tos.completeMultipartUpload(complete);
            System.out.printf("completeMultipartUpload succeed, etag is %s, crc64 value is %s, location is %s.\n",
                    completedOutput.getEtag(), completedOutput.getHashCrc64ecma(), completedOutput.getLocation());
        } catch (TosClientException e) {
            System.out.println("multipart upload failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("multipart upload failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("multipart upload failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```



3. Upload the byte array as segments.


```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

import java.io.ByteArrayInputStream;
import java.io.InputStream;
import java.util.*;

public class MultipartUploadWithByteArrayInputStreamFullExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        String uploadId = null;
        try{
            CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);

            CreateMultipartUploadOutput createOutput = tos.createMultipartUpload(create);
            System.out.println("createMultipartUpload succeed, uploadId is " + createOutput.getUploadID());

            uploadId = createOutput.getUploadID();


            long partSize = 5 * 1024 * 1024;

            List<UploadedPartV2> uploadedParts = new ArrayList<>();


            for (int i = 1; i <= 3; ++i) {
                int partNumber = i;
                byte[] data = new byte[(int)partSize];
                Arrays.fill(data, (byte)'A');
                InputStream content = new ByteArrayInputStream(data);
                UploadPartV2Input input = new UploadPartV2Input().setBucket(bucketName)
                        .setKey(objectKey).setUploadID(uploadId).setPartNumber(partNumber)
                        .setContentLength(partSize).setContent(content);
                UploadPartV2Output output = tos.uploadPart(input);
                uploadedParts.add(new UploadedPartV2().setPartNumber(partNumber).setEtag(output.getEtag()));
                System.out.printf("uploadPart succeed, partNumber is %d, etag is %s, crc64 value is %s\n",
                        output.getPartNumber(), output.getEtag(), output.getHashCrc64ecma());
            }

            CompleteMultipartUploadV2Input complete = new CompleteMultipartUploadV2Input().setBucket(bucketName)
                    .setKey(objectKey).setUploadID(uploadId);
            complete.setUploadedParts(uploadedParts);
            CompleteMultipartUploadV2Output completedOutput = tos.completeMultipartUpload(complete);
            System.out.printf("completeMultipartUpload succeed, etag is %s, crc64 value is %s, location is %s.\n",
                    completedOutput.getEtag(), completedOutput.getHashCrc64ecma(), completedOutput.getLocation());
        } catch (TosClientException e) {
            System.out.println("multipart upload failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("multipart upload failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("multipart upload failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Y-W5raI5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
## **Cancel Multipart Upload Task**

You can use the `abortMultipartUpload` API to cancel a multipart upload task. After a multipart upload task is canceled, TOS will delete all uploaded part data, and you will no longer be able to perform any operations on this task.

The following code demonstrates how to cancel the multipart upload task for the `example_object.txt` object located in the `example_dir` directory of the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.AbortMultipartUploadInput;

public class AbortMultipartUploadExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String uploadId = "the specific uploadId";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            AbortMultipartUploadInput input = new AbortMultipartUploadInput().setBucket(bucketName)
                    .setKey(objectKey).setUploadID(uploadId);
            tos.abortMultipartUpload(input);
        } catch (TosClientException e) {
            System.out.println("abortMultipartUpload failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("abortMultipartUpload failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("abortMultipartUpload failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiX5Li-5bey5LiK5Lyg55qE5YiG54mH5L-h5oGv"></span>
## **List information on uploaded fragments**

You can use the SDK's `listParts` interface to list the parts that have already been uploaded under a specific `uploadId`.

The following code demonstrates how to list all uploaded parts of the `example_object.txt` object located in the `example_dir` directory within the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.ListPartsInput;
import com.volcengine.tos.model.object.ListPartsOutput;
import com.volcengine.tos.model.object.UploadedPartV2;

public class ListPartsExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String uploadId = "the specific uploadId";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            int maxParts = 1000;
            boolean isTruncated = true;
            int partNumberMarker = 0;
            int total = 0;
            while(isTruncated) {
                ListPartsInput input = new ListPartsInput().setBucket(bucketName).setKey(objectKey)
                        .setUploadID(uploadId).setPartNumberMarker(partNumberMarker).setMaxParts(maxParts);
                ListPartsOutput output = tos.listParts(input);
                System.out.printf("listParts succeed, is truncated? %b, next partNumber marker is %d \n",
                        output.isTruncated(), output.getNextPartNumberMarker());
                if (output.getUploadedParts() != null) {
                    for (int i = 0; i < output.getUploadedParts().size(); i++) {
                        UploadedPartV2 upload = output.getUploadedParts().get(i);
                        System.out.printf("Uploaded part, partNumber is %d, etag is %s, lastModified is %s, " +
                                "size is %d.\n", upload.getPartNumber(), upload.getEtag(), upload.getLastModified(), upload.getSize());
                    }
                    total += output.getUploadedParts().size();
                }
                isTruncated = output.isTruncated();
                partNumberMarker = output.getNextPartNumberMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listParts failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listParts failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listParts failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**


* For the API documentation on creating a multipart upload task, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on uploading parts, please refer to [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart).

* For documentation on the API for merging multipart uploads, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).

* For API documentation on aborting multipart upload tasks, refer to [AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload).
