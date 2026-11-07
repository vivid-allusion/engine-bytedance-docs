---
title: "Configure Object-Level Expiration Time (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-object-level-expiration-time-java-sdk"
---

You can set the expiration time for an uploaded object using the `setObjectExpires` interface of the TOS Java SDK. After expiration, TOS will automatically delete the object.

<span id="ab21f5da"></span>
## **Notes**


* To set an object\-level expiration time, you must have the `tos:SetObjectExpires` permission. For detailed instructions, refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Set object\-level expiration time using the Java SDK; the Java SDK version must be 2.9.4 or above.


<span id="e934ce56"></span>
## Sample Code

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.*;

import java.io.ByteArrayInputStream;
import java.util.HashMap;
import java.util.Map;

public class SetObjectExpiresExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            SetObjectExpiresInput setInput = SetObjectExpiresInput.builder().bucket(bucketName).key(objectKey).objectExpires(1).build();
            tos.setObjectExpires(setInput);

            HeadObjectV2Output headRes = tos.headObject(HeadObjectV2Input.builder().bucket(bucketName).key(objectKey).build());
            String expiration = headRes.getRequestInfo().getHeader().get("x-tos-expiration");
            System.out.println("object: " + objectKey + "expiration: " + expiration);

            setInput = SetObjectExpiresInput.builder().bucket(bucketName).key(objectKey).objectExpires(0).build();
            tos.setObjectExpires(setInput);

            headRes = tos.headObject(HeadObjectV2Input.builder().bucket(bucketName).key(objectKey).build());
            expiration = headRes.getRequestInfo().getHeader().get("x-tos-expiration");
            System.out.println("object: " + objectKey + "expiration: " + expiration);
        } catch (TosClientException e) {
            System.out.println("setObjectExpires failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("setObjectExpires failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("setObjectExpires failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="c9101722"></span>
## **Related documentation**

For API documentation on configuring object\-level expiration time, refer to [SetObjectExpires](https://docs.byteplus.com/docs/tos/SetObjectExpires).
