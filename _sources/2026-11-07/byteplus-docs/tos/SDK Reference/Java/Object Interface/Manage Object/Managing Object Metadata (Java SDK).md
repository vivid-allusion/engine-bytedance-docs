---
title: "Managing Object Metadata (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-metadata-java-sdk"
---

Object metadata is a description of an object's properties and includes two types: HTTP standard attributes (HTTP Header) and user\-defined metadata (User Meta). The TOS Java SDK supports setting metadata for individual objects and viewing object metadata information.

<span id=".6K6-572u5a-56LGh5YWD5pWw5o2u"></span>
## **Configure Object Metadata**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To set object metadata, your account must have the <code>tos:PutObject</code> permission. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


You can set object metadata directly during object upload, or, after the upload is complete, use the TOS Java SDK `setObjectMeta` interface to set metadata for existing objects.

<span id=".5LiK5Lyg5a-56LGh5pe26K6-572u5a-56LGh5YWD5pWw5o2u"></span>
### **Setting object metadata when uploading objects**


* To set object metadata during a standard upload, see [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-java-sdk).

* To set object metadata during append upload, please refer to [Append Upload](https://docs.byteplus.com/docs/tos/Append-upload-java-sdk).

* To set object metadata during multipart upload, see [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-java-sdk).

* To set object metadata during object copying, refer to [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-java-sdk).

* To set object metadata during multipart copy operations, see [Multipart Copy](https://docs.byteplus.com/docs/tos/Shard-copy-java-sdk).


<span id=".6YCa6L-HLXNldG9iamVjdG1ldGEt6K6-572u"></span>
### **Approved** **`setObjectMeta`** ** setting**

The `setObjectMeta` interface of the TOS Java SDK supports setting HTTP headers and custom metadata headers for objects.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following code demonstrates how to configure the settings. All parameter values are provided for reference only; please configure them according to your actual business needs.</div>


```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;
import com.volcengine.tos.model.object.SetObjectMetaInput;
import com.volcengine.tos.model.object.SetObjectMetaOutput;

import java.util.HashMap;
import java.util.Map;

public class SetObjectMetaExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            ObjectMetaRequestOptions options = new ObjectMetaRequestOptions();

            options.setContentType("text/plain");
            options.setContentDisposition("attachment; filename=\"DownloadFileName\"");
            options.setCacheControl("no-cache");

            Map<String, String> customMeta = new HashMap<>();
            customMeta.put("userCustomKey", "userCustomValue");
            options.setCustomMetadata(customMeta);

            SetObjectMetaInput input = new SetObjectMetaInput().setBucket(bucketName).setKey(objectKey).setOptions(options);
            SetObjectMetaOutput output = tos.setObjectMeta(input);
            System.out.println("setObjectMeta succeed");
        } catch (TosClientException e) {
            System.out.println("setObjectMeta failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("setObjectMeta failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("setObjectMeta failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Related documentation**

See [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta) for the API interface to set object metadata.

<span id=".6I635Y-W5a-56LGh5YWD5pWw5o2u"></span>
## **Retrieving Object Metadata**

You can obtain object metadata through the `headObject` interface of the Java SDK.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To obtain object metadata, your account must have the <code>tos:GetObject</code> permission. For specific instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### Sample Code

The following code demonstrates how to retrieve the metadata of an object.

```java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.HeadObjectV2Input;
import com.volcengine.tos.model.object.HeadObjectV2Output;

import java.util.Map;

public class HeadObjectExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        String bucketName = "bucket-example";
        String objectKey = "example_dir/example_object.txt";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            HeadObjectV2Input input = new HeadObjectV2Input().setBucket(bucketName).setKey(objectKey);
            HeadObjectV2Output output = tos.headObject(input);
            System.out.println("headObject succeed.");
            System.out.println("object's contentType is " + output.getContentType());
            System.out.println("object's etag is " + output.getEtag());
            System.out.println("object's storageClass is " + output.getStorageClass());
            System.out.println("object's contentDisposition is " + output.getContentDisposition());
            System.out.println("object's lastModified is " + output.getLastModified());
            System.out.println("object's cacheControl is " + output.getCacheControl());
            System.out.println("object's contentLength is " + output.getContentLength());
            System.out.println("object's expires is " + output.getExpires());
            System.out.println("object's contentEncoding is " + output.getContentEncoding());
            System.out.println("object's contentLanguage is " + output.getContentLanguage());
            System.out.println("object's version id is " + output.getVersionID());
            if (output.getCustomMetadata() != null && output.getCustomMetadata().size() > 0) {
                System.out.println("object has custom meta data.");
                for (Map.Entry<String, String> custom : output.getCustomMetadata().entrySet()) {
                    System.out.println("object custom meta data key is " + custom.getKey() + ", value is " + custom.getValue());
                }
            }
        } catch (TosClientException e) {
            System.out.println("headObject failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            System.out.println("headObject failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            System.out.println("headObject failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Related documentation**

For information on the API interface for setting object metadata, see [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
