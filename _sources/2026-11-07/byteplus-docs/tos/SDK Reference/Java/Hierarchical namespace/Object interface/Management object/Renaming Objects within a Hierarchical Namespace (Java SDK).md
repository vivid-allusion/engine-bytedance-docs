---
title: "Renaming Objects within a Hierarchical Namespace (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Rename-objects-within-hierarchical-namespace-java-sdk"
---

Hierarchical Namespace (HNS), also referred to as the hierarchical bucket, is a brand new bucket type introduced by TOS. It is based on hierarchical metadata management. Besides its hierarchical namespace features, an HNS bucket can scale as much as a FNS bucket. It also delivers seamless interoperability between object and file semantics. This allows **data to be accessed through multiple protocols**, so you can process data more efficiently.

Compared with the original Flat NameSpace (FNS, also known as flat bucket), HNS now provides strong support for directory\-level mv and rename operations. It also optimizes common read operations such as List and directory Head, thereby improving data processing efficiency and performance. These enhancements are well suited to the usage scenarios of big data, data lakes, and AI.

This article explains how to use the TOS Java SDK `renameObject` interface to rename a specified object to a different object name.

<span id="20e60b26"></span>
## **Precautions**


* Concurrent renaming is not supported for the same object.

* All information contained in the metadata of the renamed object is identical to that of the source object.

* Renaming a directory to the name of an existing directory is not supported.


<span id="82652d9d"></span>
## **Sample code**

<span id="60ee7d6f"></span>
### Rename object

The following code demonstrates how to rename an object.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.RenameObjectInput;
import com.volcengine.tos.model.object.RenameObjectOutput;

public class HNSRenameObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        String renamedObjectKey = "example_dir/example_object_rename.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            RenameObjectInput input = new RenameObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setNewKey(renamedObjectKey);
            RenameObjectOutput output = tos.renameObject(input);
            System.out.println(output.getRequestInfo().getRequestId());
            System.out.println("renameObject succeed.");
        } catch (TosClientException e) {
            System.out.println("renameObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("renameObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("renameObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="6f819fbf"></span>
### Rename directory

The following code demonstrates how to rename a directory.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.RenameObjectInput;
import com.volcengine.tos.model.object.RenameObjectOutput;

public class HNSRenameDirExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "source_dir";
        String renamedObjectKey = "dest_dir";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            RenameObjectInput input = new RenameObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setNewKey(renamedObjectKey);
            RenameObjectOutput output = tos.renameObject(input);
            System.out.println(output.getRequestInfo().getRequestId());
            System.out.println("renameObject succeed.");
        } catch (TosClientException e) {
            System.out.println("renameObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("renameObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("renameObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="dff0bc4a"></span>
## Related documentation

For API documentation regarding RenameObject, please refer to [RenameObject](https://docs.byteplus.com/docs/tos/Renameobject).
