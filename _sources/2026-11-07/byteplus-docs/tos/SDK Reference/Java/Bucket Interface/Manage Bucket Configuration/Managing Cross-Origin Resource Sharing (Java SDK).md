---
title: "Managing Cross-Origin Resource Sharing (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-origin-resource-sharing-java-sdk"
---

A bucket (Bucket) in TOS is a globally unique namespace that functions as a data container for storing object (Object) data. TOS supports configuring Cross\-Origin Resource Sharing (CORS) rules for buckets. When TOS receives a cross\-origin request or an OPTIONS request, it reads the corresponding CORS rules for the bucket, performs the necessary permission checks, and returns the corresponding headers to ensure the security of cross\-origin data transmission. This document describes how to manage cross\-region resource sharing configurations for buckets using the TOS Java SDK.

<span id=".6K6-572u6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## **Configure Cross\-Origin Resource Sharing (CORS) rules**

You can configure cross\-origin resource sharing (CORS) rules for a specified bucket through the `putBucketCORS` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To configure cross\-origin resource sharing rules for a bucket, your account must have the <code>tos:PutBucketCORS</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to configure cross\-origin resource sharing (CORS) rules for a specified bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.*;

import java.util.ArrayList;
import java.util.List;

public class PutBucketCORSExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            List<CORSRule> rules = new ArrayList<>();
            List<String> allowedOrigins = new ArrayList<>();
            allowedOrigins.add("*");
            List<String> allowedMethods = new ArrayList<>();
            allowedMethods.add("GET");
            allowedMethods.add("DELETE");
            allowedMethods.add("PUT");
            List<String> allowedHeaders = new ArrayList<>();
            allowedHeaders.add("Authorization");
            List<String> exposeHeaders = new ArrayList<>();
            exposeHeaders.add("X-TOS-HEADER-1");
            exposeHeaders.add("X-TOS-HEADER-2");
            CORSRule rule1 = new CORSRule()
                    .setAllowedOrigins(allowedOrigins)
                    .setAllowedMethods(allowedMethods)
                    .setAllowedHeaders(allowedHeaders)
                    .setExposeHeaders(exposeHeaders)
                    .setMaxAgeSeconds(3600);
            rules.add(rule1);
            PutBucketCORSInput input = new PutBucketCORSInput().setBucket(bucketName).setRules(rules);
            PutBucketCORSOutput output = tos.putBucketCORS(input);
            System.out.println("putBucketCORS succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketCORS failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketCORS failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketCORS failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## **Retrieve Cross\-Origin Resource Sharing Rules**

You can obtain the Cross\-Origin Resource Sharing (CORS) rules configured for a specified bucket through the `getBucketCORS` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the cross\-origin resource sharing rules for a bucket, your account must have the <code>tos:GetBucketCORS</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to retrieve the cross\-origin resource sharing (CORS) rules for a bucket configuration.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.CORSRule;
import com.volcengine.tos.model.bucket.GetBucketCORSInput;
import com.volcengine.tos.model.bucket.GetBucketCORSOutput;

public class GetBucketCORSExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketCORSInput input = new GetBucketCORSInput().setBucket(bucketName);
            GetBucketCORSOutput output = tos.getBucketCORS(input);
            System.out.println("getBucketCORS succeed");
            if (output.getRules() != null) {
                System.out.println("this bucket has " + output.getRules().size() + " CORS rules");
                for (int i = 0; i < output.getRules().size(); i++){
                    CORSRule rule = output.getRules().get(i);
                    System.out.println("No." + (i+1) + " rule is " + rule.toString());
                }
            }
        } catch (TosClientException e) {
            System.out.println("getBucketCORS failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketCORS failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketCORS failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk6Leo5Z-f6LWE5rqQ5YWx5Lqr6KeE5YiZ"></span>
## **Delete Cross\-Origin Resource Sharing rules**

You can delete the cross\-origin resource sharing (CORS) rules configured for a specified bucket by using the `deleteBucketCORS` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the cross\-origin resource sharing rules of a bucket, your account must have the <code>tos:PutBucketCORS</code> permission. For specific instructions, refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to delete the cross\-origin resource sharing (CORS) rules for a specified bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketCORSInput;
import com.volcengine.tos.model.bucket.DeleteBucketCORSOutput;

public class DeleteBucketCORSExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketCORSInput input = new DeleteBucketCORSInput().setBucket(bucketName);
            DeleteBucketCORSOutput output = tos.deleteBucketCORS(input);
            System.out.println("deleteBucketCORS succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucketCORS failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucketCORS failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucketCORS failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information on Cross\-Origin Resource Sharing, please refer to [Cross-Origin Access Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).
