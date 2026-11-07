---
title: "Directory Scenario (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/catalog-scenes-java-sdk"
---

TOS defines only the concept of objects and stores data internally using a flat structure. To facilitate the grouping of objects and simplify management, you can organize objects using a directory hierarchy.

<span id=".5Yib5bu655uu5b2V"></span>
## **Creating a Table of Contents**

TOS only has the concept of objects; it is possible to create an object with a size of zero and an object name starting with`/`The final object simulates the functionality of a directory.

The following code demonstrates how to create the directory `example_dir/` and the subdirectory `example_dir/aaa/` in the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

public class CreateDirExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String dir = "example_dir/";
        String dir1 = "example_dir/aaa/";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            PutObjectInput putObjectInput = new PutObjectInput().setBucket(bucketName).setKey(dir).setContent(null);
            PutObjectOutput output = tos.putObject(putObjectInput);
            System.out.println("putObject succeed, object's etag is " + output.getEtag());
            System.out.println("putObject succeed, object's crc64 is " + output.getHashCrc64ecma());

            putObjectInput = new PutObjectInput().setBucket(bucketName).setKey(dir1).setContent(null);
            output = tos.putObject(putObjectInput);
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


<span id=".5qih5ouf55uu5b2V5p-l6K-i"></span>
## **Simulated Directory Query**

You can simulate the functionality of a directory using the two parameters `Delimiter` and `Prefix`:


* First, set `Delimiter` to`/`By also setting `Prefix` to empty, the system can return information about objects and subdirectories in the root directory.

* When setting the `Delimiter` to`/`By simultaneously setting `Prefix` to the subdirectory `commonPrefixes`, you can return the objects and subdirectories within that subdirectory.


The following code demonstrates how to list the objects and subdirectories under the directory `example_dir/` in the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.ListObjectsType2Input;
import com.volcengine.tos.model.object.ListObjectsType2Output;
import com.volcengine.tos.model.object.ListedCommonPrefix;
import com.volcengine.tos.model.object.ListedObjectV2;

public class ListDirExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;
        String delimiter = "/";
        String prefix = "example_dir/";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            boolean isTruncated = true;
            String continuationToken = null;
            while (isTruncated) {
                ListObjectsType2Input input = new ListObjectsType2Input().setBucket(bucketName).setMaxKeys(maxKeys)
                        .setDelimiter(delimiter).setPrefix(prefix).setContinuationToken(continuationToken);
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
                        listCommonPrefix(bucketName, maxKeys, delimiter, commonPrefix.getPrefix(), tos);
                    }
                }
                isTruncated = output.isTruncated();
                continuationToken = output.getNextContinuationToken();
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
    
    private static void listCommonPrefix(String bucketName, int maxKeys, String delimiter, String prefix, TOSV2 tos) {
        boolean isTruncated = true;
        String continuationToken = null;
        while (isTruncated) {
            ListObjectsType2Input input = new ListObjectsType2Input().setBucket(bucketName).setMaxKeys(maxKeys)
                    .setDelimiter(delimiter).setContinuationToken(continuationToken).setPrefix(prefix);
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
            isTruncated = output.isTruncated();
            continuationToken = output.getNextContinuationToken();
        }
    }
}
```


<span id=".5Yig6Zmk55uu5b2V"></span>
## **Delete Directory**

The following code demonstrates how to delete all data in the `example_dir/` directory of the `bucket-example` bucket.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">In the following code, if the <code>prefix</code> parameter is not set (i.e., <code>prefix</code> is<code>null</code>Or, setting prefix = "" (an empty string) will delete all object data within the bucket. Please review and use this option with extreme caution.</div>


```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.DeleteObjectInput;
import com.volcengine.tos.model.object.ListObjectsType2Input;
import com.volcengine.tos.model.object.ListObjectsType2Output;

public class DeleteDirExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String prefix = "example_dir/";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            boolean isTruncated = true;
            String continuationToken = null;
            while (isTruncated) {
                ListObjectsType2Input input = new ListObjectsType2Input().setBucket(bucketName)
                        .setPrefix(prefix).setContinuationToken(continuationToken);
                ListObjectsType2Output output = tos.listObjectsType2(input);
                if (output.getContents() != null){
                    for (int i = 0; i < output.getContents().size(); i++) {
                        String objectKey = output.getContents().get(i).getKey();
                        DeleteObjectInput deleteInput = new DeleteObjectInput().setBucket(bucketName)
                                .setKey(output.getContents().get(i).getKey());
                        tos.deleteObject(deleteInput);
                        System.out.println("deleteObject succeed, deleted key is " + objectKey);
                    }
                }
                isTruncated = output.isTruncated();
                continuationToken = output.getNextContinuationToken();
            }

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
