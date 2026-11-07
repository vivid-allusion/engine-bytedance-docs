---
title: "Create video transcoding template (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306572"
---

This article introduces how to create a video transcoding template using the TOS Java SDK.

<span id="f9f43aa1"></span>
## Notes

Only Java SDK version 2.9.8 and above support creating video transcoding templates.

<span id="41e22218"></span>
## Code examples

```Java
// Create video transcoding template
package org.example.PutVideoConvertTemplate;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

import java.nio.charset.StandardCharsets;
import java.util.Base64;

public class PutVideoConvertTemplateExample {
    private static String base64String(String originalStr){
        // Step 1: Convert string to byte array (specify UTF-8 to avoid garbled characters)
        byte[] originalBytes = originalStr.getBytes(StandardCharsets.UTF_8);

        // Step 2: Base64 encoding (Basic encoder)
        byte[] encodedBytes = Base64.getEncoder().encode(originalBytes);

        // Convert the encoded byte array to a string
        String encodedStr = new String(encodedBytes, StandardCharsets.UTF_8);
        return encodedStr;
    }
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
            // Set the transcoding time range, starting from 0 seconds of the video, lasting 10 seconds
            // Note: start means the start time, duration means the length, both in milliseconds
            TimeInterval timeInterval = TimeInterval.builder()
                    .start(0)
                    .duration(10000)
                    .build();

            // Configure the output container: use MP4 format
            Container container = Container.builder()
                    .format(ContainerFormatType.MP4)
                    .build();

            // Configure video encoding parameters:
            Video video = Video.builder()
                    .codec("h264")
                     // - Encoding format: h264
                    .width(1920)
                    // - Resolution: 1920x1080 (Full HD)
                    .height(1080)
                     // - CRF: 23 (balance between quality and bitrate)
                    .crf(23)
                     // - Pixel format: yuv420p
                    .pixFmt("yuv420p")
                     // - Bitrate: 4 Mbps
                    .bitRate(4_000_000)
                      // - Frame rate: 30 fps
                    .fps(30)
                    .remove(false)
                    .build();

            // Configure audio encoding parameters:
            Audio audio = Audio.builder()
                     // - Encoding format: mp3
                    .codec("mp3")
                    .bitRate(128_000)
                     // - Sample format: fltp
                    .sampleFormat("fltp")
                      // - Sample rate: 44100 Hz
                    .sampleRate(44_100)
                      // - Channels: 2 (stereo)
                    .channels(2)
                    .remove(false)
                    .build();

            // Configure AIGC metadata for marking content production and distribution chain (example values)
            AIGCMetadata aigcMetadata = AIGCMetadata.builder()
                    .label("demo-label")
                    .contentProducer("demo-producer")
                    .produceID("demo-produce-id")
                    .contentPropagator("demo-propagator")
                    .propagateID("demo-propagate-id")
                    .reservedCode1(base64 String("123abc"))
                    .reservedCode2(base64String("456def"))
                    .build();

            // Fill metadata configuration via TranscodeConfigOptions
            TranscodeConfigOptions options = TranscodeConfigOptions.builder()
                    .aigcMetadata(aigcMetadata)
                    .build();

            // Summarize transcode configuration, unify time intervals, containers, video, audio, and AIGC metadata into Transcode
            Transcode transcodeConfig = Transcode.builder()
                    .timeInterval(timeInterval)
                    .container(container)
                    .video(video)
                    .audio(audio)
                    .options(options)
                    .build();

            // Assemble input parameters to create a video transcode template:
            // - Bucket: storage bucket for the template
            // - Name: template name (example: example-video-template)
            // - TranscodeConfig: the complete transcode configuration described above
            PutVideoConvertTemplateInput input = PutVideoConvertTemplateInput.builder()
                    .bucket(bucketName)
                    .name("example-video-template")
                    .transcodeConfig(transcodeConfig)
                    .build();

            // Call API to create video transcode template
            PutVideoConvertTemplateOutput output = tos.putVideoConvertTemplate(input);

            // Print key return results for troubleshooting and confirmation:
            // - RequestID: unique identifier of the request on the server
            // - StatusCode: HTTP status code
            // - Template ID: template identifier for direct reference when creating transcode tasks later
            System.out.println("Video transcoding template created successfully");
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            System.out.println("Template ID: " + output.getId());

        } catch (TosClientException e) {
            // Operation failed due to a caught client exception, usually caused by invalid request parameters. The request was not sent.
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed due to a caught server exception. Detailed error information returned from the server is available.
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Catching all other exceptions as a fallback, this is usually not executed.
            System.out.println("Operation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="dcd8bc8d"></span>
## Related documentation

For APIs related to creating video transcoding templates, see [PutVideoConvertTemplate](https://docs.byteplus.com/docs/tos/PutVideoConvertTemplate).
