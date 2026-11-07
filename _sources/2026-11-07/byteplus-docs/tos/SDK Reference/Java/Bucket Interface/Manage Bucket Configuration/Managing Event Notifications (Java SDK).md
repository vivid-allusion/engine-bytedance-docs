---
title: "Managing Event Notifications (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-event-notifications-java-sdk"
---

TOS can deliver notifications for certain event changes to BytePlus Function Service (veFaaS). You can configure event notification rules to monitor changes to resources in TOS in real time. This article presents sample code for event notification.

Learn more in [What is veFaaS](https://docs.byteplus.com/en/docs/faas/What_is_Function_Service).

<span id=".6K6-572u5LqL5Lu26YCa55-l6KeE5YiZ"></span>
## **Configure Event Notification Rules**

You can configure event notification rules for a specified bucket through the `putBucketNotification` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To configure event notification rules for a bucket, you must be the bucket Owner.</div>


* <div data-tips="true" data-tips-type="warning">Configuring event notifications depends on the function service. You need to create and publish a function service in <a href="https://www.byteplus.com/en/product/vefaas">BytePlus</a> in advance.</div>


* <div data-tips="true" data-tips-type="warning">A maximum of 10 event notification rules can be created for a single bucket.</div>


* <div data-tips="true" data-tips-type="warning">An event notification rule can specify only one push target, which must be a function service.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to configure event notification rules for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.*;

import java.util.ArrayList;
import java.util.List;

public class PutBucketNotificationExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";

        String id = "event notification id";
        String cloudFunction = "your cloud function";

        String event = "tos:ObjectCreated:Put";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            List<String> events = new ArrayList<>();
            events.add(event);
            FilterRule rule = new FilterRule().setName("prefix").setValue("test-");
            List<FilterRule> rules = new ArrayList<>();
            rules.add(rule);
            Filter filter = new Filter().setKey(new FilterKey().setRules(rules));
            CloudFunctionConfiguration configuration = new CloudFunctionConfiguration()
                    .setId(id).setCloudFunction(cloudFunction)
                    .setEvents(events)
                    .setFilter(filter);
            List<CloudFunctionConfiguration> configurations = new ArrayList<>();
            configurations.add(configuration);
            PutBucketNotificationInput input = new PutBucketNotificationInput().setBucket(bucketName)
                    .setCloudFunctionConfigurations(configurations);
            PutBucketNotificationOutput output = tos.putBucketNotification(input);
            System.out.println("putBucketNotification succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketNotification failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketNotification failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketNotification failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W5LqL5Lu26YCa55-l6KeE5YiZ"></span>
## **Retrieve Event Notification Rules**

You can obtain the event notification rules configured for a specified bucket through the TOS Java SDK's `getBucketNotification` interface.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">By default, you must be the bucket owner to retrieve the event notification rules for a bucket.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to retrieve the event notification rules for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.CloudFunctionConfiguration;
import com.volcengine.tos.model.bucket.GetBucketNotificationInput;
import com.volcengine.tos.model.bucket.GetBucketNotificationOutput;

public class GetBucketNotificationExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketNotificationInput input = new GetBucketNotificationInput().setBucket(bucketName);
            GetBucketNotificationOutput output = tos.getBucketNotification(input);
            System.out.println("getBucketNotification succeed");
            if (output.getCloudFunctionConfiguration() != null) {
                System.out.println("this bucket has " + output.getCloudFunctionConfiguration().size() + " notification rules");
                for (int i = 0; i < output.getCloudFunctionConfiguration().size(); i++){
                    CloudFunctionConfiguration conf = output.getCloudFunctionConfiguration().get(i);
                    System.out.println("Cloud Function Configuration ID:" + conf.getId());
                    if (conf.getEvents() != null && conf.getEvents().size() > 0) {
                        for(int j = 0; j < conf.getEvents().size(); j++) {
                            System.out.println("Cloud Function Configuration Events " + j + " is " + conf.getEvents().get(j));
                        }
                    }
                    System.out.println("Cloud Function Configuration Filter " + conf.getFilter());
                    System.out.println("Cloud Function Configuration CloudFunction " + conf.getCloudFunction());
                }
            }
        } catch (TosClientException e) {
            System.out.println("getBucketNotification failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketNotification failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketNotification failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information about event notification configuration, see [Event Notification](https://docs.byteplus.com/docs/tos/Event-notification-overview).
