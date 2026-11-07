---
title: "List Hierarchical Namespaces (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-hierarchical-namespaces-java-sdk"
---

Hierarchical NameSpace (HNS), abbreviated as hierarchical bucket, is a brand\-new bucket type introduced by TOS Object Storage that is based on hierarchical metadata management. Besides its hierarchical namespace features, a HNS bucket can scale as much as a FNS bucket. It also delivers seamless interoperability between object and file semantics. This allows **data to be accessed through multiple protocols**, so you can process data more efficiently.

Compared to the original flat namespace (FNS, Flat NameSpace, also known as flat bucket), this approach provides strong support for directory\-level mv and rename operations, while also optimizing common read operations such as List and directory Head. These enhancements improve data processing efficiency and performance, making it well suited to usage scenarios in big data, data lake, and AI fields.

This document describes how to use the TOS Java SDK `listBuckets` interface to enumerate the hierarchical namespace lists for all regions under your account.

<span id="5bdeaa67"></span>
## **Category**


* Before listing buckets, you must have the `tos:ListBuckets` permission. For detailed procedures, please refer to the [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

* This interface returns all buckets in all regions for the current account.


<span id="0aba5259"></span>
## **Sample Code**

The following code demonstrates how to enumerate hierarchical namespaces across all regions for the current account.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.ListBucketsV2Input;
import com.volcengine.tos.model.bucket.ListBucketsV2Output;
import com.volcengine.tos.model.bucket.ListedBucket;

public class ListBucketExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            ListBucketsV2Input input = new ListBucketsV2Input();
            input.setBucketType(BucketType.BUCKET_TYPE_HNS);
            ListBucketsV2Output output = tos.listBuckets(input);
            System.out.println("bucket owner is " + output.getOwner());
            if (output.getBuckets() != null) {
                System.out.println("you have listed " + output.getBuckets().size() + " buckets");
                for (int i = 0; i < output.getBuckets().size(); i++){
                    ListedBucket bucket = output.getBuckets().get(i);
                    System.out.printf("Listed bucket, name is %s, location is %s, extranetEndpoint is %s, " +
                            "intranetEndpoint is %s, creationDate is %s.\n", bucket.getName(), bucket.getLocation(),
                            bucket.getExtranetEndpoint(), bucket.getIntranetEndpoint(), bucket.getCreationDate());
                }
            } else {
                System.out.println("there are no buckets in your account.");
            }
        } catch (TosClientException e) {
            System.out.println("listBuckets failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("listBuckets failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("listBuckets failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="8e80b50f"></span>
## **Related documentation**

For API documentation on listing buckets, see [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
