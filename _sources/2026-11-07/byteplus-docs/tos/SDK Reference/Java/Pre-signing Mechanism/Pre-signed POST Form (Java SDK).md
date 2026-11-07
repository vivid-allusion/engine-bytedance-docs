---
title: "Pre-signed POST Form (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Post-form-presignature-java-sdk"
---

This article presents example code for POST form presigning.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.model.object.PreSignedPostSignatureInput;
import com.volcengine.tos.model.object.PreSignedPostSignatureOutput;

public class PreSignedPostSignatureExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";
        long expires = 3600;
        List<PostSignatureCondition> conditions = new ArrayList<>(2);
        conditions.add(new PostSignatureCondition("x-tos-acl", "private"));
        conditions.add(new PostSignatureCondition("key", objectKey, "starts-with"));

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            PreSignedPostSignatureInput input = new PreSignedPostSignatureInput().setBucket(bucketName)
                    .setExpires(expires).setConditions(conditions);
            PreSignedPostSignatureOutput output = tos.preSignedPostSignature(input);
            System.out.println("preSignedPostSignature succeed, the signature is " + output.getSignature());
            System.out.println("the credential is " + output.getCredential());
            System.out.println("the policy is " + output.getPolicy());
            System.out.println("the date is " + output.getDate());
            System.out.println("the algorithm is " + output.getAlgorithm());
            System.out.println("the originPolicy is " + output.getOriginPolicy());
        } catch (TosClientException e) {
            System.out.println("preSignedPostSignature failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (Throwable t) {
            System.out.println("preSignedPostSignature failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For detailed information about POST form presigning, see [Including a signature in browser-based upload forms](https://docs.byteplus.com/docs/tos/reference-browser-based-upload-forms-include-signatures).
