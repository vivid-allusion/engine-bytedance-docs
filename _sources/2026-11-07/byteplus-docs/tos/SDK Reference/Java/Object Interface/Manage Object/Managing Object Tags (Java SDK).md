---
title: "Managing Object Tags (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-labels-java-sdk"
---

TOS supports assigning custom tags to objects and enables lifecycle management of specific objects based on these tags. This article describes how to manage object tags using the TOS Java SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Category**


* To set object tags, you must have the `tos:PutObjectTagging` permission. For detailed steps, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To retrieve object tags, you must have the `tos:GetObjectTagging` permission. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete object tags, you must have the `tos:DeleteObjectTagging` permission. For detailed instructions, refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* A maximum of 10 tags can be added to each object, and the Key for the same object must not be duplicated. For details on object tag restrictions, please refer to [Object Tag Restriction Explanation](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).


<span id=".6K6-572u5a-56LGh5qCH562-"></span>
## **Setting tags for an object**

The following code demonstrates how to use the SDK's `putObjectTagging` interface to set tags for the `bucket-example` bucket's `object-example` object.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.Tag;
import com.volcengine.tos.model.object.PutObjectTaggingInput;
import com.volcengine.tos.model.object.PutObjectTaggingOutput;
import com.volcengine.tos.model.object.TagSet;

import java.util.ArrayList;
import java.util.List;

public class PutObjectTaggingExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            PutObjectTaggingInput input = new PutObjectTaggingInput().setBucket(bucketName).setKey(objectKey);
            Tag tag1 = new Tag().setKey("tagA").setValue("valueA");
            Tag tag2 = new Tag().setKey("tagB").setValue("valueB");
            List<Tag> tagList = new ArrayList<>();
            tagList.add(tag1);
            tagList.add(tag2);
            TagSet tagSet = new TagSet();
            tagSet.setTags(tagList);
            input.setTagSet(tagSet);
            PutObjectTaggingOutput output = tos.putObjectTagging(input);
            System.out.println("putObjectTagging succeed");
        } catch (TosClientException e) {
            System.out.println("putObjectTagging failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putObjectTagging failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putObjectTagging failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W5a-56LGh5qCH562-"></span>
## **Getting tags of an object**

After setting object tags, you can retrieve the tag information of the object.

The following code demonstrates how to use the SDK's `getObjectTagging` interface to obtain the tag information of the `object-example` object in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.Tag;
import com.volcengine.tos.model.object.GetObjectTaggingInput;
import com.volcengine.tos.model.object.GetObjectTaggingOutput;

public class GetObjectTaggingExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetObjectTaggingInput input = new GetObjectTaggingInput().setBucket(bucketName).setKey(objectKey);
            GetObjectTaggingOutput output = tos.getObjectTagging(input);
            System.out.println("getObjectTagging succeed");
            if (output.getTagSet() != null && output.getTagSet().getTags() != null) {
                System.out.println("this object has " + output.getTagSet().getTags().size() + " tags");
                for (int i = 0; i < output.getTagSet().getTags().size(); i++){
                    Tag tag = output.getTagSet().getTags().get(i);
                    System.out.println("No." + (i+1) + " tag is " + tag);
                }
            } else {
                System.out.println("this object does not have tags.");
            }
        } catch (TosClientException e) {
            System.out.println("getObjectTagging failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getObjectTagging failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getObjectTagging failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk5a-56LGh5qCH562-"></span>
## **Deleting tags from an object**

The following code demonstrates how to use the SDK's `deleteObjectTagging` interface to delete the tag information of the `object-example` object in the `bucket-example` bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.DeleteObjectTaggingInput;
import com.volcengine.tos.model.object.DeleteObjectTaggingOutput;

public class DeleteObjectTaggingExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteObjectTaggingInput input = new DeleteObjectTaggingInput().setBucket(bucketName).setKey(objectKey);
            DeleteObjectTaggingOutput output = tos.deleteObjectTagging(input);
            System.out.println("deleteObjectTagging succeed.");
        } catch (TosClientException e) {
            System.out.println("deleteObjectTagging failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteObjectTagging failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteObjectTagging failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information about object tags, see [PutObjectTagging](https://docs.byteplus.com/docs/tos/reference-putobjecttagging-).
