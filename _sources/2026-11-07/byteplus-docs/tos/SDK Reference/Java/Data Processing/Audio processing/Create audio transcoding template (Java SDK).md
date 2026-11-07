---
title: "Create audio transcoding template (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306568"
---

This article explains how to create an audio transcoding template using the TOS Java SDK.

<span id="52a592d2"></span>
## Notes

Only Java SDK version 2.9.8 and above support creating audio transcoding templates.

<span id="0ed44a72"></span>
## Code example

<span id="00aa00f5"></span>
### Create audio transcoding template

```java
// Create audio transcoding template
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.AudioContainerFormatType;
import com.volcengine.tos.model.bucket.PutAudioConvertTemplateInput;
import com.volcengine.tos.model.bucket.PutAudioConvertTemplateOutput;
import com.volcengine.tos.model.bucket.AudioConvertConfig;
import com.volcengine.tos.model.bucket.TimeInterval;

public class PutAudioConvertTemplateExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // Enter BucketName
        String bucketName = System.getenv("TOS_BUCKET");

        // Initialize the client
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // Create audio transcoding template
            // 1. Set interval parameters: start at 1 second, last for 10 seconds
            TimeInterval timeInterval = TimeInterval.builder()
                    .start(1)      // Start time (milliseconds)
                    .duration(10000)  // Duration (milliseconds)
                    .build();

            // 2. Configure audio transcoding parameters
            AudioConvertConfig audioConvertConfig = AudioConvertConfig.builder()
                    .timeInterval(timeInterval)                           // Time interval configuration
                    .containerFormat(AudioContainerFormatType.MP3)       // Container format: MP3
                    .bitRate(8000)     // bit rate: 8000 bps
                    .bitRateOpt(1)
                    .sampleFormat("fltp")                                // Sample format: fltp
                    .sampleRate(11025)                                   // Sample rate: 11025 Hz
                    .channels(2)   // channels: 2 (stereo)
                    .build();

            // 3. Create audio transcoding template input parameters
            PutAudioConvertTemplateInput input = PutAudioConvertTemplateInput.builder()
                    .bucket(bucketName)
                    .name("test-audio-template")                          // Template name
                    .audioConvertConfig(audioConvertConfig)              // Audio transcoding configuration
                    .build();

            // 4. Call API to create audio transcoding template
            PutAudioConvertTemplateOutput output = tos.putAudioConvertTemplate(input);

            // 5. Handle the response
            System.out.println("Audio transcoding template created successfully");
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            System.out.println("Template ID: " + output.getId());
            System.out.println("Template Name: test-audio-template");
            System.out.println("Container format: MP3");
            System.out.println("Bitrate: 8000 bps");
            System.out.println("Sampling rate: 11025 Hz");
            System.out.println("Number of channels: 2");
            
        } catch (TosClientException e) {
            // Operation failed, caught client exception, Usually invalid request parameters or network exception, request was not sent
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed due to a server exception; detailed error information can be obtained from the server response
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Fallback catch for other exceptions; this usually does not get executed
            System.out.println("Operation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="15953d11"></span>
## Related documentation

For related API interfaces on creating audio transcoding templates, see [PutAudioConvertTemplate](https://docs.byteplus.com/docs/tos/PutAudioConvertTemplate).
