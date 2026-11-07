---
title: "Create video transcoding task (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306573"
---

This article describes how to create a video transcoding task using the TOS Java SDK.

<span id="2a47367c"></span>
## Notes

Only Java SDK version 2.9.8 and above support creating video transcoding tasks.

<span id="652066a3"></span>
## Code examples

<span id="22332d67"></span>
### Create a video transcoding task by template ID

```Java
package org.example.CreateVideoConvertJob;

// Create video transcoding task based on template ID
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class CreateVideoConvertJobExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // Provide your bucket name
        String bucketName = System.getenv("TOS_BUCKET");
        // Template ID
        String templateId = "3633373966613563353858a1015403c6e03f";
        
        // Initialize the client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // 1. Set corresponding parameters based on the case type (trigger transcoding through template ID)
            // Source object key (placeholder, replace with the actual video object)
            String sourceObjectKey = "example-input.mp4";
            ConvertJobInput jobInput = ConvertJobInput.builder()
                    .object(sourceObjectKey)
                    .build();

            // Target output (write the transcoded result into the specified object within the same bucket)
            ConvertJobOutput jobOutput = ConvertJobOutput.builder()
                    .region(region)               // Output region: use the current region
                    .bucket(bucketName)           // Output bucket: the same as the input bucket, or configure to another bucket
                    .object("example-output.mp4") // Output object key (placeholder)
                    .build();

            // Construct transcoding configuration using the template ID; Transcode can be an empty object
            TranscodeConfig transcodeConfig = TranscodeConfig.builder()
                    .templateID(templateId)       // Reference the created video transcoding template ID
                    .transcode(new Transcode())   // Transcode through the template without additional detailed settings
                    .build();

            // 2. Call the corresponding API function
            CreateVideoConvertJobInput input = CreateVideoConvertJobInput.builder()
                    .bucket(bucketName)
                    .input(jobInput)
                    .output(jobOutput)
                    .transcodeConfig(transcodeConfig)
                    .build();
            CreateVideoConvertJobOutput output = tos.createVideoConvertJob(input);

            // 3. Handle the returned result
            System.out.println("Video transcoding task created successfully");
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            System.out.println("JobID: " + output.getJobId());
            
            // 4. Add appropriate comments: this case creates a task using the template ID, suitable for reusing a unified transcoding policy
            
        } catch (TosClientException e) {
            // Operation failed, caught client exception, usually due to invalid request parameters; the request was not sent
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed, caught server exception, detailed error information can be obtained from the server response
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Fallback to catch other exceptions; this block rarely executes
            System.out.println("Operation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="032e0584"></span>
### Create a video transcoding task by parameter configuration

```Java
package org.example.CreateVideoConvertJob;

// Create video transcode tasks based on parameter settings
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class CreateVideoConvertJobExample2 {
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
            // 1. Set parameters according to the case type (directly configure video and audio transcoding parameters)
            // Container format: MP4
            Container container = Container.builder()
                    .format(ContainerFormatType.MP4)
                    .build();
            
            // Video parameters: encoding h264, resolution 1280x720, CRF=23, pixel format yuv420p, bitrate 2Mbps, frame rate 30fps
            Video video = Video.builder()
                    .codec("h264")
                    .width(1280)
                    .height(720)
                    .crf(23)
                    .pixFmt("yuv420p")
                    .bitRate(2_000_000)
                    .fps(30)
                    .remove(false)
                    .build();
            
            // Audio parameters: encoding aac, bitrate 128Kbps, sample rate 44100Hz, stereo
            Audio audio = Audio.builder()
                    .codec("aac")
                    .bitRate(128_000)
                    .sampleFormat("fltp")
                    .sampleRate(44_100)
                    .channels(2)
                    .remove(false)
                    .build();
            
            // Transcoding time range (example: start at 0 ms, duration 10 seconds)
            TimeInterval timeInterval = TimeInterval.builder()
                    .start(0)
                    .duration(10_000)
                    .build();
            
            // Summarize transcoding configuration
            Transcode transcode = Transcode.builder()
                    .timeInterval(timeInterval)
                    .container(container)
                    .video(video)
                    .audio(audio)
                    .build();
            TranscodeConfig transcodeConfig = TranscodeConfig.builder()
                    .transcode(transcode)
                    .build();
            
            // Source object and target output
            ConvertJobInput jobInput = ConvertJobInput.builder()
                    .object("example-input.mp4")
                    .build();
            ConvertJobOutput jobOutput = ConvertJobOutput.builder()
                    .region(region)
                    .bucket(bucketName)
                    .object("example-output.mp4")
                    .build();
            
            // 2. Call the corresponding API function
            CreateVideoConvertJobInput input = CreateVideoConvertJobInput.builder()
                    .bucket(bucketName)
                    .input(jobInput)
                    .output(jobOutput)
                    .transcodeConfig(transcodeConfig)
                    .callback("http://example.com/callback")
                    .build();
            CreateVideoConvertJobOutput output = tos.createVideoConvertJob(input);
            
            // 3. Process the returned results
            System.out.println("Video transcoding task created successfully");
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            System.out.println("JobID: " + output.getJobId());

            
        } catch (TosClientException e) {
            # The operation failed and a client exception was caught. This is usually due to invalid request parameters or a network exception. The request was not sent in this case.
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            # The operation failed and a server exception occurred. See the response for the error details.
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Catch all other exceptions as a fallback, generally this code does not execute
            System.out.println("Operation failed");
            System.out.println("Unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="92c036af"></span>
### Callback request details

When the Callback field is set, the system sends a callback request to the Callback URL after the task completes successfully:

```json
Post <callback_url_path> HTTP/1.1
Host: <callback_url_host>

{
    "JobID": "fa81ef2a00a2211f08a9aa5fa72ccf57a",    // task ID
    "CreateTime": "2025-03-26T17:14:01+0800",        // task creation time, RFC 3339 format
    "StartTime": "2025-03-26T17:14:02+0800",         // task execution time, RFC 3339 format
    "EndTime": "2025-03-26T17:14:02+0800",           // task completion time, RFC 3339 format
    "Callback": "https://myapp.com/callback",        // callback URL
    "State": "Success",                              // task status, values: Success/Failed
    "Code": 0,                                       // task status code
    "Message": "success",                            // task status message
    "Input" : {                     // source file
        "Object" : "sample.mp4"     
    },
    "TranscodeConfig": {           // transcoding parameters used when issuing the task
        "Transcode": {
            "TimeInterval": {
              "Start": 0,
              "Duration": 10000
            },
            "Container": {
              "Format": "mp4"
            },
            "Video": {
              "Codec": "h264",
              "Width": 480,
              "Height": 480,
              "Crf": 1,
              "PixFmt": "yuv420p"
            }
        },
    },
    "Output" : {                    // output file
        "Region" : "cn-beijing",    
        "Bucket" : "testbkt",
        "Object" : "output.mp4"
    }
}
```


<span id="54be7380"></span>
## Related documentation

For API interfaces related to creating video transcode tasks, refer to [CreateTranscodeJob](https://docs.byteplus.com/docs/tos/CreateTranscodeJob).
