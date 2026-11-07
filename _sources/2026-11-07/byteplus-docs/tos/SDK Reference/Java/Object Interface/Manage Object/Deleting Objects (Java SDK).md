---
title: "Deleting Objects (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-object-java-sdk"
---

When objects are no longer in use, you can delete them to reduce cost overhead. The TOS Java SDK supports deleting individual objects from a bucket as well as deleting multiple specified objects. For buckets with versioning enabled, you can delete data for a specified version of an object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Notes**


* To delete an object, your account must have the `tos:DeleteObject` permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete multi\-version objects, your account must have the `tos:DeleteObjectVersion` permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Please exercise caution when performing delete operations, as files cannot be restored once deleted.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5Yig6Zmk5oyH5a6a5a-56LGh"></span>
### **Delete an object**

The following code demonstrates how to delete the `example_object.txt` file located in the `example_dir` directory of the specified bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.DeleteObjectInput;
import com.volcengine.tos.model.object.DeleteObjectOutput;

public class DeleteObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteObjectInput input = new DeleteObjectInput().setBucket(bucketName).setKey(objectKey);
            DeleteObjectOutput output = tos.deleteObject(input);
            System.out.println("deleteObject succeed.");
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


<span id=".5Yig6Zmk5oyH5a6a54mI5pys5a-56LGh"></span>
### **Delete an object version**

The following code demonstrates how to delete the `example_object.txt` file located in the `example_dir` directory of the multi\-version bucket `bucket-example` by specifying its version number.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.DeleteObjectInput;
import com.volcengine.tos.model.object.DeleteObjectOutput;

public class DeleteObjectWithVersionIdExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String versionId = "the specific version id";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteObjectInput input = new DeleteObjectInput().setBucket(bucketName).setKey(objectKey).setVersionID(versionId);
            DeleteObjectOutput output = tos.deleteObject(input);
            System.out.println("deleteObject succeed.");
            System.out.println("is the object a delete marker? " + output.isDeleteMarker());
            System.out.println("the deleted version id is " + output.getVersionID());
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


<span id=".5om56YeP5Yig6Zmk5a-56LGh"></span>
### **Batch delete objects**

You can use the Java SDK's `deleteMultiObjects` interface to delete multiple objects in a single request. The following code demonstrates how to delete multiple objects from the specified bucket 'bucket\-example'.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The response mode supported for batch object deletion can be configured using <code>quiet</code>:</div>



* <div data-tips="true" data-tips-type="tip">When <code>quiet</code> is set to <code>false</code>, the response will include the deletion result regardless of whether the object was successfully deleted.</div>


* <div data-tips="true" data-tips-type="tip">When <code>quiet</code> is set to <code>true</code>, only the results of objects that failed to be deleted are returned in the response; objects not returned are considered to have been deleted successfully.</div>



```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

import java.util.ArrayList;
import java.util.List;

public class DeleteMultiObjectsExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String objectKey1 = "example_dir/example_object_1.txt";
        String objectKey2 = "example_dir/example_object_2.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            List<ObjectTobeDeleted> objs = new ArrayList<>();
            objs.add(new ObjectTobeDeleted().setKey(objectKey));
            objs.add(new ObjectTobeDeleted().setKey(objectKey1));
            objs.add(new ObjectTobeDeleted().setKey(objectKey2));
            DeleteMultiObjectsV2Input input = new DeleteMultiObjectsV2Input().setBucket(bucketName).setObjects(objs);
            DeleteMultiObjectsV2Output output = tos.deleteMultiObjects(input);
            System.out.println("deleteMultiObjects succeed.");
            if (output.getDeleteds() != null) {
                for (int i = 0; i < output.getDeleteds().size(); i++){
                    Deleted deleted = output.getDeleteds().get(i);
                    System.out.println("deleted object is " + deleted);
                }
            }
            if (output.getErrors() != null) {
                for (int i = 0; i < output.getErrors().size(); i++){
                    DeleteError error = output.getErrors().get(i);
                    System.out.println("delete error is " + error);
                }
            }
        } catch (TosClientException e) {
            System.out.println("deleteMultiObjects failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteMultiObjects failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteMultiObjects failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5om56YeP5Yig6Zmk5bim54mI5pys55qE5a-56LGh"></span>
### **Batch delete object versions**

The following code demonstrates how to delete multiple object versions by specifying version numbers in the designated bucket `bucket-example`.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

import java.util.ArrayList;
import java.util.List;

public class DeleteMultiObjectsWithVersionsExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String versionId = "the version id of objectKey";
        String objectKey1 = "example_dir/example_object_1.txt";
        String versionId1 = "the version id of objectKey1";
        String objectKey2 = "example_dir/example_object_2.txt";
        String versionId2 = "the version id of objectKey2";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            List<ObjectTobeDeleted> objs = new ArrayList<>();
            objs.add(new ObjectTobeDeleted().setKey(objectKey).setVersionID(versionId));
            objs.add(new ObjectTobeDeleted().setKey(objectKey1).setVersionID(versionId1));
            objs.add(new ObjectTobeDeleted().setKey(objectKey2).setVersionID(versionId2));
            DeleteMultiObjectsV2Input input = new DeleteMultiObjectsV2Input().setBucket(bucketName).setObjects(objs);
            DeleteMultiObjectsV2Output output = tos.deleteMultiObjects(input);
            System.out.println("deleteMultiObjects succeed.");
            if (output.getDeleteds() != null) {
                for (int i = 0; i < output.getDeleteds().size(); i++){
                    Deleted deleted = output.getDeleteds().get(i);
                    System.out.println("deleted object is " + deleted);
                }
            }
            if (output.getErrors() != null) {
                for (int i = 0; i < output.getErrors().size(); i++){
                    DeleteError error = output.getErrors().get(i);
                    System.out.println("delete error is " + error);
                }
            }
        } catch (TosClientException e) {
            System.out.println("deleteMultiObjects failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteMultiObjects failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteMultiObjects failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk5qG25Lit5oyH5a6a5YmN57yA55qE5a-56LGh"></span>
### **Delete objects with a specified prefix in the bucket**

The following code demonstrates how to delete objects with the `example_dir/` prefix from the specified bucket `bucket-example`.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">In the following code, if the <code>prefix</code> parameter is not set (that is, if <code>prefix</code> is <code>null</code>), setting prefix = "" (an empty string) will delete all objects in the bucket. Please check carefully before use.</div>


```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.DeleteObjectInput;
import com.volcengine.tos.model.object.ListObjectsType2Input;
import com.volcengine.tos.model.object.ListObjectsType2Output;

public class DeleteObjectWithPrefixExample {
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


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**


* For API documentation on deleting objects, see [DeleteObject](https://docs.byteplus.com/docs/tos/Delete-object-java-sdk).

* For API documentation on deleting multi\-version objects, please refer to [DeleteMultiObjects](https://docs.byteplus.com/docs/tos/reference-deletemultiobjects).
