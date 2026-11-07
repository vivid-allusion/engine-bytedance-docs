---
title: "Create audio transcoding task (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306565"
---

This article explains how to create an audio transcoding task using the TOS Java SDK.

<span id="36e2109a"></span>
## Notes

Only Java SDK version 2.9.8 and above support creating audio transcoding tasks.

<span id="3e533c59"></span>
## Code examples

```Java
// Create audio transcoding task using configuration
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class CreateAudioConvertJobExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // Specify BucketName
        String bucketName = System.getenv("TOS_BUCKET");
        
        // Initialize client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // 1. Prepare the source and target object keys (placeholder example, replace with actual object names)>
            String srcObject = "input-audio.mp3";    // Source audio object key
            String targetObject = "output-audio.mp3"; // Transcoded audio object key
            
            // 2. Configure time interval: start at 1000 ms, last for 10000 ms
            TimeInterval timeInterval = TimeInterval.builder()
                    .start(1000)       // Start time of the segment, in milliseconds
                    .duration(10000)   // Duration of the segment, in milliseconds
                    .build();

            // 3. Build audio transcoding configuration
            AudioConvertConfig audioConvertConfig = AudioConvertConfig.builder()
                    .timeInterval(timeInterval)                     // Audio processing time interval
                    .containerFormat(AudioContainerFormatType.MP3)  // Output audio container format: MP3
                    .bitRate(8000)                                 // Audio bitrate in bps
                    .bitRateOpt(1)                                 // Bitrate control parameter, example value 1
                    .sampleFormat("fltp")                         // Sample format, e.g., fltp
                    .sampleRate(11025)                             // Sample rate in Hz
                    .channels(2)                                   // Number of channels, 2 means stereo
                    .build();

            // 4. Construct task input: specify source object
            ConvertJobInput jobInput = ConvertJobInput.builder()
                    .object(srcObject)
                    .build();

            // 5. Build task output: specify output region, bucket name, and target object
            ConvertJobOutput jobOutput = ConvertJobOutput.builder()
                    .region(region)         // Output region
                    .bucket(bucketName)     // Output bucket
                    .object(targetObject)   // Transcoded audio object key
                    .build();

            // 6. Assemble create audio transcoding task request
            CreateAudioConvertJobInput input = CreateAudioConvertJobInput.builder()
                    .bucket(bucketName)                 // Bucket the task belongs to
                    .input(jobInput)                    // Source object configuration
                    .audioConvertConfig(audioConvertConfig) // Audio transcoding configuration
                    .output(jobOutput)                  // Output result configuration
                    .build();

            // 7. Call the create audio transcoding task interface
            CreateAudioConvertJobOutput output = tos.createAudioConvertJob(input);

            // 8. Print key return information
            System.out.println("Audio transcoding task created successfully");
            System.out.println("JobId: " + output.getJobId());
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            
        } catch (TosClientException e) {
            // Operation failed, client exception caught; usually caused by invalid request parameters or network issues
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed, server exception caught; detailed error information can be obtained from the server response
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Fallback to catch other exceptions; this typically does not execute
            System.out.println("Operation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="c659cfdf"></span>
## **Related documentation**

For APIs related to creating audio transcoding tasks, refer to [CreateAudioConvertJob](https://docs.byteplus.com/docs/tos/AudioConvert).
