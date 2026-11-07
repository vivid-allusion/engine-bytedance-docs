---
title: "Renaming Objects (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Rename-objects-java-sdk"
---

This document describes how to rename objects using the TOS Java SDK.

<span id="a5f0d621"></span>
## **Category**


* Starting from version 2.6.0, the TOS Java SDK supports object renaming.

* Before using the renaming function, you must first enable the renaming function.

* RenameObject only supports renaming objects uploaded after it is enabled. Objects uploaded before this feature is enabled are not supported.

* Concurrent renaming is not supported for the same object.

* All information contained in the metadata of the renamed object is identical to that of the source object.

* Only single\-object renaming is supported; batch renaming is not available.

* Multi\-version objects do not support renaming.

* A 400 error will occur if the objectKey remains the same during renaming; for example, renaming `objectA` to `objectA`.

* If the objectKey to be renamed already exists, it will be overwritten by default. For example, if there are two objects, `objectA` and `objectB`, and `objectA` is renamed to `objectB`, the data of `objectB` will be overwritten. For more information, see [Using RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject).


<span id="1040b47a"></span>
## **Sample Code**

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.RenameObjectInput;
import com.volcengine.tos.model.object.RenameObjectOutput;

public class RenameObjectExample {
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


<span id="948cb917"></span>
## Related documentation

For the API documentation on RenameObject, please refer to [RenameObject](https://docs.byteplus.com/docs/tos/Renameobject).
