---
title: "List Objects in Hierarchical Namespace V2 (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-in-hierarchical-namespace-v2-java-sdk"
---

Hierarchical NameSpace (HNS), abbreviated as hierarchical bucket, is a brand\-new bucket type introduced by TOS Object Storage. It is based on hierarchical metadata management. Besides its hierarchical namespace features, a HNS bucket can scale as much as a FNS bucket. It also delivers seamless interoperability between object and file semantics. This allows **data to be accessed through multiple protocols**, so you can process data more efficiently.

Compared to the original flat namespace (FNS, Flat NameSpace, also referred to as flat bucket), the system provides robust support for directory\-level 'mv' and 'rename' operations. It also optimizes common read operations such as 'List' and directory 'Head', thereby enhancing data processing efficiency and performance. These improvements effectively meet the usage scenarios of big data, data lake, and AI applications.

This article describes how to use the TOS Java SDK `listObjectsType2` interface to enumerate objects, subdirectories, etc. within a specified directory.

<span id="feb85cb4"></span>
## **Category**


* When enumerating hierarchical namespace objects, the `delimiter` must be included and only the directory separator may be used.`/` 

* Before listing objects, your account must have the `tos:ListBucket` permission. For detailed instructions, refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id="20d00992"></span>
## Parameters

`listObjectsType2` interface supports the following parameters.


|**Parameter** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used to group object names. |
|startAfter |The starting point for the objects enumerated in this instance. |
|continuationToken |The specified enumeration operation must begin from this token. It can be obtained from the nextContinuationToken in the previous listing results. |
|maxKeys |Returns the maximum number of enumerated objects. A maximum of 1,000 results can be returned per request; if not specified, the default is 1,000 results. |
|encodingType |Encode the returned content and specify the type of encoding. |


<span id="e810026b"></span>
## Sample Code

<span id="3d338694"></span>
### **List the files and subdirectories in the specified directory.** 

The layered bucket organizes metadata according to a brand\-new layered architecture and therefore has directory entities.

The directory listing function is implemented using the `Delimiter` and `Prefix` parameters:


* First, set the `Delimiter` to`/`By also setting `Prefix` to empty, you can retrieve information about objects and subdirectories under the root directory.

* Reset `Delimiter` to`/`By setting `Prefix` to a subdirectory (`commonPrefixes`), the objects and subdirectories of that subdirectory can be returned.


The following code demonstrates how to list the objects and subdirectories in the root directory of the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.ListObjectsType2Input;
import com.volcengine.tos.model.object.ListObjectsType2Output;
import com.volcengine.tos.model.object.ListedCommonPrefix;
import com.volcengine.tos.model.object.ListedObjectV2;

public class HNSListObjectsType2Example {
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
