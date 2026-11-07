---
title: "Query video transcoding tasks (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306575"
---

This article explains how to query video transcoding tasks using the TOS Java SDK.

<span id="ff66f603"></span>
## Notes

Only Java SDK version 2.9.8 and above support querying video transcoding tasks.

<span id="9762461c"></span>
## Code examples

```Java
// Query video transcoding tasks by ID
package org.example.GetVideoConvertJob;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class GetVideoConvertJobExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
       // Enter BucketName, the name of the bucket where task configurations and results are stored.
        String bucketName = System.getenv("TOS_BUCKET");

        String jobId = "18860c8a52e85836aeb60001253eb055bab7";
        
        // Initialize the client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // Construct the input parameters for querying the video transcoding task
            // bucket is the bucket name used when creating the task.
            // jobId is the task ID returned after the task is created, used to identify the specific video transcoding task.
            GetVideoConvertJobInput input = GetVideoConvertJobInput.builder()
                    .bucket(bucketName)
                    .jobId(jobId)
                    .build();
            
          // Call the API to query video transcoding tasks
            GetVideoConvertJobOutput output = tos.getVideoConvertJob(input);
            
           // Print key return information: Request ID, status code, task ID, task status, error code and error message
            com.volcengine.tos.model.RequestInfo requestInfo = output.getRequestInfo();
            if (requestInfo != null) {
                System.out.println("Video transcoding task successfully checked");
              // RequestID is a unique identifier for this request and can be used to troubleshoot problems.
                System.out.println("RequestID: " + requestInfo.getRequestId());
            // StatusCode is the HTTP status code; 200 indicates a successful request.
                System.out.println("StatusCode: " + requestInfo.getStatusCode());
            }
            // JobID is a unique identifier for the video transcoding task.
            System.out.println("JobID: " + output.getJobID());
            // State Indicates the current status of the task, such as Running, Success, Failed, etc.
            System.out.println("State: " + output.getState());
            // Code / Message This indicates the error code and message when the task fails; a success message is typically 0/OK.
            System.out.println("Code: " + output.getCode());
            System.out.println("Message: " + output.getMessage());
            System.out.println("Callback: " + output.getCallback());
            
            // If the return value contains task input information, then print the task input object.
            ConvertJobInput jobInput = output.getInput();
            if (jobInput != null) {
                System.out.println("\nTask Input:");
                // Object Key, the video source object to be processed
                System.out.println("  Object: " + jobInput.getObject());
            }
            
            // If the return value includes task output information, then print the Region, Bucket, and Object containing the output object.
            ConvertJobOutput jobOutput = output.getOutput();
            if (jobOutput != null) {
                System.out.println("\nTask Output:");
                // Region/Bucket/Object These represent the region, bucket, and object key where the transcoding result is output, respectively.
                System.out.println("  Region: " + jobOutput.getRegion());
                System.out.println("  Bucket: " + jobOutput.getBucket());
                System.out.println("  Object: " + jobOutput.getObject());
            }
            
        } catch (TosClientException e) {
            // Operation failed, and a client-side exception was caught. This usually indicates an incorrect request parameter, meaning the request was never sent.
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // If the operation fails, a server-side exception can be captured, allowing you to obtain detailed error information returned from the server.
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // As a fallback to catch other exceptions, execution usually doesn't stop here.
            System.out.println("Operation failed");
            System.out.println("Unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="c1280ec9"></span>
## Related documentation

For API interfaces related to querying video transcoding tasks, see [QueryMediaJob](https://docs.byteplus.com/docs/tos/QueryMediaJob).
