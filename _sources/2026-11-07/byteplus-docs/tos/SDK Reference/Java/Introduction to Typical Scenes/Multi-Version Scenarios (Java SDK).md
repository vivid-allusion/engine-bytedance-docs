---
title: "Multi-Version Scenarios (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multi-version-scenes-java-sdk"
---

Versioning applies to all objects within a bucket. After enabling versioning for a bucket, if an object is accidentally deleted or overwritten, you can restore the object to any of its previous versions. Several interfaces provided by the TOS Java SDK support operations involving versioning functionality. In TOS, bucket versioning status includes three states: Disabled, Enabled, and Suspended. This article describes how to manage bucket versioning status using the TOS Java SDK.

<span id=".5aSa54mI5pys6K-05piO"></span>
## Versioning status


* If versioning is enabled for your bucket, each time you call the SDK's `putObject` method, a unique version ID is generated for every uploaded object. When `deleteObject` is called, the object is not deleted; instead, a delete marker with a version ID is generated for the object, marking it as deleted. When calling interfaces such as `getObject`, `getObjectACL`, `copyObject`, `uploadPartCopy`, and `deleteObject`, you can specify the exact version of the object to operate on by using the optional parameter "versionID".

* If the versioning feature of your bucket is in Suspended status, the version ID of newly uploaded objects will be null. If a null version already exists among the historical versions of the object, that historical version will be deleted, and the latest version will be set to the null version. Specifically, in the case of object deletion, the latest version is a delete marker with a null version number. Versioning for a bucket can be enabled or suspended, but it cannot be reverted to its original unenabled state.


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* To enable or suspend bucket versioning, your account must have the `tos:PutBucketVersioning` permission.

* To query the versioning status of a bucket, your account must have the `tos:GetBucketVersioning` permission.

* The `putBucketVersioning` and `getBucketVersioning` interfaces of the Java SDK were introduced in version 2.5.0. Please upgrade to version 2.5.0 or later to use these interfaces.


<span id=".6K6-572u5qG254mI5pys5o6n5Yi254q25oCB"></span>
## **Configure bucket versioning status**

The following code demonstrates how to set the versioning status for a bucket to either Enabled or Suspended.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.VersioningStatusType;
import com.volcengine.tos.model.bucket.PutBucketVersioningInput;
import com.volcengine.tos.model.bucket.PutBucketVersioningOutput;

public class PutBucketVersioningExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            PutBucketVersioningInput input = new PutBucketVersioningInput().setBucket(bucketName)
                    .setStatus(VersioningStatusType.VERSIONING_STATUS_ENABLED);
            PutBucketVersioningOutput output = tos.putBucketVersioning(input);
            System.out.println("putBucketVersioning succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketVersioning failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketVersioning failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketVersioning failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W5qG255qE54mI5pys5o6n5Yi254q25oCB"></span>
## **Retrieve bucket versioning status**

The following code demonstrates how to retrieve the versioning status information of a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketVersioningInput;
import com.volcengine.tos.model.bucket.GetBucketVersioningOutput;

public class GetBucketVersioningExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketVersioningInput input = new GetBucketVersioningInput().setBucket(bucketName);
            GetBucketVersioningOutput output = tos.getBucketVersioning(input);
            System.out.println("getBucketVersioning succeed");
            System.out.println("bucket versioning status is " + output.getStatus());
        } catch (TosClientException e) {
            System.out.println("getBucketVersioning failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketVersioning failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketVersioning failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5LiL6L295aSa54mI5pys5a-56LGh"></span>
## **Download specified object versions**

The following code demonstrates how to download a specified version of the `example_object.txt` object located in the `example_dir` directory of the bucket `bucket-example`. It then reads the object directly into memory and prints its contents as a string.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class GetObjectVersioningInStringExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String versionId = "";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setVersionID(versionId);
        try(GetObjectV2Output output = tos.getObject(input);
            BufferedReader reader = new BufferedReader(new InputStreamReader(output.getContent()))) {
            System.out.println("begin to read content in object.");
            String line = reader.readLine();
            while (line != null) {
                System.out.println(line);
                line = reader.readLine();
            }
        } catch (IOException e) {
            System.out.println("read data in object failed");
            e.printStackTrace();
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


<span id=".5YiX5Li-5aSa54mI5pys5a-56LGh"></span>
## **List object versions**

For information on how to list objects with multiple versions, see [List object versions](https://docs.byteplus.com/docs/tos/List-multiversion-objects-java-sdk).

<span id=".5ou36LSd5aSa54mI5pys5a-56LGh"></span>
## **Copy specified object versions**

The following code demonstrates how to copy a specified version of an object to the bucket `bucket-example`, placing it in the `example_dir` directory as the object `example_object.txt`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.CopyObjectV2Input;
import com.volcengine.tos.model.object.CopyObjectV2Output;

public class CopyObjectVersioningExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String srcBucketName = "src-bucket-example";
        String srcObjectKey = "src_example_dir/example_object.txt";
        String srcObjectVersionId = "the specific version id";
        String bucketName = "bucket-example";
        String objectKey = "dst_example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            CopyObjectV2Input input = new CopyObjectV2Input().setBucket(bucketName).setKey(objectKey)
                    .setSrcBucket(srcBucketName).setSrcKey(srcObjectKey).setSrcVersionID(srcObjectVersionId);
            CopyObjectV2Output output = tos.copyObject(input);
            System.out.println("copyObject succeed, object's etag is " + output.getEtag());
            System.out.println("copyObject succeed, object's crc64 is " + output.getHashCrc64ecma());
        } catch (TosClientException e) {
            System.out.println("copyObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("copyObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("copyObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk5aSa54mI5pys5a-56LGh"></span>
## **Delete objects with multiple versions**

<span id=".5Yig6Zmk5Y2V5Liq5a-56LGh"></span>
### **Delete a specified object version**

For an example of how to delete an object with multiple versions, see [Delete a specified object version](https://docs.byteplus.com/docs/tos/Delete-object-java-sdk#%E5%88%A0%E9%99%A4%E6%8C%87%E5%AE%9A%E7%89%88%E6%9C%AC%E5%AF%B9%E8%B1%A1).

<span id=".5Yig6Zmk5oyH5a6a5YmN57yA5LiL55qE5omA5pyJ5a-56LGh"></span>
### **Delete all objects under the specified prefix**

The following code demonstrates how to delete all versions of all objects located in the `example_dir` directory within the bucket `bucket-example`.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">All objects in the bucket will be deleted if the <code>prefix</code> parameter is not set (i.e., if the <code>prefix</code> is <code>null</code>) or is set to an empty string (""). Please check carefully before using this code.</div>


```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

public class DeleteObjectVersioningWithPrefixExample {
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
            String keyMarker = null;
            String versionIdMarker = null;
            while (isTruncated) {
                ListObjectVersionsV2Input input = new ListObjectVersionsV2Input().setBucket(bucketName)
                        .setPrefix(prefix).setKeyMarker(keyMarker).setVersionIDMarker(versionIdMarker);
                ListObjectVersionsV2Output output = tos.listObjectVersions(input);
                if (output.getVersions() != null){
                    for (int i = 0; i < output.getVersions().size(); i++) {
                        ListedObjectVersion version = output.getVersions().get(i);
                        DeleteObjectInput deleteInput = new DeleteObjectInput().setBucket(bucketName)
                                .setKey(version.getKey()).setVersionID(version.getVersionID());
                        tos.deleteObject(deleteInput);
                        System.out.println("deleteObject succeed, deleted key is " + version);
                    }
                }
                if (output.getDeleteMarkers() != null){
                    for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                        ListedDeleteMarkerEntry deleteMarker = output.getDeleteMarkers().get(i);
                        DeleteObjectInput deleteInput = new DeleteObjectInput().setBucket(bucketName)
                                .setKey(deleteMarker.getKey()).setVersionID(deleteMarker.getVersionID());
                        tos.deleteObject(deleteInput);
                        System.out.println("deleteObject succeed, deleted key is " + deleteMarker);
                    }
                }
                isTruncated = output.isTruncated();
                keyMarker = output.getNextKeyMarker();
                versionIdMarker = output.getNextVersionIDMarker();
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
