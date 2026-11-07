---
title: "Managing Bucket Storage Types (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-storage-types-java-sdk"
---

A bucket is a globally unique namespace in TOS, functioning as a data container used to store object data. TOS provides multiple bucket\-level storage types, each designed for distinct application scenarios. This article explains how to manage bucket storage types using the TOS Java SDK.

<span id=".5a2Y5YKo57G75Z6L6K-05piO"></span>
## Storage types

TOS provides the following types of bucket storage.


|**Storage type** |**Description** |**Access permission value** |
|---|---|---|
|Standard |The default bucket storage type, suitable for a variety of business scenarios, including social and sharing\-type image and audio/video applications, large\-scale websites, big data analytics, program downloads, and mobile applications. |StorageClassType.STORAGE_CLASS_STANDARD |
|Infrequent Access |Applicable to business scenarios with low access frequency (an average of 1 to 2 accesses per month), such as hot standby data, surveillance video data, etc. |StorageClassType.STORAGE_CLASS_IA |
|Flashback Archive |Designed for long\-lived, rarely accessed data, such as archives. |StorageClassType.STORAGE_CLASS_ARCHIVE_FR |
|Intelligent Tiering |Designed for data with unpredictable access patterns. It automatically moves data between storage types based on how often it's accessed to reduce storage costs. |StorageClassType.STORAGE_CLASS_INTELLIGENT_TIERING |
|Cold Archive |Designed for cold data that is long\-lived and rarely accessed. Data must be stored for at least 180 days. You must first restore cold archived data before you can access it. |StorageClassType.COLD_ARCHIVE |


<span id=".6K6-572u5a2Y5YKo57G75Z6L"></span>
## **Configure storage type**

You can set the storage type for a specified bucket through the `putBucketStorageClass` interface of the TOS Java SDK.

<span id=".5a2Y5YKo57G75Z6L6K-05piO"></span>
## Storage types

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">By default, only the bucket owner is authorized to set the bucket storage type.</div>


* <div data-tips="true" data-tips-type="warning">When creating a bucket, if no storage type is specified, the default storage type is Standard Storage.</div>


* <div data-tips="true" data-tips-type="warning">After the bucket storage type is configured, if the storage type is not specified when uploading an object, copying an object, or initializing a multipart upload task, the object will, by default, inherit the storage type of the bucket.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to set the storage type for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.bucket.PutBucketStorageClassInput;
import com.volcengine.tos.model.bucket.PutBucketStorageClassOutput;

public class PutBucketStorageClassExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            StorageClassType storageClass = StorageClassType.STORAGE_CLASS_IA;
            PutBucketStorageClassInput input = new PutBucketStorageClassInput().setBucket(bucketName)
                    .setStorageClass(storageClass);
            PutBucketStorageClassOutput output = tos.putBucketStorageClass(input);
            System.out.println("putBucketStorageClass succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketStorageClass failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketStorageClass failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketStorageClass failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W5qG25a2Y5YKo57G75Z6L"></span>
## **Retrieve bucket storage type**

You can obtain the currently configured storage type of a specified bucket through the `headBucket` interface of the TOS Java SDK.

For relevant instructions and sample code regarding the `headBucket` interface, please refer to [Get bucket metadata](https://docs.byteplus.com/docs/tos/Get-bucket-metadata-java-sdk).

<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information about storage types, see [Storage types](https://docs.byteplus.com/docs/tos/docs-storage-type).
