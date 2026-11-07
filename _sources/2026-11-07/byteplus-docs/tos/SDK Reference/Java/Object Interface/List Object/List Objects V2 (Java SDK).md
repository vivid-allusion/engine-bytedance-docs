---
title: "List Objects V2 (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-v2-java-sdk"
---

This article describes how to use the TOS Java SDK's `listObjectsType2` interface to easily list objects in a specified bucket, list all objects, list objects with a specified prefix, list objects and subdirectories under a specified directory, etc.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**

To list objects, your account must have the `tos:ListBucket` permission. For specific instructions, refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

`listObjectsType2` interface supports the following parameters.


|**Parameter** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used to group object names. |
|startAfter |The starting point for the objects enumerated in this instance. |
|continuationToken |The specified enumeration operation must begin from this token. It can be obtained from the nextContinuationToken in the results listed previously. |
|maxKeys |Returns the maximum number of enumerated objects. A maximum of 1,000 results can be returned per request; if not specified, the default is 1,000 results. |
|encodingType |Encode the returned content and specify the encoding type. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Brief Enumeration**

The following code demonstrates how to list up to 10 objects in the bucket 'bucket\-example'.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectsType2BasicExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListObjectsType2Input input = new ListObjectsType2Input()
                    .setBucket(bucketName).setMaxKeys(maxKeys);
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


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paginated Listing**

The following code demonstrates how to paginate the listing of objects in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.ListObjectsType2Input;
import com.volcengine.tos.model.object.ListObjectsType2Output;
import com.volcengine.tos.model.object.ListedCommonPrefix;
import com.volcengine.tos.model.object.ListedObjectV2;

public class ListObjectsType2ByPageExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListObjectsType2Input input = new ListObjectsType2Input()
                    .setBucket(bucketName).setMaxKeys(maxKeys);
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
                    if (output.getCommonPrefixes() != null) {
                        for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                            ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                            System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                        }
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


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with the specified prefix**

The following code demonstrates how to list all objects with a specified prefix in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.ListObjectsType2Input;
import com.volcengine.tos.model.object.ListObjectsType2Output;
import com.volcengine.tos.model.object.ListedCommonPrefix;
import com.volcengine.tos.model.object.ListedObjectV2;

public class ListObjectsType2ByPrefixExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;
        String prefix = "example_dir/";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            boolean isTruncated = true;
            String continuationToken = null;
            while (isTruncated) {
                ListObjectsType2Input input = new ListObjectsType2Input().setBucket(bucketName)
                        .setMaxKeys(maxKeys).setPrefix(prefix).setContinuationToken(continuationToken);
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


<span id=".5YiX5Li-5qG25YaF5omA5pyJ5a-56LGh"></span>
### **List all objects in the bucket**

The following code demonstrates how to list all objects in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectsType2AllObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            boolean isTruncated = true;
            String continuationToken = null;
            while (isTruncated) {
                ListObjectsType2Input input = new ListObjectsType2Input().setBucket(bucketName).setMaxKeys(maxKeys)
                        .setContinuationToken(continuationToken);
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


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### **List the files and subdirectories in the specified directory.** 

TOS only supports the concept of objects; it is possible to create an object with a size of zero and a slash in its name.`/`The object at the end simulates the functionality of a directory.

The functionality of a directory can be simulated using the two parameters `Delimiter` and `Prefix`:


* First, set `Delimiter` to`/`Additionally, when `Prefix` is set to empty, information about objects and subdirectories in the root directory can be returned.

* When setting `Delimiter` to`/`When `Prefix` is set as a subdirectory (`commonPrefixes`), objects and subdirectories within that subdirectory can be returned.


The following code demonstrates how to list the objects and subdirectories in the root directory of the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.ListObjectsType2Input;
import com.volcengine.tos.model.object.ListObjectsType2Output;
import com.volcengine.tos.model.object.ListedCommonPrefix;
import com.volcengine.tos.model.object.ListedObjectV2;

public class ListObjectsType2ByDelimiterExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;
        String delimiter = "/";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            boolean isTruncated = true;
            String continuationToken = null;
            while (isTruncated) {
                ListObjectsType2Input input = new ListObjectsType2Input().setBucket(bucketName)
                        .setMaxKeys(maxKeys).setDelimiter(delimiter).setContinuationToken(continuationToken);
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
