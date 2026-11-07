---
title: "Query audio transcoding task (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306563"
---

This article describes how to query audio transcoding tasks through the TOS Java SDK.

<span id="e1bf992f"></span>
## Notes

Only Java SDK version 2.9.8 and above support querying audio transcoding tasks.

<span id="18c3fcdb"></span>
## Code examples

```Java
// Audio transcoding task created successfully
package org.example.GetAudioConvertJob;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class GetAudioConvertJobExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        // Enter BucketName, which corresponds to the name of the bucket where task configurations and results are stored.
        String bucketName = System.getenv("TOS_BUCKET");

        // Read the audio transcoding task ID from environment variables, typically returned by the task creation interface.
        String jobId = "1885ff636fc5bb4331c40001834f292e698d";

        // Initialize client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            // Construct input parameters for the query audio transcoding task
            // bucket Bucket name used when creating the task
            // jobId The task ID returned after task creation is used to identify the specific audio transcoding task.
            GetAudioConvertJobInput input = GetAudioConvertJobInput.builder()
                    .bucket(bucketName)
                    .jobId(jobId)
                    .build();

            // Call the audio transcoding task query interface
            GetAudioConvertJobOutput output = tos.getAudioConvertJob(input);

            // Print key return information: Request ID, Status Code, Task ID, Task Status, Error Code and Error Message
            com.volcengine.tos.model.RequestInfo requestInfo = output.getRequestInfo();
            if (requestInfo != null) {
                System.out.println("Audio transcoding task successfully queried");
                System.out.println("RequestID: " + requestInfo.getRequestId());
                System.out.println("StatusCode: " + requestInfo.getStatusCode());
            }
            System.out.println("JobID: " + output.getJobID());
            System.out.println("State: " + output.getState());
            System.out.println("Code: " + output.getCode());
            System.out.println("Message: " + output.getMessage());

            // If the return value contains task input information, then print the task input object.
            ConvertJobInput jobInput = output.getInput();
            if (jobInput != null) {
                System.out.println("\nTask Input:");
                // Object represents the source audio object to be processed. Key
                System.out.println("  Object: " + jobInput.getObject());
            }

            // If the return value includes task output information, then print the Region, Bucket, and Object containing the output object.
            ConvertJobOutput jobOutput = output.getOutput();
            if (jobOutput != null) {
                System.out.println("\nTask Output:");
                // Region/Bucket/Object represent the region, bucket, and object where the transcoding result is output, respectively.
                System.out.println("  Region: " + jobOutput.getRegion());
                System.out.println("  Bucket: " + jobOutput.getBucket());
                System.out.println("  Object: " + jobOutput.getObject());
            }

            // If the return value includes audio transcoding configuration, print the audio transcoding configuration and time range.
            AudioConvertConfig config = output.getAudioConvertConfig();
            if (config != null) {
                System.out.println("\nAudio transcoding configuration AudioConvertConfig:");
                // AudioConvertConfig This indicates the audio transcoding parameter configuration for this task.
                System.out.println("  Container format ContainerFormat: " + config.getContainerFormat());
                System.out.println("  Bitrate BitRate: " + config.getBitRate() + " bps");
                System.out.println("  Sampling format SampleFormat: " + config.getSampleFormat());
                System.out.println("  Sampling rate SampleRate: " + config.getSampleRate() + " Hz");
                System.out.println("  Number of channels Channels: " + config.getChannels());

                // TimeInterval Indicates the start time and duration of an audio clip.
                TimeInterval timeInterval = config.getTimeInterval();
                if (timeInterval != null) {
                    System.out.println("  Time range TimeInterval:");
                    System.out.println("  Start time Start: " + timeInterval.getStart() + " millisecond");
                    System.out.println("  Duration Duration: " + timeInterval.getDuration() + " millisecond");
                }
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
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="8af9c953"></span>
## **Related documentation**

For the API interface related to querying audio transcoding tasks, see [GetAudioConvertJob](https://docs.byteplus.com/docs/tos/GetAudioConvertJob).
