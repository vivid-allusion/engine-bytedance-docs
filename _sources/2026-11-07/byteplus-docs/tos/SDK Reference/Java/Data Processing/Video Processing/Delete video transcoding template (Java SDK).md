---
title: "Delete video transcoding template (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306571"
---

This article explains how to delete a video transcoding template through the TOS Java SDK.

<span id="1d79378d"></span>
## Notes

Only Java SDK version 2.9.8 and above support deleting video transcoding templates.

<span id="2913d5de"></span>
## Code examples

```java
// Delete video transcoding template
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class DeleteVideoConvertTemplateExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // Provide your bucket name
        String bucketName = System.getenv("TOS_BUCKET");
        
        // Provide the video transcoding template ID to delete, read from environment variable TOS_TEMPLATE_ID
        // Template ID can be obtained from the create video transcoding template API response and uniquely identifies a transcoding template
        String templateId = "3233613939376631636358a101**********";
        
        // Initialize the client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // Construct input parameters for deleting a video transcoding template:
            // - Bucket: the storage bucket name where the template is located, must match the bucket used when creating the template
            // - Id: the ID of the video transcoding template to be deleted
            DeleteVideoConvertTemplateInput input = DeleteVideoConvertTemplateInput.builder()
                    .bucket(bucketName)
                    .id(templateId)
                    .build();
            
            // Call the delete video transcoding template API to remove the template with the specified ID
            DeleteVideoConvertTemplateOutput output = tos.deleteVideoConvertTemplate(input);
          
            // Process the response:
            // - RequestID: the unique identifier of this request on the server side, useful for troubleshooting
            // - StatusCode: the HTTP status code, usually 204 indicates successful deletion with no response body
            System.out.println("Video transcoding template successfully deleted");
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            
        } catch (TosClientException e) {
            // Operation failed, client exception caught, usually caused by invalid request parameters, and the request was not sent
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // The operation failed and a server exception was caught. Detailed error information can be obtained from the server response
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Catch all other exceptions as a fallback, this usually does not execute
            System.out.println("Operation failed");
            System.out.println("Unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="50a6f81f"></span>
## Related documentation

For the API related to deleting video transcoding templates, refer to [DeleteVideoConvertTemplate](https://docs.byteplus.com/docs/tos/DeleteVideoConvertTemplate).
