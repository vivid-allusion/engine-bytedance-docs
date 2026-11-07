---
title: "Detect deepfakes with the SDK"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Detect_deepfakes_with_the_SDK"
---

You can use the LLM Application Firewall SDK to detect AI\-generated or manipulated content in images and videos, including deepfakes, compositing, and partial tampering.

This guide uses a local image file as an example to demonstrate how to configure an asset, submit content through the SDK, interpret the response, and review detection logs.

<span id="581d536b"></span>
## Applicable scenarios


* **Automated content review**: Automatically scan images or videos after users upload them, reducing the effort required for initial manual screening.

* **Risk pre\-screening**: Identify potentially manipulated content before it enters insurance claims, risk management, content governance, or similar workflows.

* **Review system integration**: Return detection results to your business system to support further manual review and decision\-making.


<span id="16e70c2e"></span>
## Prerequisites

Follow [Install and initialize the Python SDK](https://docs.byteplus.com/docs/LLM-Application-Firewall/Python_installation_and_initialization) to install the required SDK dependencies and initialize the client.

<span id="74ca4c6e"></span>
## Sample requirements

Before calling the SDK, verify that each image or video meets the applicable format and size requirements.

<span id="a2f1565d"></span>
### Images


* **Supported formats**: `jpg`, `jpeg`, `png`, and `webp`

* **Maximum size**: 10 MB per image

* **Base64 encoding**: You can normally submit the image as a raw Base64\-encoded string without a MIME prefix. If your application uses Data URIs, add the appropriate prefix:

   * `jpg` and `jpeg`: `data:image/jpeg;base64,`

   * `png`: `data:image/png;base64,`

   * `webp`: `data:image/webp;base64,`


<span id="420131fe"></span>
### Videos


* **Supported formats**: `mp4` and `avi`

* **Maximum size**: 50 MB per video

* **Base64 encoding**: You can submit the video as a raw Base64\-encoded string. If your application uses Data URIs, add the appropriate prefix:

   * `mp4`: `data:video/mp4;base64,`

   * `avi`: `data:video/x-msvideo;base64,`


<span id="32fd2c4e"></span>
## Step 1: Create an asset


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. In the left navigation bar, select **Asset management**, then click **Add asset**.

3. Configure the following parameters and click **Submit**.

   * **Integration method**: SDK integration.

   * **Application name**: Use deepfake_demo as an example.

   * **Protection scenario**: Deepfake detection.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fccbac9c43774941be94bcbd0be64a50) </span>

4. Return to the asset management page and copy the asset’s `AppID`. You will use this value for the `scene` parameter in the SDK request.


<span id="dfb00b0d"></span>
## Step 2: Prepare configuration parameters

The following table describes the main parameters used in the SDK examples.


|Parameter |Sample value |Description |
|---|---|---|
|myUrl |https://`ap-southeast-1.sdk.access-bp.llm-shield.omni-shield.ai` |The service endpoint for the LLM Application Firewall, in the format `https://{region}.sdk.access-bp.llm-shield.omni-shield.ai`, where region is the region of the instance you purchased.<br><br><br>* Asia Pacific (Johor): ap\-southeast\-1<br><br>* Hong Kong: cn\-hongkong |
|ak, sk |* AK：AKLTYWRhNDMw\*\*\*\*<br><br>* SK：TWprNE5XVXlZbc\*\*\*\* |The **Access Key ID** and **Secret Access Key** of your BytePlus account. For instructions, see [Access Key (Secret) Management](https://www.volcengine.com/docs/6291/65568).<br><br><br>1. Log in to the [BytePlus IAM Console](https://console.byteplus.com/iam/keymanage).<br><br>2. Check the Access Key ID and Secret Access Key of the BytePlus account or create a new one. |
|appid |app\-d35p9du8pa51\*\*\*\* |The unique identifier of the asset. After completing console access configuration, the system will automatically generate an AppID. Corresponds to the `scene` in [Check whether input or output content is compliant](https://docs.byteplus.com/docs/LLM-Application-Firewall/Check_whether_input_or_output_content_is_compliant).<br><br> You can go to the asset management module in the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield) to view the AppID of assets integrated via SDK.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">When calling the SDK, you must use the AppID of an asset configured for SDK integration. AppIDs for assets that use other integration methods are not valid.</div><br> |
|region |ap\-southeast\-1 |The region to which the **asset** belongs, consistent with the region in myUrl.<br><br><br>* Asia Pacific (Johor): ap\-southeast\-1<br><br>* Hong Kong: cn\-hongkong |
|image_file |/Users/DeepFakeTest/image_001.png |The local path of the object to be detected. |
|message.role |user |Source of the content. Supported values are `user` and `assistant`. Use  `user` for content uploaded by an end user and `assistant` for content generated by a model. |
|message.contenttype |IMAGE |Type of content submitted for detection. Use `ContentTypeV2.IMAGE` for images or `ContentTypeV2.VIDEO` for videos. |


<span id="0c5185be"></span>
## Step 3: Call the SDK

The following examples read a local image, encode it as Base64, submit it to the detection API, and print the response.


<Tabs>
<Tab zoneid="fE9SRwUDuy" title="Python">
<TabTitle>Python</TabTitle>

```Python
from byteplussdkllmshield import *
import base64


def load_image_content(image_file):
    with open(image_file, 'rb') as f:
        img_bytes = f.read()
    base64_bytes = base64.b64encode(img_bytes).decode('utf-8')
    return base64_bytes, len(base64_bytes)


def main():
    # Replace the parameters with the actual values
    myUrl = "https://ap-southeast-1.sdk.access-bp.llm-shield.omni-shield.ai"  # Endpoint of your LLM Application Firewall instance
    ak = "YOUR AK" # Access Key of Your BytePlus account
    sk = "YOUR SK" # Secret Key of Your BytePlus account
    appid = "app-****"  # AppId of the asset, which can be obtained on the asset management page in the console
    region = "ap-southeast-1"  # Region of the LLM Application Firewall instance
    TIMEOUT = 50  # Timeout duration (seconds)


    image_file = "/Users/test/image_002872.png"  # Local storage path of image to be checked
    image_content, size = load_image_content(image_file)
    # The size after Base64 encoding does not exceed 10 MB
    if size > 1010241024:
        print(f"Request failed: {size/1024}KB")
        return
    try:
        # Send request and get response
        client = ClientV2(myUrl, ak, sk, region, TIMEOUT)
        # Build request (using a Pydantic model)
        request = ModerateV2Request(
            scene=appid,  # AppId of the asset
            message=MessageV2(
                role="user",  # Content source: 'user' for user prompts or 'assistant' for model responses
                content=image_content,  # Image content to be checked
                content_type=ContentTypeV2.IMAGE  # Type of the content: `IMAGE` for image content
            ),
        )


        response = client.Moderate(request)


        # Use pydantic's built-in serialization method
        print("Moderation result (JSON format):")
        print(response.model_dump_json(by_alias=True, indent=2))  # Directly convert a Pydantic model to JSON


    except Exception as e:
        print(f"Request failed: {e}")


if __name__ == "__main__":
    main()
```



</Tab>
<Tab zoneid="YxlHVmQs4q" title="Go">
<TabTitle>Go</TabTitle>

```Go
package main


import (
    "encoding/base64"
    "fmt"
    "os"
    "time"


    "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/llmshield"
)


func EncodeImageToBase64(imagePath string) (string, error) {
    // Read image file content
    data, err := os.ReadFile(imagePath)
    if err != nil {
        return "", fmt.Errorf("failed to read image: %v", err)
    }


    // Perform Base64 encoding
    base64Str := base64.StdEncoding.EncodeToString(data)
    return base64Str, nil
}


func main() {
    var response *llmshield.ModerateV2Response
    var err error
    // Replace the parameters with the actual values
    myUrl := "https://ap-southeast-1.sdk.access-bp.llm-shield.omni-shield.ai" // Endpoint of your LLM Application Firewall instance
    ak := "YOUR AK"                   // Access Key of Your BytePlus account
    sk := "YOUR SK"      // Secret Key of Your BytePlus account
    appid := "app-****"                                       // The asset's AppId can be obtained from the console
    region := "ap-southeast-1"                                                // Region of the LLM Application Firewall instance
    timeout := time.Second * 50                                              // Timeout (seconds)
    request := llmshield.ModerateV2Request{
        Message: nil,
        Scene:   appid,
    }


    dtstr, err := EncodeImageToBase64("/Users/test/example_image.jpeg") // Local storage path of the image to be detected
    dsize := len(dtstr)
    // Base64 encoded size should not exceed 10 MB
    if err != nil || dsize > 1010241024 {
        fmt.Printf("%v,dsize:%v", err, dsize)
        return
    }
    request.Message = &llmshield.MessageV2{
        Content:     dtstr,
        ContentType: llmshield.ContentTypeV2_IMAGE,
        Role:        "user",
    }


    // Create client instance
    client := llmshield.New(myUrl, ak, sk, region, timeout)
    if client == nil {
        fmt.Printf("Failed to create client instance\n")
        return
    }
    response, err = client.Moderate(&request)
    if err != nil {
        fmt.Printf("Error occurred while checking LLM response: %v\n", err)
    }
    if response == nil {
        fmt.Println("Received empty result")
    } else {
        fmt.Printf("Received result: %s\n", response.String())
    }
}
```





</Tab>
<Tab zoneid="BFVu2Bgrpi" title="Java">
<TabTitle>Java</TabTitle>

```Java
package com.demo;
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.util.Base64;

import com.byteplus.llmshield.*;

public class ModerateBoe {
    public static String convertImageToBase64(String imagePath) throws IOException {
        File file = new File(imagePath);
        try (FileInputStream fis = new FileInputStream(file)) {
            byte[] imageBytes = new byte[(int) file.length()];
            fis.read(imageBytes);
            return Base64.getEncoder().encodeToString(imageBytes);
        }
    }

    // Replace the parameters with the actual values
    public static void main(String[] args) throws IOException {
        String myUrl = "https://ap-southeast-1.sdk.access-bp.llm-shield.omni-shield.ai";  // Endpoint of your LLM Application Firewall instance
        String ak = "YOUR AK";  // Access Key of your BytePlus account
        String sk = "YOUR SK";  // Secret Key of your BytePlus account
        String region = "ap-southeast-1";  // Region of the LLM Application Firewall instance
        String myAppID = "app-d45gff4r7odm2ols****"; // AppId of your asset
        long timeout = 5000; // Timeout (milliseconds)
        ApiClient client = ApiClient.New(myUrl, ak,sk,region, timeout);

        ModerateV2Request request = new ModerateV2Request();
        request.setScene(myAppID);

        String image_content = "";
        String image_file = "/Users/Image/20251105-211228.jpeg"; // Local storage path of the image to be detected
        try {
            image_content = convertImageToBase64(image_file);
            int flen =image_file.length();
            //The size after Base64 encoding does not exceed 10 MB
            if (flen > 10 * 1024 * 1024) {
                System.out.println("Content size bigger than system: " + flen/1024 + "KB");
                return;
            }

        } catch (IOException e) {
            System.err.println("Converting failed:" + e.getMessage());
            e.printStackTrace();
        }
        System.out.println("Content is:" + image_content);

        // Set detection content
        MessageV2 message = new MessageV2();
        message.setContent(image_content);
        message.setRole("user"); // Content source: 'user' for user prompts; 'assistant' for model responses
        message.setContentType(ContentTypeV2.IMAGE);
        request.setMessage(message);

        try {
            // Call the Moderate interface to perform a check
            ModerateV2Response response = client.Moderate(request );
            if (response != null) {
                System.out.println("response: " + response);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```





</Tab>
</Tabs>


<span id="2a5789f8"></span>
## Step 4: Interpret the results

After receiving the response, use the risk and decision fields to determine whether the submitted image or video was identified as manipulated content.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/985cbcef554f4dadb15372c58bffaa73) </span>


|Field |Sample value |Description |
|---|---|---|
|RiskInfo.Risks.Category |109 |Primary risk category. 109 indicates a deepfake risk was detected. |
|RiskInfo.Risks.Label |10900000 |Secondary detection category label information. 10900000 indicates the label corresponding to the detected deepfake risk. Refer to [Check whether input or output content is compliant](https://docs.byteplus.com/docs/LLM-Application-Firewall/Check_whether_input_or_output_content_is_compliant) for label details. |
|RiskInfo.Risks.Prob |1.0 |Risk probability, indicating the likelihood that the detected content belongs to this risk. The value ranges from 0 to 1. |
|Decision.DecisionType |2 |The triggered policy action, indicating how the detected content is handled:<br><br><br>* 1: Allow. The detected content did not trigger the deepfake detection policy.<br><br>* 2: Block. The detected content triggered the deepfake detection policy. |
|Decision.HitStrategyIDs |rule\-d87gnhdtmscn1mp2\*\*\*\* |List of triggered policy IDs, indicating all policies triggered by the content. Only built\-in detection policies for the deepfake detection scenario (with fixed IDs) are effective; other custom policies will not take effect. |
|ContentInfo |png |Content format.<br><br><br>* Image: Supports `jpg`, `jpeg`, `png`, `webp`<br><br>* Video: Supports `mp4`, `avi` |


<span id="891dff0f"></span>
## Step 5: View detection logs

After the request is complete, review the corresponding logs in the console for auditing and troubleshooting.


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield).

2. In the left menu bar, select **Attack Logs**.

3. On the **Deepfake logs** tab, view logs where the verdict is **Manipulated**.

   Test results are displayed separately for each image or video, including whether the sample is identified as manipulated content, the triggered manipulation labels, and the confidence score.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">A single sample may trigger multiple manipulation labels. We recommend reviewing the results against the original image or video.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ae14651b10bb4435b4973f26fab634c3) </span>


&nbsp;
