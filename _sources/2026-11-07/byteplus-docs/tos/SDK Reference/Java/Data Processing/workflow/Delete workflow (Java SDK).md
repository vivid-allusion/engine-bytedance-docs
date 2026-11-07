---
title: "Delete workflow (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306574"
---

This article explains how to delete a workflow using the TOS Java SDK.

<span id="2404ed90"></span>
## Notes

Only Java SDK version 2.9.8 and above support the delete workflow feature.

<span id="5504565a"></span>
## Code examples

```java
// Delete transcoding workflow
package org.example.DeleteConvertWorkflow;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class DeleteConvertWorkflowExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // Fill in BucketName
        String bucketName = System.getenv("TOS_BUCKET");
        
        // Initialize client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // To construct a delete transcoding workflow, The input parameters only need to specify the bucket in which the workflow resides.
            // Note: If a transcoding workflow is already configured in the bucket, Calling this API will delete the transcoding workflow configuration for the current bucket.
            DeleteConvertWorkflowInput input = DeleteConvertWorkflowInput.builder()
                    .bucket(bucketName)
                    .build();
            
            // Call the Deletion Transcoding Workflow API
            DeleteConvertWorkflowOutput output = tos.deleteConvertWorkflow(input);
            
            //Process the returned results, And print the request ID and HTTP status code for easy troubleshooting and confirmation.
            System.out.println("Successfully deleted transcoding workflow");
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            
        } catch (TosClientException e) {
            // Operation failed, and a client-side exception was caught. This usually indicates an incorrect request parameter, meaning the request was never sent.
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed，By capturing server-side exceptions, You can obtain detailed error information returned by the server.
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // As a fallback to catch other exceptions, Execution usually doesn't stop here.
            System.out.println("Operation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="eb8b4f63"></span>
## Related documentation

For APIs related to querying workflows, see [DeleteWorkflow](https://docs.byteplus.com/docs/tos/DeleteWorkflow).
