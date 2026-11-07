---
title: "Managing Cross-Region Replication (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-region-replication-java-sdk"
---

TOS supports cross\-region replication (CRR), which enables you to copy objects from one bucket to another in different regions. After configuring CRR rules, when you upload a new object to the source bucket, TOS will automatically synchronize the object to the destination bucket. This feature is designed to meet the requirements for remote disaster recovery and data replication.

<span id=".6K6-572u6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## **Configure CRR rules**

You can configure CRR rules for a specified bucket through the TOS Java SDK's `putBucketReplication` interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
### **Notes**


* The corresponding objects will be synchronized only after CRR rules have been configured.

* CRR utilizes an asynchronous replication mechanism. Depending on the size of your objects, the process may take anywhere from several minutes to several hours.

* A maximum of 100 CRR rules can be created for a single bucket.

* CRR can be enabled only if the versioning status of the source bucket and the destination bucket is the same.

* To configure CRR rules for a bucket, you must be the bucket owner.

* For more information on configuring CRR rules, see [Cross-region replication rules](https://docs.byteplus.com/docs/tos/Cross-regional-replication-within-the-same-account).


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to configure CRR rules for a specified bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.StatusType;
import com.volcengine.tos.comm.common.StorageClassInheritDirectiveType;
import com.volcengine.tos.model.bucket.Destination;
import com.volcengine.tos.model.bucket.PutBucketReplicationInput;
import com.volcengine.tos.model.bucket.PutBucketReplicationOutput;
import com.volcengine.tos.model.bucket.ReplicationRule;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class PutBucketReplicationExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";

        String destinationRegion = "your destination region";
        String destinationBucket = "your destination bucket";
        String role = "your role";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            ReplicationRule rule = new ReplicationRule()
                    .setId("1")
                    .setStatus(StatusType.STATUS_ENABLED)
                    .setPrefixSet(Arrays.asList("prefix1", "prefix2"))
                    .setDestination(new Destination()
                            .setBucket(destinationBucket).setLocation(destinationRegion)
                            .setStorageClassInheritDirectiveType(StorageClassInheritDirectiveType.STORAGE_CLASS_ID_SOURCE_OBJECT))
                    .setHistoricalObjectReplication(StatusType.STATUS_DISABLED);
            List<ReplicationRule> rules = new ArrayList<>();
            rules.add(rule);
            PutBucketReplicationInput input = new PutBucketReplicationInput().setBucket(bucketName).setRules(rules).setRole(role);
            PutBucketReplicationOutput output = tos.putBucketReplication(input);
            System.out.println("putBucketReplication succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketReplication failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketReplication failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketReplication failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5p-l55yL6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## **View CRR rules**

You can obtain the CRR rules configured for a specified bucket through the `getBucketReplication` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain the CRR rules for a bucket, you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to retrieve the CRR rules for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketReplicationInput;
import com.volcengine.tos.model.bucket.GetBucketReplicationOutput;
import com.volcengine.tos.model.bucket.ReplicationRule;

public class GetBucketReplicationExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketReplicationInput input = new GetBucketReplicationInput().setBucket(bucketName);
            GetBucketReplicationOutput output = tos.getBucketReplication(input);
            if (output.getRules() != null && output.getRules().size() > 0) {
                for (int i = 0; i < output.getRules().size(); i++){
                    ReplicationRule rule = output.getRules().get(i);
                    System.out.println("rule id:" + rule.getId());
                    System.out.println("rule status:" + rule.getStatus());
                    for (String prefix : rule.getPrefixSet()) {
                        System.out.println("rule prefix:" + prefix);
                    }
                    System.out.println("rule dst bucket:" + rule.getDestination().getBucket());
                    System.out.println("rule dst location:" + rule.getDestination().getLocation());
                    System.out.println("rule dst storage class:" + rule.getDestination().getStorageClass());
                    System.out.println("rule dst storage class inherit directive:" +
                            rule.getDestination().getStorageClassInheritDirectiveType());
                }
            }
        } catch (TosClientException e) {
            System.out.println("getBucketLocation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketLocation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketLocation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5p-l55yL6Leo5Yy65Z-f5aSN5Yi26L-b5bqm"></span>
## **View CRR progress**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To obtain the CRR progress of a bucket, you must be the bucket owner.</div>


* <div data-tips="true" data-tips-type="warning">The progress of historical data replication is represented as a percentage and is only applicable to storage spaces with historical data replication enabled.</div>


* <div data-tips="true" data-tips-type="warning">The replication progress of newly written data is indicated by the timestamp of the newly written data.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to retrieve the CRR progress of a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketReplicationInput;
import com.volcengine.tos.model.bucket.GetBucketReplicationOutput;
import com.volcengine.tos.model.bucket.ReplicationRule;

public class GetBucketReplicationByRuleIdExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "bucket-example";

        String ruleId = "the specific rule id";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketReplicationInput input = new GetBucketReplicationInput().setBucket(bucketName).setRuleID(ruleId);
            GetBucketReplicationOutput output = tos.getBucketReplication(input);
            if (output.getRules() != null && output.getRules().size() > 0) {
                for (int i = 0; i < output.getRules().size(); i++){
                    ReplicationRule rule = output.getRules().get(i);
                    System.out.println("rule id:" + rule.getId());
                    System.out.println("rule historical object:" + rule.getProgress().getHistoricalObject());
                    System.out.println("rule new object:" + rule.getProgress().getNewObject());
                }
            }
        } catch (TosClientException e) {
            System.out.println("getBucketLocation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketLocation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketLocation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## **Delete CRR rules**

You can use the `deleteBucketReplication` interface of the TOS Java SDK to delete CRR rules configured for a specified bucket.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete a bucket's CRR rule, you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code demonstrates how to delete CRR rules for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketReplicationInput;
import com.volcengine.tos.model.bucket.DeleteBucketReplicationOutput;

public class DeleteBucketReplicationExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 
        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketReplicationInput input = new DeleteBucketReplicationInput().setBucket(bucketName);
            DeleteBucketReplicationOutput output = tos.deleteBucketReplication(input);
            System.out.println("deleteBucketReplication succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucketReplication failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucketReplication failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucketReplication failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
 

}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For more information on configuring CRR rules, see [Cross-region replication rules](https://docs.byteplus.com/docs/tos/Cross-regional-replication-within-the-same-account).
