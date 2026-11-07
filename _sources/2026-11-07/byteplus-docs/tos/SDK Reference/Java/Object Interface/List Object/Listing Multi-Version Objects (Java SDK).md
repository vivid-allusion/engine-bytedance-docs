---
title: "Listing Multi-Version Objects (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multiversion-objects-java-sdk"
---

The `listObjectVersions` interface of the TOS Java SDK is used to list multi\-version objects in a bucket. This article describes how to use the `listObjectVersions` API to simply list multi\-version objects in a specified bucket, list all multi\-version objects, list multi\-version objects with a specified prefix, list multi\-version objects and subdirectories within a specified directory, etc.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**

To list multi\-version objects, your account must have the `tos:ListBucketVersions` permission. For detailed instructions, please refer to [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

The parameters supported by the `listObjectVersions` API are as follows.


|**Parameter** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used to group object names. |
|keyMarker |The starting point for the enumeration of objects in this instance. Initially set to null; subsequently, it may take the value of nextKeyMarker returned by the previous request. |
|versionIDMarker |Use in conjunction with keyMarker. Initially set to null; subsequently, it may take the value of nextVersionIDMarker returned by the previous request. |
|maxKeys |Returns the maximum number of enumerated objects. A maximum of 1,000 results can be returned per request; if not specified, the default is 1,000 results. |
|encodingType |Encode the returned content and specify the encoding type. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Brief Enumeration**

The following code demonstrates how to list up to 10 multi\-version objects in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectVersionsBasicExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListObjectVersionsV2Input input = new ListObjectVersionsV2Input().setBucket(bucketName)
                    .setMaxKeys(maxKeys);
            ListObjectVersionsV2Output output = tos.listObjectVersions(input);
            System.out.printf("listObjectVersions succeed, is truncated? %b, next key marker is %s, " + 
                            "next version id marker is %s.\n", output.isTruncated(), 
                    output.getNextKeyMarker(), output.getNextVersionIDMarker());
            if (output.getVersions() != null) {
                for (int i = 0; i < output.getVersions().size(); i++) {
                    ListedObjectVersion object = output.getVersions().get(i);
                    System.out.printf("Listed object version, key is %s, size is %d, versionId is %s, " + 
                                        "storageClass is %s, ETag is %s, last modified is %s, isLatest? %b.\n", 
                                object.getKey(), object.getSize(), object.getVersionID(), object.getStorageClass(), 
                                object.getEtag(), object.getLastModified(), object.isLatest());
                }
            }
            if (output.getCommonPrefixes() != null) {
                for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                    ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                    System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                }
            }
            if (output.getDeleteMarkers() != null) {
                for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                    ListedDeleteMarkerEntry deleteMarker = output.getDeleteMarkers().get(i);
                    System.out.printf("Listed deleteMarker is %s\n", deleteMarker);
                }
            }
        } catch (TosClientException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjectVersions failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paginated Listing**

The following code demonstrates how to paginate the listing of multi\-version objects in the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectVersionsByPageExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListObjectVersionsV2Input input = new ListObjectVersionsV2Input().setBucket(bucketName)
                    .setMaxKeys(maxKeys);
            ListObjectVersionsV2Output output = tos.listObjectVersions(input);
            System.out.printf("listObjectVersions succeed, is truncated? %b, next key marker is %s, " +
                            "next version id marker is %s.\n", output.isTruncated(),
                    output.getNextKeyMarker(), output.getNextVersionIDMarker());
            if (output.getVersions() != null) {
                for (int i = 0; i < output.getVersions().size(); i++) {
                    ListedObjectVersion object = output.getVersions().get(i);
                    System.out.printf("Listed object version, key is %s, size is %d, versionId is %s, " + 
                                        "storageClass is %s, ETag is %s, last modified is %s, isLatest? %b.\n", 
                                object.getKey(), object.getSize(), object.getVersionID(), object.getStorageClass(), 
                                object.getEtag(), object.getLastModified(), object.isLatest());
                }
            }
            if (output.getCommonPrefixes() != null) {
                for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                    ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                    System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                }
            }
            if (output.getDeleteMarkers() != null) {
                for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                    ListedDeleteMarkerEntry deleteMarker = output.getDeleteMarkers().get(i);
                    System.out.printf("Listed deleteMarker is %s\n", deleteMarker);
                }
            }
            if (output.isTruncated()) {
                input.setKeyMarker(output.getNextKeyMarker()).setVersionIDMarker(output.getNextVersionIDMarker());
                output = tos.listObjectVersions(input);
                System.out.printf("listObjectVersions succeed, is truncated? %b, next key marker is %s, " +
                                "next version id marker is %s.\n", output.isTruncated(),
                        output.getNextKeyMarker(), output.getNextVersionIDMarker());
                if (output.getVersions() != null) {
                    for (int i = 0; i < output.getVersions().size(); i++) {
                        ListedObjectVersion object = output.getVersions().get(i);
                        System.out.printf("Listed object version, key is %s, size is %d, versionId is %s, " + 
                                        "storageClass is %s, ETag is %s, last modified is %s, isLatest? %b.\n", 
                                object.getKey(), object.getSize(), object.getVersionID(), object.getStorageClass(), 
                                object.getEtag(), object.getLastModified(), object.isLatest());
                    }
                }
                if (output.getCommonPrefixes() != null) {
                    for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                        ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                        System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                    }
                }
                if (output.getDeleteMarkers() != null) {
                    for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                        ListedDeleteMarkerEntry deleteMarker = output.getDeleteMarkers().get(i);
                        System.out.printf("Listed deleteMarker is %s\n", deleteMarker);
                    }
                }
            }
        } catch (TosClientException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjectVersions failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5aSa54mI5pys5a-56LGh"></span>
### **List all multi\-version objects with the specified prefix**

The following code demonstrates how to list all multi\-version objects with the specified prefix in the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectVersionsByPrefixExample {
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
            String keyMarker = null;
            String versionIdMarker = null;
            while (isTruncated) {
                ListObjectVersionsV2Input input = new ListObjectVersionsV2Input().setBucket(bucketName)
                        .setMaxKeys(maxKeys).setPrefix(prefix).setKeyMarker(keyMarker).setVersionIDMarker(versionIdMarker);
                ListObjectVersionsV2Output output = tos.listObjectVersions(input);
                System.out.printf("listObjectVersions succeed, is truncated? %b, next key marker is %s, " +
                                "next version id marker is %s.\n", output.isTruncated(),
                        output.getNextKeyMarker(), output.getNextVersionIDMarker());
                if (output.getVersions() != null) {
                    for (int i = 0; i < output.getVersions().size(); i++) {
                        ListedObjectVersion object = output.getVersions().get(i);
                        System.out.printf("Listed object version, key is %s, size is %d, versionId is %s, " +
                                        "storageClass is %s, ETag is %s, last modified is %s, isLatest? %b.\n",
                                object.getKey(), object.getSize(), object.getVersionID(), object.getStorageClass(),
                                object.getEtag(), object.getLastModified(), object.isLatest());
                    }
                }
                if (output.getCommonPrefixes() != null) {
                    for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                        ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                        System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                    }
                }
                if (output.getDeleteMarkers() != null) {
                    for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                        ListedDeleteMarkerEntry deleteMarker = output.getDeleteMarkers().get(i);
                        System.out.printf("Listed deleteMarker is %s\n", deleteMarker);
                    }
                }
                isTruncated = output.isTruncated();
                keyMarker = output.getNextKeyMarker();
                versionIdMarker = output.getNextVersionIDMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjectVersions failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiX5Li-5qG25YaF5omA5pyJ5aSa54mI5pys5a-56LGh"></span>
### **List all multi\-version objects in the bucket**

The following code demonstrates how to list all versioned objects in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectVersionsAllObjectExample {
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
            String keyMarker = null;
            String versionIdMarker = null;
            while (isTruncated) {
                ListObjectVersionsV2Input input = new ListObjectVersionsV2Input().setBucket(bucketName)
                        .setMaxKeys(maxKeys).setKeyMarker(keyMarker).setVersionIDMarker(versionIdMarker);
                ListObjectVersionsV2Output output = tos.listObjectVersions(input);
                System.out.printf("listObjectVersions succeed, is truncated? %b, next key marker is %s, " +
                                "next version id marker is %s.\n", output.isTruncated(),
                        output.getNextKeyMarker(), output.getNextVersionIDMarker());
                if (output.getVersions() != null) {
                    for (int i = 0; i < output.getVersions().size(); i++) {
                        ListedObjectVersion object = output.getVersions().get(i);
                        System.out.printf("Listed object version, key is %s, size is %d, versionId is %s, " + 
                                        "storageClass is %s, ETag is %s, last modified is %s, isLatest? %b.\n", 
                                object.getKey(), object.getSize(), object.getVersionID(), object.getStorageClass(), 
                                object.getEtag(), object.getLastModified(), object.isLatest());
                    }
                }
                if (output.getCommonPrefixes() != null) {
                    for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                        ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                        System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                    }
                }
                if (output.getDeleteMarkers() != null) {
                    for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                        ListedDeleteMarkerEntry deleteMarker = output.getDeleteMarkers().get(i);
                        System.out.printf("Listed deleteMarker is %s\n", deleteMarker);
                    }
                }
                isTruncated = output.isTruncated();
                keyMarker = output.getNextKeyMarker();
                versionIdMarker = output.getNextVersionIDMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjectVersions failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5aSa54mI5pys5a-56LGh5ZKM5a2Q55uu5b2V"></span>
### **List multi\-version objects and subdirectories in the specified directory.** 

TOS defines only the concept of objects; it is possible to create an object with a size of zero and an object name ending with a slash.`/`An object at the end that simulates the functionality of a directory.

The functionality of a directory can be simulated using the `Delimiter` and `Prefix` parameters:


* First, set `Delimiter` to`/`Also, by setting `Prefix` to empty, you can return information about objects and subdirectories in the root directory.

* When setting `Delimiter` to`/`When you set `Prefix` to a subdirectory (commonPrefixes), the objects and subdirectories within that subdirectory can be returned.


The following code demonstrates how to list versioned objects and subdirectories in the root directory of the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListObjectVersionsByDelimiterExample {
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
            String keyMarker = null;
            String versionIdMarker = null;
            while (isTruncated) {
                ListObjectVersionsV2Input input = new ListObjectVersionsV2Input().setBucket(bucketName)
                        .setMaxKeys(maxKeys).setDelimiter(delimiter).setKeyMarker(keyMarker).setVersionIDMarker(versionIdMarker);
                ListObjectVersionsV2Output output = tos.listObjectVersions(input);
                System.out.printf("listObjectVersions succeed, is truncated? %b, next key marker is %s, " +
                                "next version id marker is %s.\n", output.isTruncated(),
                        output.getNextKeyMarker(), output.getNextVersionIDMarker());
                if (output.getVersions() != null) {
                    for (int i = 0; i < output.getVersions().size(); i++) {
                        ListedObjectVersion object = output.getVersions().get(i);
                        System.out.printf("Listed object version, key is %s, size is %d, versionId is %s, " +
                                        "storageClass is %s, ETag is %s, last modified is %s, isLatest? %b.\n",
                                object.getKey(), object.getSize(), object.getVersionID(), object.getStorageClass(),
                                object.getEtag(), object.getLastModified(), object.isLatest());
                    }
                }
                if (output.getCommonPrefixes() != null) {
                    for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                        ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                        System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                        listCommonPrefix(bucketName, maxKeys, delimiter, commonPrefix.getPrefix(), tos);
                    }
                }
                if (output.getDeleteMarkers() != null) {
                    for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                        ListedDeleteMarkerEntry deleteMarker = output.getDeleteMarkers().get(i);
                        System.out.printf("Listed deleteMarker is %s\n", deleteMarker);
                    }
                }
                isTruncated = output.isTruncated();
                keyMarker = output.getNextKeyMarker();
                versionIdMarker = output.getNextVersionIDMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listObjectVersions failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listObjectVersions failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static void listCommonPrefix(String bucketName, int maxKeys, String delimiter, String prefix, TOSV2 tos) {
        boolean isTruncated = true;
        String keyMarker = null;
        String versionIdMarker = null;
        while (isTruncated) {
            ListObjectVersionsV2Input input = new ListObjectVersionsV2Input().setBucket(bucketName).setMaxKeys(maxKeys)
                    .setDelimiter(delimiter).setKeyMarker(keyMarker).setVersionIDMarker(versionIdMarker).setPrefix(prefix);
            ListObjectVersionsV2Output output = tos.listObjectVersions(input);
            System.out.printf("listObjectVersions succeed, is truncated? %b, next key marker is %s, " +
                            "next version id marker is %s.\n", output.isTruncated(),
                    output.getNextKeyMarker(), output.getNextVersionIDMarker());
            if (output.getVersions() != null) {
                for (int i = 0; i < output.getVersions().size(); i++) {
                    ListedObjectVersion object = output.getVersions().get(i);
                    System.out.printf("Listed object version, key is %s, size is %d, versionId is %s, " +
                                    "storageClass is %s, ETag is %s, last modified is %s, isLatest? %b.\n",
                            object.getKey(), object.getSize(), object.getVersionID(), object.getStorageClass(),
                            object.getEtag(), object.getLastModified(), object.isLatest());
                }
            }
            if (output.getCommonPrefixes() != null) {
                for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                    ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                    System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                }
            }
            if (output.getDeleteMarkers() != null) {
                for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                    ListedDeleteMarkerEntry deleteMarker = output.getDeleteMarkers().get(i);
                    System.out.printf("Listed deleteMarker is %s\n", deleteMarker);
                }
            }
            isTruncated = output.isTruncated();
            keyMarker = output.getNextKeyMarker();
            versionIdMarker = output.getNextVersionIDMarker();
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For API documentation on listing multi\-version objects, refer to [ListObjectsVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
