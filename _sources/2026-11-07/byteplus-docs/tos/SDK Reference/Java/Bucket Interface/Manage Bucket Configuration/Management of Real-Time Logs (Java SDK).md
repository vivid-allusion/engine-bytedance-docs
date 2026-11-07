---
title: "Management of Real-Time Logs (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-real-time-logs-java-sdk"
---

TOS supports log analysis functionality and enables you to retrieve and analyze access logs generated during your interactions with TOS via the log service. You can configure log analysis settings using the TOS Java SDK.

<span id=".6K6-572u5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Configure real\-time log configuration rules**

You can configure real\-time log settings for a bucket using the `putBucketRealTimeLog` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To use the log analysis feature, you must have enabled the log service feature and authorized TOS to access Volcengine Log Service (TLS).</div>


* <div data-tips="true" data-tips-type="warning">After the log analysis feature is enabled, the log service will automatically create log projects and topics to store logs related to TOS.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to configure real\-time log configuration rules for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.AccessLogConfiguration;
import com.volcengine.tos.model.bucket.PutBucketRealTimeLogInput;
import com.volcengine.tos.model.bucket.PutBucketRealTimeLogOutput;
import com.volcengine.tos.model.bucket.RealTimeLogConfiguration;

public class PutBucketRealTimeLogExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";

        String realTimeLogRole = "your real time log role";
        String tlsProjectId = "the tls project id";
        String tlsTopicId = "the tls topic id";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            RealTimeLogConfiguration configuration = new RealTimeLogConfiguration().setRole(realTimeLogRole)
                    .setConfiguration(new AccessLogConfiguration()
                            .setUseServiceTopic(true)
                            .setTlsProjectID(tlsProjectId)
                            .setTlsTopicID(tlsTopicId));
            PutBucketRealTimeLogInput input = new PutBucketRealTimeLogInput().setBucket(bucketName)
                    .setConfiguration(configuration);
            PutBucketRealTimeLogOutput output = tos.putBucketRealTimeLog(input);
            System.out.println("putBucketRealTimeLog succeed");
        } catch (TosClientException e) {
            System.out.println("putBucketRealTimeLog failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("putBucketRealTimeLog failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("putBucketRealTimeLog failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".6I635Y-W5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Retrieve Real\-Time Log Configuration Rules**

You can obtain the real\-time log configuration of a bucket through the `getBucketRealTimeLog` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To access the real\-time log configuration rules of a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to retrieve the real\-time log configuration rules for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.GetBucketRealTimeLogInput;
import com.volcengine.tos.model.bucket.GetBucketRealTimeLogOutput;

public class GetBucketRealTimeLogExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 

        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            GetBucketRealTimeLogInput input = new GetBucketRealTimeLogInput().setBucket(bucketName);
            GetBucketRealTimeLogOutput output = tos.getBucketRealTimeLog(input);
            System.out.println("getBucketRealTimeLog succeed, the config is " + output.getConfiguration());
        } catch (TosClientException e) {
            System.out.println("getBucketRealTimeLog failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("getBucketRealTimeLog failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("getBucketRealTimeLog failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".5Yig6Zmk5a6e5pe25pel5b-X6YWN572u6KeE5YiZ"></span>
## **Delete Real\-Time Log Configuration Rules**

You can delete the real\-time log configuration of a bucket through the `deleteBucketRealTimeLog` interface of the TOS Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To delete the real\-time log configuration rules of a bucket, you must, by default, be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample Code**

The following code demonstrates how to delete real\-time log configuration rules for a bucket.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketRealTimeLogInput;
import com.volcengine.tos.model.bucket.DeleteBucketRealTimeLogOutput;

public class DeleteBucketRealTimeLogExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY"); 
        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketRealTimeLogInput input = new DeleteBucketRealTimeLogInput().setBucket(bucketName);
            DeleteBucketRealTimeLogOutput output = tos.deleteBucketRealTimeLog(input);
            System.out.println("deleteBucketRealTimeLog succeed, " + output);
        } catch (TosClientException e) {
            System.out.println("deleteBucketRealTimeLog failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("deleteBucketRealTimeLog failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("deleteBucketRealTimeLog failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information about real\-time log configuration, see [Log Analysis](https://docs.byteplus.com/docs/tos/Log-analysis).
