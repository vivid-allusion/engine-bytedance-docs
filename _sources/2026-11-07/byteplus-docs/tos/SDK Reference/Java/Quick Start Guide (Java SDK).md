---
title: "Quick Start Guide (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-java-sdk"
---

This article describes how to quickly use the TOS Java SDK to perform common operations, including general client examples, creating buckets, uploading objects, downloading objects, listing objects, and deleting objects.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Install the SDK](https://docs.byteplus.com/docs/tos/Install-java-sdk)

2. [Initialize Client](https://docs.byteplus.com/docs/tos/Initialize-client-side-java-sdk)


<span id=".5a6i5oi356uv6YCa55So56S65L6L"></span>
## General Client Example

The following code provides a general template for using the TOS Java SDK, using object upload as an example.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.ByteArrayInputStream;

public class TOSV2ClientBasicExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        try{
            String data = "1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'";
            ByteArrayInputStream stream = new ByteArrayInputStream(data.getBytes());
            PutObjectInput putObjectInput = new PutObjectInput().setBucket(bucketName).setKey(objectKey).setContent(stream);
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


<span id=".5Yib5bu65qG2"></span>
## Create Bucket

A bucket (bucket) in TOS serves as a globally unique namespace, functioning as a data container for storing object data. The following code demonstrates how to create a new bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For constraints and restrictions on bucket names, see <a href="https://docs.byteplus.com/docs/tos/docs-common-concepts">Common Concepts</a>.</div>


```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.CreateBucketV2Input;
import com.volcengine.tos.model.bucket.CreateBucketV2Output;

public class CreateBucketBasicExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            CreateBucketV2Input input = new CreateBucketV2Input().setBucket(bucketName);
            CreateBucketV2Output output = tos.createBucket(input);
            System.out.println("bucket created: " + output.getLocation());
        } catch (TosClientException e) {
            System.out.println("createBucket failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("createBucket failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("createBucket failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about creating buckets, see <a href="https://docs.byteplus.com/docs/tos/Create-bucket-java-sdk">Creating Buckets</a>.</div>


<span id=".5LiK5Lyg5a-56LGh"></span>
## Uploads an object.

After the bucket is created successfully, objects can be uploaded to the bucket. The following code demonstrates how to upload an object to an existing bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.ByteArrayInputStream;

public class PutObjectBasicExample {
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
            PutObjectInput putObjectInput = new PutObjectInput().setBucket(bucketName).setKey(objectKey).setContent(stream);
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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you wish to upload an object to a specific folder (a logical concept in object storage), you can add to the object name with<code>/</code>Object names can include multi\-level folder paths as suffixes. For example, <code>folder1/folder2/objectName</code> means that <code>objectName</code> will be uploaded into the <code>folder1</code> folder, inside the <code>folder2</code> subfolder.</div>


* <div data-tips="true" data-tips-type="tip">When uploading an object to a folder, the folder is only a logical concept in object storage; as a result, no actual folder is created on the object storage server.</div>


* <div data-tips="true" data-tips-type="tip">When downloading an object, you must use the full path with the appropriate prefix. For example, the object name to be provided during download should also be <code>folder1/folder2/objectName</code>.</div>


* <div data-tips="true" data-tips-type="tip">For additional example links on uploading objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-upload-java-sdk">Uploading Objects</a>.</div>



<span id=".5LiL6L295a-56LGh"></span>
## Download Object

The following code demonstrates how to download an existing object from a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.FileOutputStream;
import java.io.IOException;

public class GetObjectBasicExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";
        String objectKey = "the object key name";
        String filePath = "the file path to download";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey);
            try(FileOutputStream fileOutputStream = new FileOutputStream(filePath);
                GetObjectV2Output output = tos.getObject(input)) {
                byte[] buffer = new byte[1024];
                int length;
                while ((length = output.getContent().read(buffer)) != -1) {
                    fileOutputStream.write(buffer, 0, length);
                }
            } catch (IOException e) {
                System.out.println("write data to file failed");
                e.printStackTrace();
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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional example links related to download objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-download-java-sdk">Download Objects</a>.</div>


<span id=".5YiX5Li-5a-56LGh"></span>
## Enumeration of Objects

The following code demonstrates how to enumerate the objects that have been uploaded from a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectsBasicExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListObjectsType2Input input = new ListObjectsType2Input().setBucket(bucketName);
            ListObjectsType2Output output = tos.listObjectsType2(input);
            System.out.printf("listObjectsType2 succeed, is truncated? %b, next continuation token is %s.\n",
                    output.isTruncated(), output.getNextContinuationToken());
            if (output.getContents() != null) {
                for (int i = 0; i < output.getContents().size(); i++) {
                    ListedObjectV2 object = output.getContents().get(i);
                    System.out.printf("Listed object, key is %s, size is %d, storageClass is %s, ETag is %s, " +
                                    "last modified is %s, crc64 value is %s.\n", object.getKey(), object.getSize(),
                            object.getStorageClass(), object.getEtag(), object.getLastModified().toString(), object.getHashCrc64ecma());
                }
            }
            if (output.getCommonPrefixes() != null) {
                for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                    ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                    System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                }
            }
            if (output.isTruncated()) {
                input.setContinuationToken(output.getNextContinuationToken());
                output = tos.listObjectsType2(input);
                System.out.printf("listObjectsType2 succeed, is truncated? %b, next continuation token is %s.\n",
                        output.isTruncated(), output.getNextContinuationToken());
                if (output.getContents() != null) {
                    for (int i = 0; i < output.getContents().size(); i++) {
                        ListedObjectV2 object = output.getContents().get(i);
                        System.out.printf("Listed object, key is %s, size is %d, storageClass is %s, ETag is %s, " +
                                        "last modified is %s, crc64 value is %s.\n", object.getKey(), object.getSize(),
                                object.getStorageClass(), object.getEtag(), object.getLastModified().toString(), object.getHashCrc64ecma());
                    }
                }
                if (output.getCommonPrefixes() != null) {
                    for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                        ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                        System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                    }
                }
            }
        } catch (TosClientException e) {
            System.out.println("listObjectsType2 failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjectsType2 failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjectsType2 failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional example links for object listing, please refer to <a href="https://docs.byteplus.com/docs/tos/List-objects-java-sdk">Object Listing</a>.</div>


<span id=".5Yig6Zmk5a-56LGh"></span>
## When you delete an object

The following code demonstrates how to delete an existing object from a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.DeleteObjectInput;
import com.volcengine.tos.model.object.DeleteObjectOutput;

public class DeleteObjectBasicExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";
        String objectKey = "the object key name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteObjectInput input = new DeleteObjectInput().setBucket(bucketName).setKey(objectKey);
            DeleteObjectOutput output = tos.deleteObject(input);
            System.out.println("deleteObject succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example links, including those about downloading objects, see <a href="https://docs.byteplus.com/docs/tos/Delete-object-java-sdk">Delete Object</a>.</div>
