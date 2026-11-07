---
title: "List video transcoding templates (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306570"
---

This article explains how to list video transcoding templates using the TOS Java SDK.

<span id="c3d1205c"></span>
## Notes

Only Java SDK version 2.9.8 and above supports the feature to list video transcoding templates.

<span id="501652e8"></span>
## Code examples

```java
// List video transcoding templates
package org.example.ListVideoConvertTemplates;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.*;
import com.volcengine.tos.model.bucket.*;
import com.volcengine.tos.model.object.*;

public class ListVideoConvertTemplatesExample {
    public static void main(String[] args) {
        String endpoint = System.getenv("TOS_ENDPOINT");
        String region = System.getenv("TOS_REGION");
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        
        // Specify BucketName, corresponding to the bucket containing the video transcoding templates to list
        String bucketName = System.getenv("TOS_BUCKET");
        
        // Initialize the client using endpoint, region, and AK/SK from environment variables for authentication
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);
        
        try {
            // Create a request to list video transcoding templates by specifying the Bucket name only
            ListVideoConvertTemplatesInput input = ListVideoConvertTemplatesInput.builder()
                    .bucket(bucketName)
                    .build();
            
            // Call the list video transcoding templates API
            ListVideoConvertTemplatesOutput output = tos.listVideoConvertTemplates(input);
            
            // Print key information of this request for troubleshooting
            System.out.println("List of video transcoding templates successfully");
            if (output.getRequestInfo() != null) {
                System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
                System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            }
            
            // Get the list of video transcoding templates
            java.util.List<VideoConvertTemplate> templates = output.getVideoConvertTemplates();
            if (templates != null && !templates.isEmpty()) {
                System.out.println("Turn up " + templates.size() + " Video transcoding templates:");
                for (VideoConvertTemplate template : templates) {
                    System.out.println("\n Template Information:");
                    System.out.println(" ID: " + template.getId());
                    System.out.println(" Name: " + template.getName());
                    System.out.println(" Label: " + template.getTag());
                    
                    // Print core fields of the transcode configuration
                    Transcode transcodeConfig = template.getTranscodeConfig();
                    if (transcodeConfig != null) {
                        System.out.println("Transcoding configuration:");
                        
                        // Container configuration, such as MP4/TS and segment duration
                        Container container = transcodeConfig.getContainer();
                        if (container != null) {
                            System.out.println(" Container configuration:");
                            System.out.println(" Container format: " + container.getFormat());
                            ClipConfig clipConfig = container.getClipConfig();
                            if (clipConfig != null) {
                                System.out.println("  Slicing time: " + cSlicing timelipConfig.getDuration());
                            }
                        }
                        
                        // Video parameters, including resolution, bitrate, and frame rate
                        Video video = transcodeConfig.getVideo();
                        if (video != null) {
                            System.out.println("  Video parameters:");
                            System.out.println("  Encoding format: " + video.getCodec());
                            System.out.println("  Resolution: " + video.getWidth() + "x" + video.getHeight());
                            System.out.println("  Bitrate: " + video.getBitRate());
                            System.out.println("  Frame rate: " + video.getFps());
                            System.out.println("  Pixel format: " + video.getPixFmt());
                            System.out.println("  Remove video stream: " + video.getRemove());
                        }
                        
                        // Audio parameters, including bitrate, sample rate, and number of channels
                        Audio audio = transcodeConfig.getAudio();
                        if (audio != null) {
                            System.out.println("  Audio parameters:");
                            System.out.println("  Encoding format: " + audio.getCodec());
                            System.out.println("  Bitrate: " + audio.getBitRate());
                            System.out.println("  Sampling rate: " + audio.getSampleRate());
                            System.out.println("  Number of channels: " + audio.getChannels());
                            System.out.println("  Sampling format: " + audio.getSampleFormat());
                            System.out.println("  Remove audio stream: " + audio.getRemove());
                        }
                        
                        // Time interval parameters to control the start time and duration of the transcoding task
                        TimeInterval timeInterval = transcodeConfig.getTimeInterval();
                        if (timeInterval != null) {
                            System.out.println("   Time range:");
                            System.out.println("   Start time (milliseconds): " + timeInterval.getStart());
                            System.out.println("   Duration (milliseconds): " + timeInterval.getDuration());
                       
                    }
                }
            } else {
                System.out.println("No video transcoding template found");
            }
            
        } catch (TosClientException e) {
            // Operation failed and a client exception was caught, usually due to invalid request parameters; the request was not sent
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed, caught a server exception, detailed error information can be obtained from the server response
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // As a fallback for catching other exceptions, this point is usually not reached
            System.out.println("Operation failed");
            System.out.println("Unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="a5c4493e"></span>
## Related documentation

For the API related to listing video transcoding templates, please refer to [ListVideoConvertTemplates](https://docs.byteplus.com/docs/tos/ListVideoConvertTemplates).
