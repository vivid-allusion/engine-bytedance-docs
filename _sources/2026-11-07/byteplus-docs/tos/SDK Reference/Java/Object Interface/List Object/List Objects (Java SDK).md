---
title: "List Objects (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-java-sdk"
---

This article describes how to use the TOS Java SDK `listObjects` interface to easily list objects in a specified bucket, list all objects, list objects with a specified prefix, list objects and subdirectories under a specified directory, etc.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* Before listing objects, your account must have the `tos:ListBucket` permission. For details on how to proceed, refer to the [IAM policy overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

* The current TOS now supports the new `listObjectsType2` interface, whose usage is largely consistent with that of the `listObjects` interface. It is strongly recommended that you use the `listObjectsType2` interface to achieve higher listing efficiency. For detailed usage methods, please refer to [List Objects V2 (Java SDK)](https://docs.byteplus.com/docs/tos/List-objects-v2-java-sdk).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

The parameters supported by the `listObjects` interface are as follows.


|**Parameter** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used to group object names. |
|marker |The starting point for the listing of objects in this instance. Initially set to null; subsequently, it may take the value of nextMarker returned by the previous request. |
|maxKeys |Returns the maximum number of objects to be enumerated. A maximum of 1,000 results can be returned per request; if not specified, the default is 1,000 results. |
|encodingType |Encode the returned content and specify the encoding type. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Simple listing**

The following code demonstrates how to list up to 10 objects in the `bucket-example` bucket.

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

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListObjectsV2Input input = new ListObjectsV2Input()
                    .setBucket(bucketName).setMaxKeys(maxKeys);
            ListObjectsV2Output output = tos.listObjects(input);
            System.out.printf("listObjects succeed, is truncated? %b, next marker is %s.\n",
                    output.isTruncated(), output.getNextMarker());
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
            System.out.println("listObjects failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjects failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjects failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paginated listing**

The following code demonstrates how to list objects by page in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectsByPageExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListObjectsV2Input input = new ListObjectsV2Input()
                    .setBucket(bucketName).setMaxKeys(maxKeys);
            ListObjectsV2Output output = tos.listObjects(input);
            System.out.printf("listObjects succeed, is truncated? %b, next marker is %s.\n",
                    output.isTruncated(), output.getNextMarker());
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
                input.setMarker(output.getNextMarker());
                output = tos.listObjects(input);
                System.out.printf("listObjects succeed, is truncated? %b, next marker is %s.\n",
                        output.isTruncated(), output.getNextMarker());
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
            System.out.println("listObjects failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjects failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjects failed");
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
import com.volcengine.tos.model.object.*;

public class ListObjectsByPrefixExample {
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
            String marker = null;
            while (isTruncated) {
                ListObjectsV2Input input = new ListObjectsV2Input().setBucket(bucketName)
                        .setMaxKeys(maxKeys).setPrefix(prefix).setMarker(marker);
                ListObjectsV2Output output = tos.listObjects(input);
                System.out.printf("listObjects succeed, is truncated? %b, next marker is %s.\n",
                        output.isTruncated(), output.getNextMarker());
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
                marker = output.getNextMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listObjects failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjects failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjects failed");
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

public class ListObjectsAllObjectExample {
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
            String marker = null;
            while (isTruncated) {
                ListObjectsV2Input input = new ListObjectsV2Input().setBucket(bucketName)
                        .setMaxKeys(maxKeys).setMarker(marker);
                ListObjectsV2Output output = tos.listObjects(input);
                System.out.printf("listObjects succeed, is truncated? %b, next marker is %s.\n",
                        output.isTruncated(), output.getNextMarker());
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
                marker = output.getNextMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listObjects failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjects failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjects failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### **List objects and subdirectories in the specified directory**

TOS only supports the concept of objects. To simulate directory functionality, create a zero\-byte object that ends with a forward slash (`/`).

You can simulate directory functionality using the two parameters `Delimiter` and `Prefix`:


* First, set `Delimiter` to `/`. By setting `Prefix` to empty, you can retrieve information about objects and subdirectories in the root directory.

* When `Delimiter` is `/`, by setting `Prefix` as a subdirectory (`commonPrefixes`), both the objects in the subdirectory and its subdirectories can be returned.


The following code demonstrates how to list the objects and subdirectories in the root directory of the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectsByDelimiterExample {
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
            String marker = null;
            while (isTruncated) {
                ListObjectsV2Input input = new ListObjectsV2Input().setBucket(bucketName)
                        .setMaxKeys(maxKeys).setDelimiter(delimiter).setMarker(marker);
                ListObjectsV2Output output = tos.listObjects(input);
                System.out.printf("listObjects succeed, is truncated? %b, next marker is %s.\n",
                        output.isTruncated(), output.getNextMarker());
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
                marker = output.getNextMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listObjects failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjects failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjects failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static void listCommonPrefix(String bucketName, int maxKeys, String delimiter, String prefix, TOSV2 tos) {
        boolean isTruncated = true;
        String marker = null;
        while (isTruncated) {
            ListObjectsV2Input input = new ListObjectsV2Input().setBucket(bucketName).setMaxKeys(maxKeys)
                    .setDelimiter(delimiter).setMarker(marker).setPrefix(prefix);
            ListObjectsV2Output output = tos.listObjects(input);
            System.out.printf("listObjects succeed, is truncated? %b, next marker is %s.\n",
                    output.isTruncated(), output.getNextMarker());
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
            marker = output.getNextMarker();
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For documentation on the API for listing objects, refer to [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects).
