---
title: "Create workflow (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306567"
---

This article explains how to create workflows using the TOS Java SDK.

<span id="d8bf935a"></span>
## Notes

Only Java SDK version 2.9.8 and above support workflow creation.

<span id="a512ca6f"></span>
## Code examples

<span id="6f03f137"></span>
### Create video transcoding workflow

```java
// Create a video transcoding workflow
package org.example.PutConvertWorkflow;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class PutConvertWorkflowExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // Enter BucketName
        String bucketName = System.getenv("TOS_BUCKET");
        
        // Initialize client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // Scenario Description: Create a video transcoding workflow that automatically triggers a transcoding task when an mp4 file with the `videos/` prefix is uploaded to a specified bucket.
            // 1. Create a video transcoding template and configure parameters such as container, video, audio, and time range.
            // Set the time interval: starting from 0ms and lasting for 60 seconds.
            TimeInterval timeInterval = TimeInterval.builder()
                    .start(0)
                    .duration(60_000)
                    .build();

            // Configure the output container: Use MP4 format and set a short clip duration (10 seconds in the example).
            ClipConfig clipConfig = ClipConfig.builder()
                    // Segment duration, in milliseconds
                    .duration(10_000)
                    .build();
            Container container = Container.builder()
                    .format(ContainerFormatType.MP4)
                    .clipConfig(clipConfig)
                    .build();

            // Configure video encoding parameters; here, we use the common H.264 encoding.
            Video video = Video.builder()
                    .codec("h264")
                    .width(1920)
                    .height(1080)// - Resolution: 1920x1080
                    .crf(23)  // - CRF：23
                    .pixFmt("yuv420p")   // - Pixel format: yuv420p
                    .bitRate(4_000_000)   // - Video bitrate: 4 Mbps
                    .fps(25)   // - Frame rate: 25 fps
                    .remove(false)
                    .build();

            // Configure audio encoding parameters; AAC encoding is used here.
            Audio audio = Audio.builder()
                    .codec("aac")
                    .bitRate(128_000)  // - Bitrate: 128 kbps
                    .sampleFormat("fltp")
                    .sampleRate(44_100)   // - Sampling rate: 44100 Hz
                    .channels(2)   // - Number of channels: 2 (stereo)
                    .remove(false)
                    .build();

            // Summary of video transcoding configurations
            Transcode transcode = Transcode.builder()
                    .timeInterval(timeInterval)
                    .container(container)
                    .video(video)
                    .audio(audio)
                    .build();

            // Create a video transcoding template; the template name can be customized according to your business needs.
            PutVideoConvertTemplateInput putVideoTemplateInput = PutVideoConvertTemplateInput.builder()
                    .bucket(bucketName)
                    .name("example-video-convert-workflow-template")
                    .transcodeConfig(transcode)
                    .build();
            PutVideoConvertTemplateOutput putVideoTemplateOutput = tos.putVideoConvertTemplate(putVideoTemplateInput);

            // 2. Transcoding operations in constructing a transcoding workflow
            // Configure the transcoding output location; this example writes it to output/video.mp4 within the same bucket.
            ConvertJobOutput videoOutput = ConvertJobOutput.builder()
                    .region(region)
                    .bucket(bucketName)
                    .object("output/video.mp4")
                    .build();

            // OperationID This operation is used to reference the topology; here it's named "transcode".
            OperationsTranscode videoTranscodeOperation = OperationsTranscode.builder()
                    .operationID("transcode")
                    .templateID(putVideoTemplateOutput.getId())
                    .output(videoOutput)
                    .build();

            // WorkflowOperations only contains video transcoding operations.
            WorkflowOperations workflowOperations = WorkflowOperations.builder()
                    .transcode(java.util.Arrays.asList(videoTranscodeOperation))
                    .build();

            // 3. Set an extension filter to only apply to video files with the .mp4 extension.
            WorkflowExtFilter extFilter = WorkflowExtFilter.builder()
                    .videoExts(java.util.Arrays.asList("mp4"))
                    .build();

            // 4. Construct transcoding workflow rules
            // Rule IDs should ideally be globally unique; here, we simply use the current timestamp concatenated with a prefix.
            String ruleId = "video-convert-workflow-" + System.currentTimeMillis();

            // Topology configuration: Only one node indicates that a transcode operation is being performed.
            java.util.List<java.util.List<String>> topology = java.util.Arrays.asList(
                    java.util.Arrays.asList("transcode")
            );

            ConvertWorkflowRule rule = ConvertWorkflowRule.builder()
                    .id(ruleId)
                    // Rules enabled
                    .enabled(true)
                    // Match only objects with the prefix "videos/".
                    .prefix("videos/")
                    .extFilter(extFilter)
                    .topology(topology)
                    .operations(workflowOperations)
                    .build();

            // 5. Create a workflow by calling the putConvertWorkflow interface.
            PutConvertWorkflowInput putWorkflowInput = PutConvertWorkflowInput.builder()
                    .bucket(bucketName)
                    .rules(java.util.Arrays.asList(rule))
                    .build();

            PutConvertWorkflowOutput putWorkflowOutput = tos.putConvertWorkflow(putWorkflowInput);

            // Print key return fields and rule summary information
            System.out.println("Video transcoding workflow created successfully");
            System.out.println("RequestID: " + putWorkflowOutput.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + putWorkflowOutput.getRequestInfo().getStatusCode());
            System.out.println("Rule ID: " + ruleId);
            System.out.println("Video transcoding output location: " + videoOutput.getBucket() + "/" + videoOutput.getObject());
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


<span id="e6fa2dbc"></span>
### Create audio transcoding workflow

```java
// Creating an audio transcoding workflow
package org.example.PutConvertWorkflow;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class PutConvertWorkflowExample2 {
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
            // Scenario Description: Create an audio transcoding workflow that automatically triggers an audio transcoding task when an mp3 file with the prefix "audis/" under a specified bucket is uploaded.
            // 1. Create an audio transcoding template and configure the container format, bitrate, sample rate, number of channels, and time interval.
            // Set the time interval: starting from 0ms and continuing for 5 minutes.
            TimeInterval timeInterval = TimeInterval.builder()
                    .start(0)
                    .duration(300_000)
                    .build();

            // Configure audio transcoding parameters
            AudioConvertConfig audioConvertConfig = AudioConvertConfig.builder()
                    .timeInterval(timeInterval)
                    // - Container format: MP3
                    .containerFormat(AudioContainerFormatType.MP3)
                     // - Bitrate: 128 kbps
                    .bitRate(128_000)
                    .bitRateOpt(1)
                    // - Sampling format: fltp
                    .sampleFormat("fltp")
                     // - Sampling rate: 44100 Hz
                    .sampleRate(44_100)
                     // - Number of channels: 2 (stereo)
                    .channels(2)
                    .build();

            // Create an audio transcoding template
            PutAudioConvertTemplateInput putAudioTemplateInput = PutAudioConvertTemplateInput.builder()
                    .bucket(bucketName)
                    .name("example-audio-convert-workflow-template")
                    .audioConvertConfig(audioConvertConfig)
                    .build();
            PutAudioConvertTemplateOutput putAudioTemplateOutput = tos.putAudioConvertTemplate(putAudioTemplateInput);

            // 2. Audio transcoding operations in constructing a transcoding workflow
            // Configure the transcoding output location; this example writes it to output/audio.mp3 within the same bucket.
            ConvertJobOutput audioOutput = ConvertJobOutput.builder()
                    .region(region)
                    .bucket(bucketName)
                    .object("output/audio.mp3")
                    .build();

            // OperationID this operation is used to reference the topology; here it's named "audio-transcode".
            OperationsAudioTranscode audioTranscodeOperation = OperationsAudioTranscode.builder()
                    .operationID("audio-transcode")
                    .templateID(putAudioTemplateOutput.getId())
                    .output(audioOutput)
                    .build();

            // WorkflowOperations contains only audio transcoding operations.
            WorkflowOperations workflowOperations = WorkflowOperations.builder()
                    .audioTranscode(java.util.Arrays.asList(audioTranscodeOperation))
                    .build();

            // 3. Set the file extension filter to only apply to mp3 audio files.
            WorkflowExtFilter extFilter = WorkflowExtFilter.builder()
                    .audioExts(java.util.Arrays.asList("mp3"))
                    .build();

            // 4. Constructing audio transcoding workflow rules
            String ruleId = "audio-convert-workflow-" + System.currentTimeMillis();

            // Topology configuration: Only one node indicates that an audio-transcode operation is being performed.
            java.util.List<java.util.List<String>> topology = java.util.Arrays.asList(
                    java.util.Arrays.asList("audio-transcode")
            );

            ConvertWorkflowRule rule = ConvertWorkflowRule.builder()
                    .id(ruleId)
                    // Rules enabled
                    .enabled(true)
                    // Match only objects with the audios/ prefix.
                    .prefix("audios/")
                    .extFilter(extFilter)
                    .topology(topology)
                    .operations(workflowOperations)
                    .build();

            // 5.Call the putConvertWorkflow interface to create an audio transcoding workflow
            PutConvertWorkflowInput putWorkflowInput = PutConvertWorkflowInput.builder()
                    .bucket(bucketName)
                    .rules(java.util.Arrays.asList(rule))
                    .build();

            PutConvertWorkflowOutput putWorkflowOutput = tos.putConvertWorkflow(putWorkflowInput);

            // Print key return fields and rule summary information
            System.out.println("Audio transcoding workflow created successfully");
            System.out.println("RequestID: " + putWorkflowOutput.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + putWorkflowOutput.getRequestInfo().getStatusCode());
            System.out.println("Rule ID: " + ruleId);
            System.out.println("Audio transcoding output location: " + audioOutput.getBucket() + "/" + audioOutput.getObject());
        } catch (TosClientException e) {
            // Operation failed, and a client-side exception was caught. This usually indicates an incorrect request parameter, meaning the request was never sent.
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed，By capturing server-side exceptions, you can obtain detailed error information returned by the server.
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


<span id="3f1ea2b9"></span>
## **Related documentation**

For API interfaces related to workflow creation, see [CreateWorkflow](https://docs.byteplus.com/docs/tos/CreateWorkflow).
