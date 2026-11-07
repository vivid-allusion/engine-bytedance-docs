---
title: "Delete audio transcoding template (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306569"
---

This article explains how to delete an audio transcoding template using the TOS Java SDK.

<span id="0a52cb07"></span>
## Notes

Only Java SDK version 2.9.8 and above support deleting audio transcoding templates.

<span id="bf30a1d0"></span>
## Code examples

```Java
// Delete audio transcoding template
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class DeleteAudioConvertTemplateExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // Provide your bucket name
        String bucketName = System.getenv("TOS_BUCKET");
        
        // Initialize the client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // Set the audio transcoding template ID to be deleted
            String templateId = "65653537313835383563611601527c28a07e";
            
            // Build the input parameters for deleting the audio transcoding template
            DeleteAudioConvertTemplateInput input = DeleteAudioConvertTemplateInput.builder()
                    .bucket(bucketName)
                    .id(templateId)
                    .build();
            
            // Call the delete audio transcoding template API
            DeleteAudioConvertTemplateOutput output = tos.deleteAudioConvertTemplate(input);
            
            // Process the returned result
            System.out.println("Audio transcoding template successfully deleted");
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            
        } catch (TosClientException e) {
            // Operation failed: caught a client exception, usually due to invalid request parameters or the request was not sent
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed: caught a server exception, detailed error information can be obtained from the server response
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Catch all other exceptions as a fallback, normally this will not be executed
            System.out.println("Operation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="d5b57a77"></span>
## **Related documentation**

For API interfaces related to deleting audio transcoding templates, see [DeleteAudioConvertTemplates](https://docs.byteplus.com/docs/tos/DeleteAudioConvertTemplates).
