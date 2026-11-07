---
title: "Query workflow (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306566"
---

This article explains how to query workflows using the TOS Java SDK.

<span id="a1ed2233"></span>
## Notes

Only Java SDK version 2.9.8 and above support querying workflows.

<span id="089314d5"></span>
## Code examples

```Java
// Query transcoding workflow
package org.example.GetConvertWorkflow;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class GetConvertWorkflowExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");

        // Provide your bucket name
        String bucketName = System.getenv("TOS_BUCKET");

        // If the region is not set, the default is North China 2 (Beijing)
        if (region == null || region.isEmpty()) {
            region = "cn-beijing";
        }

        // Initialize the client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try {
            // Construct GetConvertWorkflowInput to query the transcode workflow configured under the specified bucket
            GetConvertWorkflowInput input = GetConvertWorkflowInput.builder()
                    .bucket(bucketName)
                    .build();

            // Call the getConvertWorkflow interface
            GetConvertWorkflowOutput output = tos.getConvertWorkflow(input);

            // Print request information
            if (output != null && output.getRequestInfo() != null) {
                System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
                System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            }

            // Print rule information
            if (output != null && output.getRules() != null) {
                System.out.println("Number of rules: " + output.getRules().size());

                if (!output.getRules().isEmpty()) {
                    ConvertWorkflowRule firstRule = output.getRules().get(0);
                    if (firstRule != null) {
                        // Basic rule information
                        System.out.println("First rule ID: " + firstRule.getId());
                        System.out.println("First rule Enabled: " + firstRule.getEnabled());
                        System.out.println("First rule (Prefix): " + firstRule.getPrefix());

                        // Audio and video extension filter configuration
                        WorkflowExtFilter extFilter = firstRule.getExtFilter();
                        if (extFilter != null) {
                            if (extFilter.getAudioExts() != null) {
                                System.out.println("Audio extension AudioExts: " + extFilter.getAudioExts());
                            }
                            if (extFilter.getVideoExts() != null) {
                                System.out.println("Video extension VideoExts: " + extFilter.getVideoExts());
                            }
                        }

                        // Topology information
                        if (firstRule.getTopology() != null) {
                            System.out.println("拓扑 Topology: " + firstRule.getTopology());
                        }

                        // Operation configuration
                        WorkflowOperations operations = firstRule.getOperations();
                        if (operations != null) {
                            // Transcode operation
                            if (operations.getTranscode() != null && !operations.getTranscode().isEmpty()) {
                                OperationsTranscode transcodeOp = operations.getTranscode().get(0);
                                if (transcodeOp != null) {
                                    System.out.println("First Transcode OperationID: " + transcodeOp.getOperationID());
                                    System.out.println("First Transcode TemplateID: " + transcodeOp.getTemplateID());
                                    ConvertJobOutput transcodeOutput = transcodeOp.getOutput();
                                    if (transcodeOutput != null) {
                                        System.out.println("First Transcode Output Region: " + transcodeOutput.getRegion());
                                        System.out.println("First Transcode Output Bucket: " + transcodeOutput.getBucket());
                                        System.out.println("First Transcode Output Object: " + transcodeOutput.getObject());
                                    }
                                }
                            }

                            // AudioTranscode operation
                            if (operations.getAudioTranscode() != null && !operations.getAudioTranscode().isEmpty()) {
                                OperationsAudioTranscode audioTranscodeOp = operations.getAudioTranscode().get(0);
                                if (audioTranscodeOp != null) {
                                    System.out.println("First AudioTranscode OperationID: " + audioTranscodeOp.getOperationID());
                                    System.out.println("First AudioTranscode TemplateID: " + audioTranscodeOp.getTemplateID());
                                    ConvertJobOutput audioOutput = audioTranscodeOp.getOutput();
                                    if (audioOutput != null) {
                                        System.out.println("First AudioTranscode Output Region: " + audioOutput.getRegion());
                                        System.out.println("First AudioTranscode Output Bucket: " + audioOutput.getBucket());
                                        System.out.println("First AudioTranscode Output Object: " + audioOutput.getObject());
                                    }
                                }
                            }
                        }
                    }
                }
            }

        } catch (TosClientException e) {
            // Operation failed: client exception caught, Usually due to invalid request parameters; the request was not sent
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed: server exception caught, Detailed error information returned from the server is available
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Catch-all for other exceptions, Generally this should not occur
            System.out.println("Operation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="4480d9b6"></span>
## **Related documentation**

For the API interfaces related to querying workflows, see [GetWorkflow](https://docs.byteplus.com/docs/tos/GetWorkflow) and [GetWorkflowExecution](https://docs.byteplus.com/en/docs/tos/GetWorkflowExecution).
