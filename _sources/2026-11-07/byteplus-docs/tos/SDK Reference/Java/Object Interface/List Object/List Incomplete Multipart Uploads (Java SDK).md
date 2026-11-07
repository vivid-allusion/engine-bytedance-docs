---
title: "List Incomplete Multipart Uploads (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-unmerged-objects-java-sdk"
---

The `listMultipartUploads` interface of the TOS Java SDK is used to list incomplete multipart uploads within a bucket. This article describes how to use the `listMultipartUploads` API to simply list incomplete multipart uploads in a specified bucket, list all incomplete multipart uploads, list incomplete multipart uploads with a specified prefix, and list incomplete multipart uploads within a specified directory, etc.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* To list multipart uploads, you must have the `tos:ListBucketMultipartUploads` permission for the bucket. For detailed instructions, refer to [IAM policy overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

* This listing method pertains to incomplete multipart uploads for which the parts have not yet been merged. If the parts of a multipart upload have already been merged, it will no longer be listed.


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

The parameters supported by the `listMultipartUploads` API are as follows.


|**Parameter** |**Description** |
|---|---|
|prefix |The object name prefix for the current query result. |
|delimiter |Character used to group object names. |
|keyMarker |The starting point for the listing of objects in this instance. Initially set to null; subsequently, it may take the value of nextKeyMarker returned by the previous request. |
|uploadIDMarker |Use in conjunction with keyMarker. Initially set to null; subsequently, it may take the value of nextUploadIDMarker returned by the previous request. |
|maxUploads |Returns the maximum number of multipart uploads that can be listed. A maximum of 1,000 results can be returned per request; if not specified, the default is 1,000 results. |
|encodingType |Encode the returned content and specify the type of encoding.<br><br>Default value: None |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Simple listing**

The following code demonstrates how to list up to 10 incomplete multipart uploads in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListMultipartUploadsBasicExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input().setBucket(bucketName)
                    .setMaxUploads(maxKeys);
            ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
            System.out.printf("listMultipartUploads succeed, is truncated? %b, next uploadIDMarker is %s, " +
                    "next keyMarker is %s.\n", output.isTruncated(), output.getNextUploadIdMarker(), output.getNextKeyMarker());
            if (output.getUploads() != null) {
                for (int i = 0; i < output.getUploads().size(); i++) {
                    ListedUpload upload = output.getUploads().get(i);
                    System.out.printf("Listed upload, key is %s, uploadId is %s, storageClass is %s\n", 
                            upload.getKey(), upload.getUploadID(), upload.getStorageClass().getStorageClass());
                }
            }
            if (output.getCommonPrefixes() != null) {
                for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                    ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                    System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                }
            }
        } catch (TosClientException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listMultipartUploads failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paginated listing**

The following code demonstrates how to list incomplete multipart uploads by page in the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListMultipartUploadsByPageExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        int maxKeys = 10;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        try{
            ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input().setBucket(bucketName)
                    .setMaxUploads(maxKeys);
            ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
            System.out.printf("listMultipartUploads succeed, is truncated? %b, next uploadIDMarker is %s, " +
                    "next keyMarker is %s.\n", output.isTruncated(), output.getNextUploadIdMarker(), output.getNextKeyMarker());
            if (output.getUploads() != null) {
                for (int i = 0; i < output.getUploads().size(); i++) {
                    ListedUpload upload = output.getUploads().get(i);
                    System.out.printf("Listed upload, key is %s, uploadId is %s, storageClass is %s\n", 
                            upload.getKey(), upload.getUploadID(), upload.getStorageClass().getStorageClass());
                }
            }
            if (output.getCommonPrefixes() != null) {
                for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                    ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                    System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                }
            }
            if (output.isTruncated()) {
                input.setKeyMarker(output.getNextKeyMarker()).setUploadIDMarker(output.getNextUploadIdMarker());
                output = tos.listMultipartUploads(input);
                System.out.printf("listMultipartUploads succeed, is truncated? %b, next uploadIDMarker is %s, " +
                        "next keyMarker is %s.\n", output.isTruncated(), output.getNextUploadIdMarker(), output.getNextKeyMarker());
                if (output.getUploads() != null) {
                    for (int i = 0; i < output.getUploads().size(); i++) {
                        ListedUpload upload = output.getUploads().get(i);
                        System.out.printf("Listed upload, key is %s, uploadId is %s, storageClass is %s\n", 
                            upload.getKey(), upload.getUploadID(), upload.getStorageClass().getStorageClass());
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
            System.out.println("listMultipartUploads failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listMultipartUploads failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5YiG54mH5Lu75Yqh"></span>
### **List all multipart uploads with the specified prefix**

The following code demonstrates how to list all incomplete multipart uploads with a specified prefix in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListMultipartUploadsByPrefixExample {
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
            String uploadIdMarker = null;
            while (isTruncated) {
                ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input().setBucket(bucketName)
                        .setMaxUploads(maxKeys).setPrefix(prefix).setKeyMarker(keyMarker).setUploadIDMarker(uploadIdMarker);
                ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
                System.out.printf("listMultipartUploads succeed, is truncated? %b, next uploadIDMarker is %s, " +
                        "next keyMarker is %s.\n", output.isTruncated(), output.getNextUploadIdMarker(), output.getNextKeyMarker());
                if (output.getUploads() != null) {
                    for (int i = 0; i < output.getUploads().size(); i++) {
                        ListedUpload upload = output.getUploads().get(i);
                        System.out.printf("Listed upload, key is %s, uploadId is %s, storageClass is %s\n",
                                upload.getKey(), upload.getUploadID(), upload.getStorageClass().getStorageClass());
                    }
                }
                if (output.getCommonPrefixes() != null) {
                    for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                        ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                        System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                    }
                }
                isTruncated = output.isTruncated();
                keyMarker = output.getNextKeyMarker();
                uploadIdMarker = output.getNextUploadIdMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listMultipartUploads failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiX5Li-5qG25YaF5omA5pyJ5YiG54mH5Lu75Yqh"></span>
### **List all multipart uploads within the bucket**

The following code demonstrates how to list all incomplete multipart uploads in the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListMultipartUploadsAllObjectExample {
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
            String uploadIdMarker = null;
            while (isTruncated) {
                ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input().setBucket(bucketName)
                        .setMaxUploads(maxKeys).setKeyMarker(keyMarker).setUploadIDMarker(uploadIdMarker);
                ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
                System.out.printf("listMultipartUploads succeed, is truncated? %b, next uploadIDMarker is %s, " +
                        "next keyMarker is %s.\n", output.isTruncated(), output.getNextUploadIdMarker(), output.getNextKeyMarker());
                if (output.getUploads() != null) {
                    for (int i = 0; i < output.getUploads().size(); i++) {
                        ListedUpload upload = output.getUploads().get(i);
                        System.out.printf("Listed upload, key is %s, uploadId is %s, storageClass is %s\n", 
                            upload.getKey(), upload.getUploadID(), upload.getStorageClass().getStorageClass());
                    }
                }
                if (output.getCommonPrefixes() != null) {
                    for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                        ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                        System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                    }
                }
                isTruncated = output.isTruncated();
                keyMarker = output.getNextKeyMarker();
                uploadIdMarker = output.getNextUploadIdMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listMultipartUploads failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5pyq5ZCI5bm255qE5YiG54mH5LiK5Lyg5Lu75Yqh5ZKM5a2Q55uu5b2V"></span>
### **List incomplete multipart uploads and subdirectories under the specified directory**

TOS only supports the concept of objects. To simulate directory functionality, create a zero\-byte object that ends with a forward slash (`/`).

By using the two parameters `Delimiter` and `Prefix`, you can simulate the functionality of a directory:


* First, set `Delimiter` to `/`. At the same time, set `Prefix` to empty to return objects and subdirectory information in the root directory.

* When `Delimiter` is `/`, by simultaneously setting `Prefix` to the subdirectory `commonPrefixes`, objects and subdirectories in the subdirectory can be returned.


The following code demonstrates how to list incomplete multipart uploads and subdirectories in the root directory of the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class ListMultipartUploadsByDelimiterExample {
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
            String uploadIdMarker = null;
            while (isTruncated) {
                ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input().setBucket(bucketName)
                        .setMaxUploads(maxKeys).setDelimiter(delimiter).setKeyMarker(keyMarker).setUploadIDMarker(uploadIdMarker);
                ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
                System.out.printf("listMultipartUploads succeed, is truncated? %b, next uploadIDMarker is %s, " +
                        "next keyMarker is %s.\n", output.isTruncated(), output.getNextUploadIdMarker(), output.getNextKeyMarker());
                if (output.getUploads() != null) {
                    for (int i = 0; i < output.getUploads().size(); i++) {
                        ListedUpload upload = output.getUploads().get(i);
                        System.out.printf("Listed upload, key is %s, uploadId is %s, storageClass is %s\n",
                                upload.getKey(), upload.getUploadID(), upload.getStorageClass().getStorageClass());
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
                keyMarker = output.getNextKeyMarker();
                uploadIdMarker = output.getNextUploadIdMarker();
            }
        } catch (TosClientException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listMultipartUploads failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listMultipartUploads failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }

    private static void listCommonPrefix(String bucketName, int maxKeys, String delimiter, String prefix, TOSV2 tos) {
        boolean isTruncated = true;
        String keyMarker = null;
        String uploadIdMarker = null;
        while (isTruncated) {
            ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input().setBucket(bucketName)
                    .setMaxUploads(maxKeys).setDelimiter(delimiter).setKeyMarker(keyMarker)
                    .setUploadIDMarker(uploadIdMarker).setPrefix(prefix);
            ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
            System.out.printf("listMultipartUploads succeed, is truncated? %b, next uploadIDMarker is %s, " +
                    "next keyMarker is %s.\n", output.isTruncated(), output.getNextUploadIdMarker(), output.getNextKeyMarker());
            if (output.getUploads() != null) {
                for (int i = 0; i < output.getUploads().size(); i++) {
                    ListedUpload upload = output.getUploads().get(i);
                    System.out.printf("Listed upload, key is %s, uploadId is %s, storageClass is %s\n",
                            upload.getKey(), upload.getUploadID(), upload.getStorageClass().getStorageClass());
                }
            }
            if (output.getCommonPrefixes() != null) {
                for (int i = 0; i < output.getCommonPrefixes().size(); i++) {
                    ListedCommonPrefix commonPrefix = output.getCommonPrefixes().get(i);
                    System.out.println("Listed commonPrefix is " + commonPrefix.getPrefix());
                }
            }
            isTruncated = output.isTruncated();
            keyMarker = output.getNextKeyMarker();
            uploadIdMarker = output.getNextUploadIdMarker();
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For API documentation on listing multipart uploads, refer to [ListMultipartUploads](https://docs.byteplus.com/docs/tos/reference-listmultipartuploads).
