---
title: "List audio transcoding templates (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/2306564"
---

This article explains how to list audio transcoding templates using the TOS Java SDK.

<span id="a441a2f9"></span>
## Notes

Only Java SDK version 2.9.8 and above support listing audio transcoding templates.

<span id="dff055fc"></span>
## Code examples

```Java
// List audio transcoding templates
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.comm.common.AudioContainerFormatType;
import com.volcengine.tos.model.bucket.*;

public class ListAudioConvertTemplatesExample {
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
            // Create request to list audio transcoding templates
            ListAudioConvertTemplatesInput input = ListAudioConvertTemplatesInput.builder()
                    .bucket(bucketName)
                    .build();
            
            // Call list audio transcoding templates interface
            ListAudioConvertTemplatesOutput output = tos.listAudioConvertTemplates(input);
            
            // Process returned results
            System.out.println("Audio transcoding templates listed successfully");
            System.out.println("RequestID: " + output.getRequestInfo().getRequestId());
            System.out.println("StatusCode: " + output.getRequestInfo().getStatusCode());
            
            // Get list of audio transcoding templates
            java.util.List<AudioConvertTemplate> templates = output.getAudioConvertTemplates();
            if (templates != null && !templates.isEmpty()) {
                System.out.println("Turn up " + templates.size() + " Audio transcoding templates:");
                for (AudioConvertTemplate template : templates) {
                    System.out.println("\nTemplate Information:");
                    System.out.println("  ID: " + template.getId());
                    System.out.println("  Name: " + template.getName());
                    System.out.println("  Label: " + template.getTag());
                    
                    // Print audio transcoding configuration information
                    AudioConvertConfig config = template.getAudioConvertConfig();
                    if (config != null) {
                        System.out.println("  Audio Configuration:");
                        System.out.println("  Container format: " + config.getContainerFormat());
                        System.out.println("  Bitrate: " + config.getBitRate());
                        System.out.println("  Sampling rate: " + config.getSampleRate());
                        System.out.println("  Number of channels: " + config.getChannels());
                        System.out.println("  Sampling format: " + config.getSampleFormat());
                        
                        // Print time range information
                        TimeInterval timeInterval = config.getTimeInterval();
                        if (timeInterval != null) {
                            System.out.println("    Time range:");
                            System.out.println("    Start time: " + timeInterval.getStart());
                            System.out.println("    Duration: " + timeInterval.getDuration());
                        }
                    }
                }
            } else {
                System.out.println("No audio transcoding template found");
            }
            
        } catch (TosClientException e) {
            // Operation failed: caught a client exception, usually due to invalid request parameters, request not sent
            System.out.println("Operation failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
            // Operation failed: caught a server exception, detailed error info available from the server response
            System.out.println("Operation failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
            // Fallback catch for other exceptions, generally not reached here
            System.out.println("Operation failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="1e282ee0"></span>
## **Related documentation**

For API interfaces related to creating audio transcoding templates, see [ListAudioConvertTemplates](https://docs.byteplus.com/docs/tos/ListAudioConvertTemplates).
