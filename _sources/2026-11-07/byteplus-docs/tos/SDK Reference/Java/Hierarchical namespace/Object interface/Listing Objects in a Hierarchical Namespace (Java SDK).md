---
title: "Listing Objects in a Hierarchical Namespace (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-within-hierarchical-namespace-java-sdk"
---

Hierarchical NameSpace (HNS), abbreviated in Chinese as 'hierarchical bucket', is a brand new bucket type introduced by TOS Object Storage that is based on hierarchical metadata management. Besides its hierarchical namespace features, a HNS bucket can scale as much as a FNS bucket. It also delivers seamless interoperability between object and file semantics. This allows **data to be accessed through multiple protocols**, so you can process data more efficiently.

Compared to the original Flat NameSpace (FNS, also known as flat bucket), directory\-level mv and rename operations are now well supported. Common read operations such as List and directory Head have also been optimized, improving data processing efficiency and performance. These enhancements effectively meet the requirements of big data, data lake, and AI application scenarios.

This article describes how to use the TOS Java SDK `listObjects` interface to enumerate objects, subdirectories, etc., within a specified directory.

<span id="feb85cb4"></span>
## **Notes**


* When enumerating hierarchical namespace objects, the `delimiter` must be specified, and only directory separators are permitted.`/` 

* Before listing objects, your account must have the `tos:ListBucket` permission. For detailed instructions, refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

* The current TOS already supports the new `listObjectsType2` interface, and its usage is generally consistent with that of the `listObjects` interface. It is strongly recommended that you use the `listObjectsType2` interface to achieve higher enumeration efficiency. For detailed instructions on usage, please refer to [List of Objects V2](https://docs.byteplus.com/docs/tos/List-objects-v2-java-sdk).


<span id="20d00992"></span>
## Parameters

The parameters supported by the `listObjects` interface are as follows.


|**Parameter** |**Description** |
|---|---|
|prefix |The prefix of the current query result. |
|delimiter |When listing hierarchical namespace objects, the grouping character must include the `delimiter`. Only the directory separator can be used.`/`  |
|marker |The starting point for the items enumerated in this instance. Initially set to null; subsequently, it can take the value of nextMarker returned by the previous request. |
|maxKeys |Returns the maximum number of objects to be enumerated. A maximum of 1,000 results can be returned per request. If this parameter is not specified, 1,000 results will be returned by default. |
|encodingType |Encode the returned content and specify the encoding type. |


<span id="62a31f82"></span>
## Sample Code

<span id="339480bd"></span>
### **List the files and subdirectories in the specified directory.** 

The hierarchical bucket organizes metadata according to a brand\-new hierarchical architecture, and therefore contains directory entities.

The directory listing function is implemented using the `Delimiter` and `Prefix` parameters:


* First, set `Delimiter` to`/`By setting `Prefix` to empty, you can retrieve information about objects and subdirectories in the root directory.

* Reset `Delimiter` to`/`When you set the `Prefix` as a subdirectory (`commonPrefixes`), objects in the subdirectory and its subdirectories can be returned.


The following code demonstrates how to list the objects and subdirectories in the root directory of the bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class HNSListObjectsExample {
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


<span id="ae0fcf20"></span>
## **Related documentation**

For API documentation on listing objects, refer to [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects).
