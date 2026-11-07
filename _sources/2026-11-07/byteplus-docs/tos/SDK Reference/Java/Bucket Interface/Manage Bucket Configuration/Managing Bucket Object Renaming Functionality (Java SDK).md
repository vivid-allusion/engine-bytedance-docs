---
title: "Managing Bucket Object Renaming Functionality (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-rename-object-functionality-java-sdk"
---

TOS supports the renaming of individual objects within a bucket. To use the object renaming feature, you must first enable the bucket's renaming function.

<span id="4ba0a069"></span>
## **Enable bucket renaming rules**

You can enable the bucket renaming feature through the `PutBucketRename` interface of the TOS Java SDK.

<span id="7939972e"></span>
### **Category**


* The `renameEnable` parameter can only be set to `true`.

* Enabling the rename function is not supported for multi\-version buckets.


<span id="2719e726"></span>
### **Sample Code**

The following code demonstrates how to enable the bucket renaming feature.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.PutBucketRenameInput;
import com.volcengine.tos.model.bucket.PutBucketRenameOutput;

public class PutBucketRenameExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            boolean renameEnable = true;
            PutBucketRenameInput input = new PutBucketRenameInput().setBucket(bucketName).setRenameEnable(renameEnable);
            PutBucketRenameOutput output = tos.putBucketRename(input);
            System.out.println("putBucketRename succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketRename failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketRename failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketRename failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="63728472"></span>
## **Retrieve the bucket renaming rules.** 

You can query whether a bucket is in the rename enabled state via the TOS Java SDK `GetBucketRename` API.

<span id="447b1295"></span>
### **Category**

Get whether the bucket is in the renaming enabled state; by default, you must be the bucket owner.

<span id="60f19a17"></span>
### **Sample Code**

The following code demonstrates how to query the renaming status of a bucket.

```Java

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketRenameInput;
import com.volcengine.tos.model.bucket.GetBucketRenameOutput;

public class GetBucketRenameExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketRenameInput input = new GetBucketRenameInput().setBucket(bucketName);
            GetBucketRenameOutput output = tos.getBucketRename(input);
            System.out.println("getBucketRename succeed, bucket rename enable? " + output.isRenameEnable());
        } catch (TosClientException e) {
            System.out.println("getBucketRename failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketRename failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketPolicy failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="21e9a3e6"></span>
## **Disable bucket renaming rules**

You can disable the bucket rename status via the TOS Java SDK `DeleteBucketRename` interface. Once disabled, renaming operations cannot be performed.

<span id="60021edb"></span>
### **Category**

To disable the renaming status of a bucket, you must be the bucket owner by default.

<span id="fd1e1538"></span>
### **Sample Code**

The following code demonstrates how to disable the renaming state of a bucket.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketRenameInput;
import com.volcengine.tos.model.bucket.DeleteBucketRenameOutput;

public class DeleteBucketRenameExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketRenameInput input = new DeleteBucketRenameInput().setBucket(bucketName);
            DeleteBucketRenameOutput output = tos.deleteBucketRename(input);
            System.out.println("deleteBucketRename succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucketRename failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucketRename failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucketPolicy failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="8ffc67bf"></span>
## Related documentation


* For detailed information about RenameObject, refer to [Using RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject).

* For API documentation regarding the renaming rules for enabled buckets, refer to [PutBucketRename](https://docs.byteplus.com/docs/tos/Putbucketrename).

* For the API documentation on obtaining bucket renaming rules, see [GetBucketRename](https://docs.byteplus.com/docs/tos/Getbucketrename).

* For API documentation on the renaming rules when closing buckets, refer to [DeleteBucketRename](https://docs.byteplus.com/docs/tos/Deletebucketrename).
