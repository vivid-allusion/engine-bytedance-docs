---
title: "Managing Mirroring Rules (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-image-return-to-source-java-sdk"
---

A bucket is the globally unique namespace in TOS, functioning as a data container for storing object data. When the requested object data does not exist in the bucket, TOS returns a 404 error by default. However, if you configure the bucket's back\-to\-origin rule and enter the correct object data address, TOS will obtain data from the origin site using the origin retrieval rule. TOS supports both mirror\-based (mirroring) and redirect\-based (redirection) back\-to\-origin, enabling you to meet requirements such as hot data migration and redirection of specific requests.

This article describes how to manage bucket back\-to\-origin rules using the TOS Java SDK.

<span id=".6K6-572u6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## **Configure mirroring rules**

You can set the mirroring rule for a specified bucket through the `putBucketMirrorBack` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To configure mirroring rules for a bucket, you must be the bucket owner.</div>


* <div data-tips="true" data-tips-type="warning">Each bucket supports the creation of only one back\-to\-origin rule.</div>


* <div data-tips="true" data-tips-type="warning">Mirroring supports objects up to a maximum size of 5 GiB. If you need to request objects larger than 5 GiB, please use the Get Range feature.</div>


* <div data-tips="true" data-tips-type="warning">The maximum supported size for redirection is 300 GiB.</div>


* <div data-tips="true" data-tips-type="warning">For more information about mirroring, see <a href="https://docs.byteplus.com/docs/tos/Overview9">Configuring back\-to\-origin rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to configure the mirroring rule for a specified bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.RedirectType;
import com.volcengine.tos.model.bucket.*;

import java.util.ArrayList;
import java.util.List;

public class PutBucketMirrorBackExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            Condition condition = new Condition().setHttpCode(404);
            List<String> passList = new ArrayList<>();
            passList.add("pass_header1");
            passList.add("pass_header2");
            List<String> removeList = new ArrayList<>();
            removeList.add("remove_header1");
            removeList.add("remove_header2");
            MirrorHeader mirrorHeader = new MirrorHeader().setPassAll(true)
                    .setPass(passList).setRemove(removeList);

            List<String> primary = new ArrayList<>();
            primary.add("http://www.volcengine.com/obj/tostest/1");
            List<String> follower = new ArrayList<>();
            follower.add("http://www.volcengine.com/obj/tostest/2");
            SourceEndpoint sourceEndpoint = new SourceEndpoint().setPrimary(primary).setFollower(follower);
            PublicSource publicSource = new PublicSource().setSourceEndpoint(sourceEndpoint);
            Redirect redirect = new Redirect()
                    .setRedirectType(RedirectType.REDIRECT_MIRROR)
                    .setFetchSourceOnRedirect(true)
                    .setPassQuery(true)
                    .setFollowRedirect(true)
                    .setMirrorHeader(mirrorHeader)
                    .setPublicSource(publicSource);
            MirrorBackRule rule = new MirrorBackRule().setId("1").setCondition(condition).setRedirect(redirect);
            List<MirrorBackRule> rules = new ArrayList<>();
            rules.add(rule);
            PutBucketMirrorBackInput input = new PutBucketMirrorBackInput().setBucket(bucketName).setRules(rules);
            PutBucketMirrorBackOutput output = tos.putBucketMirrorBack(input);
            System.out.println("putBucketMirrorBack succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketMirrorBack failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketMirrorBack failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketMirrorBack failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## **Retrieve mirroring rules**

You can use the `getBucketMirrorBack` interface of the TOS Java SDK to obtain the current mirroring rules configured for the specified bucket.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To obtain the mirroring rules for a bucket, you must be the bucket owner.</div>


* <div data-tips="true" data-tips-type="warning">For more information about mirroring, see <a href="https://docs.byteplus.com/docs/tos/Overview9">Configuring back\-to\-origin rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to retrieve the mirroring rules for a specified bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketMirrorBackInput;
import com.volcengine.tos.model.bucket.GetBucketMirrorBackOutput;
import com.volcengine.tos.model.bucket.MirrorBackRule;

public class GetBucketMirrorBackExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketMirrorBackInput input = new GetBucketMirrorBackInput().setBucket(bucketName);
            GetBucketMirrorBackOutput output = tos.getBucketMirrorBack(input);
            System.out.println("getBucketMirrorBack succeed");
            if (output.getRules() != null) {
                System.out.println("this bucket has " + output.getRules().size() + " mirror back rules");
                for (int i = 0; i < output.getRules().size(); i++){
                    MirrorBackRule rule = output.getRules().get(i);
                    System.out.println("No." + (i+1) + " rule is " + rule.toString());
                }
            }
        } catch (TosClientException e) {
            System.out.println("getBucketMirrorBack failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketMirrorBack failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketMirrorBack failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk5qG255qE6ZWc5YOP5Zue5rqQ6KeE5YiZ"></span>
## **Delete mirroring rules**

You can use the `deleteBucketMirrorBack` interface of the TOS Java SDK to delete the currently configured mirroring rule for a specified bucket.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To delete a bucket's mirroring rule, you must be the bucket owner.</div>


* <div data-tips="true" data-tips-type="warning">For more information about mirroring, see <a href="https://docs.byteplus.com/docs/tos/Overview9">Configuring back\-to\-origin rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to delete the mirroring rule for a specified bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketMirrorBackInput;
import com.volcengine.tos.model.bucket.DeleteBucketMirrorBackOutput;

public class DeleteBucketMirrorBackExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketMirrorBackInput input = new DeleteBucketMirrorBackInput().setBucket(bucketName);
            DeleteBucketMirrorBackOutput output = tos.deleteBucketMirrorBack(input);
            System.out.println("deleteBucketMirrorBack succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucketMirrorBack failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucketMirrorBack failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucketMirrorBack failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information about mirroring, see [Configuring back-to-origin rules](https://docs.byteplus.com/docs/tos/Overview9).
