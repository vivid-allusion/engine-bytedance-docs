---
title: "Managing Static Websites (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-static-websites-java-sdk"
---

You can use TOS to host a static website. First, store all contents of the website in a TOS bucket. Next, configure rules to host the website so that it can be accessed via the bucket's domain name.

<span id=".6K6-572u572R56uZ6YWN572u6KeE5YiZ"></span>
## **Set Website Configuration Rules**

You can configure website configuration rules for a specified bucket using the `putBucketWebsite` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Each bucket can only contain one static website hosting rule.</div>


* <div data-tips="true" data-tips-type="warning">A hosting rule will not take effect until you associate a custom domain with the bucket. For instructions, see <a href="https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name">Associating a custom domain</a>.</div>


* <div data-tips="true" data-tips-type="warning">Starting from October 18, 2022, for security and compliance reasons, if you use the bucket's default domain to access web page files with the MIME type text/html and extensions including .htm, .html, .jsp, .plg, .htx, and .stm, the response header will automatically include <code>Content-Disposition:attachment</code>. This means that, when you access web page files via a browser, the website will not preview the content directly. Instead, the content will be downloaded locally.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates two scenarios: how to configure redirection for all requests to another site, and how to set specific redirection rules to redirect particular requests.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.ProtocolType;
import com.volcengine.tos.model.bucket.*;

import java.util.ArrayList;
import java.util.List;

public class PutBucketWebsiteExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            RedirectAllRequestsTo redirectAllRequestsTo = new RedirectAllRequestsTo().setHostname("www.example.com").setProtocol("http");
            PutBucketWebsiteInput input = new PutBucketWebsiteInput().setBucket(bucketName)
                    .setRedirectAllRequestsTo(redirectAllRequestsTo);
            PutBucketWebsiteOutput output = tos.putBucketWebsite(input);
            System.out.println("putBucketWebsite succeed");

            RoutingRule rule = new RoutingRule()
                    .setCondition(new RoutingRuleCondition()
                            .setKeyPrefixEquals("prefix")
                            .setHttpErrorCodeReturnedEquals(404))
                    .setRedirect(new RoutingRuleRedirect()
                            .setProtocol(ProtocolType.PROTOCOL_HTTP)
                            .setHostname("www.redirect.com"));
            List<RoutingRule> rules = new ArrayList<>();
            rules.add(rule);
            IndexDocument indexDocument = new IndexDocument().setSuffix("index.html").setForbiddenSubDir(true);
            ErrorDocument errorDocument = new ErrorDocument().setKey("error.html");
            input = new PutBucketWebsiteInput().setBucket(bucketName)
                    .setRoutingRules(rules)
                    .setIndexDocument(indexDocument)
                    .setErrorDocument(errorDocument);
            output = tos.putBucketWebsite(input);
            System.out.println("putBucketWebsite succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketWebsite failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketWebsite failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketWebsite failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W572R56uZ6YWN572u6KeE5YiZ"></span>
## **Retrieve website configuration rules**

You can obtain the website configuration rules for a specified bucket through the `getBucketWebsite` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the website configuration rules for a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to retrieve the website configuration rules of a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.*;

public class GetBucketWebsiteExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketWebsiteInput input = new GetBucketWebsiteInput().setBucket(bucketName);
            GetBucketWebsiteOutput output = tos.getBucketWebsite(input);
            System.out.println("getBucketWebsite succeed");
            if (output.getRedirectAllRequestsTo() != null) {
                System.out.println("getBucketWebsite RedirectAllRequestsTo HostName:" + output.getRedirectAllRequestsTo().getHostname());
                System.out.println("getBucketWebsite RedirectAllRequestsTo Protocol:" + output.getRedirectAllRequestsTo().getProtocol());
            }
            if (output.getIndexDocument() != null) {
                System.out.println("getBucketWebsite IndexDocument ForbiddenSubDir:" + output.getIndexDocument().isForbiddenSubDir());
                System.out.println("getBucketWebsite IndexDocument Suffix:" + output.getIndexDocument().getSuffix());
            }
            if (output.getErrorDocument() != null) {
                System.out.println("getBucketWebsite ErrorDocument Key:" + output.getErrorDocument().getKey());
            }
            if (output.getRoutingRules() != null && output.getRoutingRules().size() > 0) {
                for(int i = 0; i < output.getRoutingRules().size(); i++) {
                    RoutingRule rule = output.getRoutingRules().get(i);
                    System.out.println("No." + i + " rule");
                    if (rule.getCondition() != null) {
                        System.out.println("getBucketWebsite RoutingRules Rule Condition HttpErrorCodeReturnedEquals:" + rule.getCondition().getHttpErrorCodeReturnedEquals());
                        System.out.println("getBucketWebsite RoutingRules Rule Condition KeyPrefixEquals:" + rule.getCondition().getKeyPrefixEquals());
                    }
                    if (rule.getRedirect() != null) {
                        System.out.println("getBucketWebsite RoutingRules Rule Redirect HostName:" + rule.getRedirect().getHostname());
                        System.out.println("getBucketWebsite RoutingRules Rule Redirect Protocol:" + rule.getRedirect().getProtocol());
                        System.out.println("getBucketWebsite RoutingRules Rule Redirect ReplaceKeyWith:" + rule.getRedirect().getReplaceKeyWith());
                        System.out.println("getBucketWebsite RoutingRules Rule Redirect ReplaceKeyPrefixWith:" + rule.getRedirect().getReplaceKeyPrefixWith());
                        System.out.println("getBucketWebsite RoutingRules Rule Redirect HttpRedirectCode:" + rule.getRedirect().getHttpRedirectCode());
                    }
                }
            }
        } catch (TosClientException e) {
            System.out.println("getBucketWebsite failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketWebsite failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketWebsite failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk572R56uZ6YWN572u6KeE5YiZ"></span>
## **Delete Website Configuration Rules**

You can delete the website configuration rules of a specified bucket through the TOS Java SDK `deleteBucketWebsite` interface.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete a bucket's website configuration rule, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to delete a website configuration rule from a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketWebsiteInput;
import com.volcengine.tos.model.bucket.DeleteBucketWebsiteOutput;

public class DeleteBucketWebsiteExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 
        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketWebsiteInput input = new DeleteBucketWebsiteInput().setBucket(bucketName);
            DeleteBucketWebsiteOutput output = tos.deleteBucketWebsite(input);
            System.out.println("deleteBucketWebsite succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucketWebsite failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucketWebsite failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucketWebsite failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information on configuring static website settings, see [Static Website Setup](https://docs.byteplus.com/docs/tos/Set-up-a-static-website).
