---
title: "Managing Bucket Lifecycle (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-the-bucket-lifecycle-java-sdk"
---

A Bucket is the globally unique namespace in TOS, functioning as a data container for storing object data. TOS supports configuring Lifecycle rules for buckets, enabling the automatic deletion of expired objects and unmerged parts, or transitioning expired objects to infrequent or archive storage types, thereby reducing user storage costs. This article describes how to manage bucket lifecycle rules using the TOS Java SDK.

<span id=".6K6-572u55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## **Configure lifecycle rules**

You can configure lifecycle rules for a specified bucket through the `putBucketLifecycle` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To configure lifecycle rules for a bucket, your account must have the <code>tos:PutLifecycleConfiguration</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs--overview">Permission configuration overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">If lifecycle rules have already been configured for the specified bucket, performing this operation again will overwrite the existing configuration.</div>


* <div data-tips="true" data-tips-type="warning">To append or modify the lifecycle rules of a specified bucket, first use the Java SDK <code>getBucketLifecycle</code> interface to obtain the current rules of the bucket. Then, append or modify the existing rules as needed, and finally call <code>putBucketLifecycle</code> to update the rules. For instructions on using the <code>getBucketLifecycle</code> interface, please refer to the following sections.</div>


* <div data-tips="true" data-tips-type="warning">For more information about lifecycle rules, see <a href="https://docs.byteplus.com/docs/tos/Lifecycle-rules-overview">Bucket lifecycle rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to configure lifecycle rules for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.StatusType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.bucket.*;

import java.time.LocalDateTime;
import java.time.ZoneOffset;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

public class PutBucketLifecycleExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            List<LifecycleRule> rules = new ArrayList<>();
            LifecycleRule rule1 = new LifecycleRule()
                    .setId("rule1")
                    .setPrefix("test1/")
                    .setStatus(StatusType.STATUS_ENABLED)
                    .setExpiration(new Expiration().setDays(70));
            rules.add(rule1);
            Date expirationDate = Date.from(LocalDateTime.of(2023, 12, 31, 0, 0, 0, 0).toInstant(ZoneOffset.UTC));
            LifecycleRule rule2 = new LifecycleRule()
                    .setId("rule2")
                    .setPrefix("test2/")
                    .setStatus(StatusType.STATUS_ENABLED)
                    .setExpiration(new Expiration().setDate(expirationDate));
            rules.add(rule2);
            AbortInCompleteMultipartUpload abortRule = new AbortInCompleteMultipartUpload().setDaysAfterInitiation(10);
            LifecycleRule rule3 = new LifecycleRule()
                    .setId("rule3")
                    .setPrefix("test3/")
                    .setStatus(StatusType.STATUS_ENABLED)
                    .setAbortInCompleteMultipartUpload(abortRule);
            rules.add(rule3);
            Transition transition = new Transition().setDays(30).setStorageClass(StorageClassType.STORAGE_CLASS_IA);
            List<Transition> transitions = new ArrayList<>();
            transitions.add(transition);
            LifecycleRule rule4 = new LifecycleRule()
                    .setId("rule4")
                    .setPrefix("test4/")
                    .setStatus(StatusType.STATUS_ENABLED)
                    .setTransitions(transitions);
            rules.add(rule4);
            Tag tag = new Tag().setKey("key1").setValue("value1");
            List<Tag> tags = new ArrayList<>();
            tags.add(tag);
            LifecycleRule rule5 = new LifecycleRule()
                    .setId("rule5")
                    .setPrefix("test5/")
                    .setStatus(StatusType.STATUS_ENABLED)
                    .setTransitions(transitions)
                    .setTags(tags);
            rules.add(rule5);
            NoncurrentVersionTransition noncurrentVersionTransition = new NoncurrentVersionTransition().setNoncurrentDays(30)
                    .setStorageClass(StorageClassType.STORAGE_CLASS_IA);
            List<NoncurrentVersionTransition> noncurrentVersionTransitions = new ArrayList<>();
            noncurrentVersionTransitions.add(noncurrentVersionTransition);
            NoncurrentVersionExpiration noncurrentVersionExpiration = new NoncurrentVersionExpiration().setNoncurrentDays(40);
            LifecycleRule rule6 = new LifecycleRule()
                    .setId("rule6")
                    .setPrefix("test6/")
                    .setStatus(StatusType.STATUS_ENABLED)
                    .setExpiration(new Expiration().setDays(70))
                    .setNoncurrentVersionExpiration(noncurrentVersionExpiration)
                    .setNoncurrentVersionTransitions(noncurrentVersionTransitions);
            rules.add(rule6);

            PutBucketLifecycleInput input = new PutBucketLifecycleInput().setBucket(bucketName).setRules(rules);
            PutBucketLifecycleOutput output = tos.putBucketLifecycle(input);
            System.out.println("putBucketLifecycle succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketLifecycle failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketLifecycle failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketLifecycle failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## **Retrieve lifecycle rules**

You can use the TOS Java SDK's `getBucketLifecycle` interface to obtain the lifecycle rules currently configured for a specified bucket.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To retrieve lifecycle rules for a bucket, your account must have the <code>tos:GetLifecycleConfiguration</code> permission. For detailed instructions, refer to <a href="https://docs.byteplus.com/docs/tos/docs--overview">Permission configuration overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information on lifecycle rules, please refer to <a href="https://docs.byteplus.com/docs/tos/Lifecycle-rules-overview">Bucket lifecycle rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to retrieve the lifecycle rules of a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketLifecycleInput;
import com.volcengine.tos.model.bucket.GetBucketLifecycleOutput;
import com.volcengine.tos.model.bucket.LifecycleRule;

public class GetBucketLifecycleExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketLifecycleInput input = new GetBucketLifecycleInput().setBucket(bucketName);
            GetBucketLifecycleOutput output = tos.getBucketLifecycle(input);
            System.out.println("getBucketLifecycle succeed");
            if (output.getRules() != null) {
                System.out.println("this bucket has " + output.getRules().size() + " lifecycle rules");
                for (int i = 0; i < output.getRules().size(); i++){
                    LifecycleRule rule = output.getRules().get(i);
                    System.out.println("No." + (i+1) + " rule is " + rule.toString());
                }
            }
        } catch (TosClientException e) {
            System.out.println("getBucketLifecycle failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketLifecycle failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketLifecycle failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk55Sf5ZG95ZGo5pyf6KeE5YiZ"></span>
## **Delete lifecycle rules**

You can delete the currently configured lifecycle rules for a specified bucket using the `deleteBucketLifecycle` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To delete a bucket lifecycle rule, your account must have the <code>tos:PutLifecycleConfiguration</code> permission. For detailed instructions, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Permission configuration overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">For more information about lifecycle rules, see <a href="https://docs.byteplus.com/docs/tos/Lifecycle-rules-overview">Bucket lifecycle rules</a>.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to delete lifecycle rules from a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketLifecycleInput;
import com.volcengine.tos.model.bucket.DeleteBucketLifecycleOutput;

public class DeleteBucketLifecycleExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "your bucket name";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketLifecycleInput input = new DeleteBucketLifecycleInput().setBucket(bucketName);
            DeleteBucketLifecycleOutput output = tos.deleteBucketLifecycle(input);
            System.out.println("deleteBucketLifecycle succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucketLifecycle failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucketLifecycle failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucketLifecycle failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information about lifecycle rules, see [Setting lifecycle rules](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules).
