---
title: "Restoring Objects (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Restore-objects-java-sdk"
---

You need to restore files in Cold Archive before reading them. This article describes how to restore Cold Archive objects using the TOS Java SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Category


* Starting from version 2.6.0, the TOS Java SDK supports restoring Cold Archive objects.

* Cold Archive objects cannot be read directly; you must restore the object before performing any read operations. Before restoring a Cold Archive object, you need to have the `RestoreObject` permission.

* After a Cold Archive object is restored, TOS generates a temporary copy in the standard storage class for you to access. This copy will automatically be deleted after the validity period ends.

* After the object is restored, you can also use the RestoreObject interface to extend the validity period of the restored object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to use the SDK's `restoreObject` interface to restore the object "object\-example" in the bucket "bucket\-example".

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.TierType;
import com.volcengine.tos.model.object.RestoreJobParameters;
import com.volcengine.tos.model.object.RestoreObjectInput;
import com.volcengine.tos.model.object.RestoreObjectOutput;

public class RestoreObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        int days = 1;

        TierType type = TierType.TIER_STANDARD;

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            RestoreObjectInput input = new RestoreObjectInput().setBucket(bucketName).setKey(objectKey)
                    .setRestoreJobParameters(new RestoreJobParameters().setTier(type))
                    .setDays(days);
            RestoreObjectOutput output = tos.restoreObject(input);
            System.out.println(output.getRequestInfo().getRequestId());
            System.out.println("restoreObject succeed.");
        } catch (TosClientException e) {
            System.out.println("restoreObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("restoreObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("restoreObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For more information about restoring objects, see [RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject).
