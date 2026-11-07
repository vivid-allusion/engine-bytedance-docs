---
title: "Video and Image Understanding"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1408245"
---

In addition to voice interaction, you can integrate a visual understanding model to enable vision capabilities for your agent. This allows it to comprehend real\-time video frames or images, supporting visual interactions such as video calls, image\-based questions, and photo object recognition.

<span id="60433fd5"></span>
## Restrictions

This feature is supported only by the Model Ark LLMs and third\-party LLMs / Agents, and the models must possess visual understanding capabilities.

> For models on the Model Ark that support video understanding, see [Model List-Visual understanding](https://docs.byteplus.com/en/docs/ModelArk/1330310#ff5ef604).


<span id="ea6ad001"></span>
## Video Understanding vs. Image Understanding

&nbsp;


|Solution |Video understanding |Image understanding |
|---|---|---|
|**Interaction mode** |Passive continuous perception. The agent continuously subscribes to RTC real\-time video streams and automatically extracts frames in the background to analyze the live images, enabling video calls with real people. |Active single request. The user sends one or more images to the agent at a specific time and asks questions. |
|**Data sources** |Real\-time video streams published by the RTC client (camera or screen sharing). |Static images actively uploaded via API (URL or Base64). |
|**Use cases** |Scenarios where the agent needs to continuously observe and provide feedback, such as real\-time environment perception, AR visual guidance, and game companion. |One\-time analysis scenarios actively triggered by the user, such as object recognition by taking photos, album image analysis, and screenshot Q&A. |


<span id="9623a291"></span>
## Video Understanding

The agent service automatically captures frames from the real\-time video stream and sends the images to the LLM for analysis.

<span id="562f270d"></span>
### Procedure


1. **Client: Enable video capture**.

   1. Establish basic audio and video calls, and ensure that video capture is enabled via the RTC SDK API (`startVideoCapture`) and the video stream is published.

   2. (Recommended) Call `setLocalVideoMirrorType` to set video mirroring, ensuring the agent sees the correct orientation of the video (for example, text is not reversed).

      On mobile devices or hardware with cameras, the local preview from the front camera is usually mirrored. If this view is sent directly to the agent, it may result in incorrect understanding of spatial relationships or text orientation. It is recommended to set the correct mirroring mode according to the camera in use, ensuring the video stream sent to the agent has the correct orientation.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details on video capture and video mirroring interfaces on each platform, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-client-api">Client API</a>.   </div>
   

2. **Server: Enable visual capabilities.** 

   When enabling a task, call `StartVoiceChat` or, after starting the task, call `UpdateVoiceChat` and configure `LLMConfig.VisionConfig`:

   * `Enable`: **Required**. Set to `true` to enable visual understanding capabilities.

   * `SnapshotConfig`: **Optional**. Adjust the screenshot frequency (Interval) and stream type (StreamType) according to the scenario; see [VisionConfig Examples](https://docs.byteplus.com/docs/byteplus-rtc/docs-1408245#6c1c4a7c).

   * `StorageConfig`: **Optional**. Configure the storage location for screenshots (server or TOS).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If configured for TOS storage, you must first enable the <a href="https://console.byteplus.com/tos/bucket">BytePlus TOS service</a>, create a bucket, and grant TOS cross\-service authorization for the RTC service.      </div>
      

After completing the configuration, start the agent and turn on the camera to begin video interaction with the agent.

<span id="6c1c4a7c"></span>
### VisionConfig Examples

Here are recommended configurations for popular use cases:


<Tabs>
<Tab zoneid="sBbBriG7Tm" title="AI social">
<TabTitle>AI social</TabTitle>

The scene changes slowly in this scenario, and the requirements for real\-time performance are not high. A lower screenshot frequency and fewer images can be used to save costs.

```JSON
"VisionConfig": {
    "Enable": true,
    "SnapshotConfig": {   
        "StreamType": 0,      // 0: Main stream (camera)
        "ImageDetail": "low", // Low detail mode
        "Height": 480,        // Resolution
        "Interval": 1000,     // Capture one image per second
        "ImagesLimit": 2      // Send two images each time
    }
}
```



</Tab>
<Tab zoneid="dnSz8pMoTu" title="Game companion">
<TabTitle>Game companion</TabTitle>

Game screens change rapidly, requiring the AI to process information in real time. We recommend increasing the screenshot frequency and image quality to ensure responsive performance.

```JSON
"VisionConfig": {
    "Enable": true,
    "SnapshotConfig": {
        "StreamType": 1,       // 1: Screen stream
        "ImageDetail": "high", // High detail mode
        "Height": 720,         // High resolution
        "Interval": 200,       // Capture one image every 200 ms
        "ImagesLimit": 10      // Send ten images each time
    }
}
```



</Tab>
</Tabs>


<span id="81d0177f"></span>
## Image Understanding

During the conversation, you can send one or more images to the agent at any time via the client or server and ask questions. It supports multiple image uploads and chunked image uploads.


* Client implementation: Supports images in Base64 and URL formats, and Base64 images support chunked uploads. The image data uploaded in a single operation must not exceed 64 KB.

* Server implementation: Only images in URL format are supported.


<span id="5f4b34be"></span>
### Client Implementation (supports Base64/URL)


1. Enable visual understanding capability.

   When calling `StartVoiceChat`, set `LLMConfig.VisionConfig.Enable` to `true`.

2. Call the `ByteRTC SDK` [sendUserBinaryMessage](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTSRoom-senduserbinarymessage) interface to send images.

   * `userId`: Enter the agent ID (the `AgentConfig.UserId` configured in `StartVoiceChat`).

   * `buffer`: Must meet the following requirements:

      * **Size limit**: The binary message content (buffer) sent by this interface in a single operation must not exceed 64 KB. If the image is large, you must call this interface multiple times for chunked upload. It is recommended to keep the size of each chunk within 60 KB to reserve space for other JSON fields. For configuration methods, see [Examples](https://docs.byteplus.com/docs/byteplus-rtc/docs-1408245#7665d419).

      * **Chunked upload of Base64 images**:

      * **Message format**:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5f49c0ca26d16c6e300267b8fd76ef6.jpg) </span>

   
   |Parameter name |Type |Description |
   |---|---|---|
   |magic_number |binary |Fixed string `ctrl`, indicating a control message. |
   |length |binary |The byte length of control_message, stored in big\-endian format. |
   |control_message |binary |JSON object containing instructions and image information. |
   

   control_message

&nbsp;

   
   |Parameter |Type |Required |Description |
   |---|---|---|---|
   |Command |String |Yes |Fixed as `ExternalTextToLLM`. |
   |Message |String |No |Text question associated with the image.<br><br><br>* For chunked/multipart image uploads: only include the `Message` parameter in the final request; previous requests can use an empty string `""`. For images uploaded first, the system only caches the images in the current context.<br><br>* To ask a question immediately, include the `Message` parameter. The system will then send the image and text to the LLM simultaneously, triggering a voice reply. |
   |InterruptMode |Int |Yes |Interrupt priority.<br><br><br>* `1`: High priority. The agent will terminate the current interaction, send the text to the large language model (LLM) for processing, and output the result.<br><br>* `2`: Medium priority. The agent will send the text to the large language model (LLM) for processing and output the result after the current interaction ends.<br><br>* `3`: Low priority. If the agent is currently interacting, it will directly discard the incoming text content. If not interacting, the agent will send the text to the LLM for processing and output the result. |
   |ImageConfig |object |Yes |Image configuration. |
   

   ImageConfig

&nbsp;

   
   |Parameter |Type |Required |Description |
   |---|---|---|---|
   |Action |String |Yes |Operation on the image. The possible values are as follows:<br><br><br>* `insert`: Upload an image. The system will cache the uploaded image.<br><br>* `delete`: Delete the image cache for the specified `GroupID`. |
   |GroupID |Integer |Yes |Image round ID.<br><br><br>* When Action is `insert`: Used to associate images and text in the same conversation round. This ID is defined and maintained by you, and must increase sequentially.<br><br>* When Action is `delete`: Specify `GroupID` to clear the image cached by the system. |
   |ImageType |String |No |The data type of the image to be uploaded. Required when `Action` is `insert`. The possible values are as follows:<br><br><br>* `base64`: Image data encoded in Base64.<br><br>* `url`: The URL of the image. |
   |Images |String[] |Yes |Array of image data (Base64 strings or URLs).<br><br><br>* The message content must not exceed 60 KB.<br><br>* When passing a URL, please ensure the URL is accessible from the public internet. |
   |Total |Int |No |The total number of `sendUserBinaryMessage` calls required for the current `GroupID`.<br><br>Formula: `Total` = (Number of fragments for Image1) + (Number of fragments for Image2) + ...<br><br>For example, in GroupID=1, if two images need to be sent in 5 transmissions, then `Total` is 5.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid and required only when <code>ImageType</code> is <code>base64</code>.</div><br> |
   |ImageID |Int |No |The ID of the image, used for sorting. When uploading multiple images in the same round (`GroupID`), assign a unique, sequential `ImageID` to each image, starting from 1.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Valid and required only when <code>ImageType</code> is <code>base64</code>.</div><br> |
   |IsPartial |Bool |No |Whether it is a fragment:<br><br><br>* `true`: Indicates this is a fragment.<br><br>* `false` (default value): Indicates a complete image. When uploading a complete image or the last fragment in a multipart upload, set `IsPartial` to `false`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Valid only when <code>ImageType</code> is <code>base64</code>, and required for fragmented uploads.</div><br> |
   |FragmentID |Int |No |Fragment ID, starting from 1 and increasing. The system will concatenate the image fragments according to the order.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Valid only when <code>ImageType</code> is <code>base64</code>, and required for fragmented uploads.</div><br> |
   


<span id="7665d419"></span>
#### Examples

Examples of JSON content constructed for different scenarios are as follows:


<Tabs>
<Tab zoneid="qJLDUjC7pk" title="Example 1: Upload a Base64 image (no fragments)">
<TabTitle>Example 1: Upload a Base64 image (no fragments)</TabTitle>

After compressing the image to less than 60 KB, send it directly and ask a question immediately.

```JSON
{
    "Command": "ExternalTextToLLM",
    "Message": "Analyze this logo",
    "InterruptMode": 1,
    "ImageConfig": {
        "Action": "insert",
        "GroupID": 100,
        "ImageType": "base64",
        "Images": ["iVBORw0KGgoAAA..."], 
        "Total": 1,      // Only one packet is sent in total
        "ImageID": 1,
        "IsPartial": false
    }
}
```



</Tab>
<Tab zoneid="zULF0bZjA4" title="Example 2: Send a URL image">
<TabTitle>Example 2: Send a URL image</TabTitle>

Upload an image stored in TOS and ask a question immediately.

```JSON
{
    "Command": "ExternalTextToLLM",
    "Message": "What is in this image?", // Ask immediately
    "InterruptMode": 1,
    "ImageConfig": {
        "Action": "insert",
        "GroupID": 101,
        "ImageType": "url",
        "Images": ["https://your-bucket.com/image.jpg"]
    }
}
```



</Tab>
<Tab zoneid="hyvbGn6FQv" title="Example 3: Single Base64 image (multipart upload)">
<TabTitle>Example 3: Single Base64 image (multipart upload)</TabTitle>

When a Base64\-encoded image exceeds the size limit, you need to split it into multiple parts and send them by calling `sendUserBinaryMessage` multiple times.


1. First call (send Part 1).

   ```JSON
   {
       "Command": "ExternalTextToLLM",
       "Message": "",    // No text is sent in intermediate fragments
       "InterruptMode": 1,
       "ImageConfig": {
           "Action": "insert",
           "GroupID": 200,
           "ImageType": "base64",
           "Images": ["base64_part_1..."],
           "Total": 2,       // Plan to send two packets in total
           "ImageID": 1,     // First image
           "IsPartial": true, // Is a fragment
           "FragmentID": 1   // First fragment
       }
   }
   ```
   

2. Second call (send Part 2 and ask a question).

   ```JSON
   {
       "Command": "ExternalTextToLLM",
       "Message": "How many people are in the picture?", // The last fragment includes the question to trigger the AI response
       "InterruptMode": 1,
       "ImageConfig": {
           "Action": "insert",
           "GroupID": 200,
           "ImageType": "base64",
           "Images": ["base64_part_2..."],
           "Total": 2,       // Remain consistent
           "ImageID": 1,     // Remain consistent
           "IsPartial": false, // Set the last fragment to false
           "FragmentID": 2
       }
   }
   ```
   


</Tab>
<Tab zoneid="oFrnbr9uTF" title="Example 4: Upload Base64 images in the same round">
<TabTitle>Example 4: Upload Base64 images in the same round</TabTitle>

Suppose you need to show two images (Image1 and Image2) to the AI at once and ask a question based on them. Image1 is 40 KB and does not need to be split; Image2 needs to be split into 2 fragments. The entire process belongs to the same round of Q&A, and the GroupID remains unchanged.

`Send Image1 (Complete)` \-\> `Send Image2 (Part 1)` \-\> `Send Image2 (Part 2) + Question`

All three `sendUserBinaryMessage` calls use the same `GroupID`.


1. Upload Image1.


```JSON
// First call to sendUserBinaryMessage
{
    "Command": "ExternalTextToLLM",
    "Message": "", 
    "InterruptMode": 1,
    "ImageConfig": {
        "Images": ["Image1...."],
        "ImageType": "base64",
        "Action": "insert",
        "GroupID": 200,
        "Total": 3,   // Plan to send three packets in total
        "ImageID": 1,  
        "IsPartial": false  // Complete image
    }
}
```



2. Upload Image2.

   1. Fragmented upload of Image2_Part1:

   ```JSON
   // Second call to sendUserBinaryMessage
   {
       "Command": "ExternalTextToLLM",
       "Message": "", // When dealing with partial images, there is no need to transmit text content.
       "InterruptMode": 1,
       "ImageConfig": {
           "Images": ["Image2_Part1...."],
           "ImageType": "base64",
           "Action": "insert",
           "GroupID": 200,
           "Total": 3,
           "ImageID": 2,  // This is the second image
           "IsPartial": true,  // This is a fragment
           "FragmentID": 1    // This is the first fragment
       }
   }
   ```
   

   2. Fragmented upload of Image2_Part2:

   ```JSON
   // Third call to sendUserBinaryMessage
   {
       "Command": "ExternalTextToLLM",
       "Message": "What is in this image?", // When sending the last image information, transmit text content.
       "InterruptMode": 1,
       "ImageConfig": {
           "Images": ["Image2_Part2...."],
           "ImageType": "base64",
           "Action": "insert",
           "GroupID": 200,
           "Total": 3,
           "ImageID": 2,
           "IsPartial": false,  // Set the last fragment to false
           "FragmentID": 2   // This is the second fragment
       }
   }
   ```
   


</Tab>
</Tabs>


<span id="80df833c"></span>
### Server Implementation (URL only)


1. Enable visual understanding capability.

   Call `StartVoiceChat` and set the `Enable` property in the `LLMConfig.VisionConfig` object to `true` to enable visual understanding capability.

2. Pass in the image. Call the `UpdateVoiceChat` interface and configure the following parameters:

&nbsp;

   
   |Parameter |Required? |Description |
   |---|---|---|
   |AppId |Yes |Your application's `AppId`. This must match the `AppId` from the `StartVoiceChat` request. Can be obtained from [BytePlus RTC Console-App management](https://console.byteplus.com/rtc/listRTC). |
   |RoomId |Yes |Room ID for the call. Must be consistent with the RoomId used when starting the task by calling `StartVoiceChat`. |
   |TaskId |Yes |ID of the target agent task. Must be consistent with the TaskId defined when starting the task by calling `StartVoiceChat`. |
   |Command |Yes |Set to `ExternalTextToLLM`. |
   |Message |No |Text question associated with the image.<br><br><br>* If not provided: only the image is cached, the agent will not respond, and it will wait for subsequent instructions.<br><br>* If text is provided: the agent will respond immediately. |
   |InterruptMode |Yes |Processing priority.<br><br><br>* `1`: High priority. The agent will terminate the current interaction, send the text and image to the large model for processing, and output the result.<br><br>* `2`: Medium priority. The agent will send the text and image to the large model for processing and output the result after the current interaction ends.<br><br>* `3`: Low priority. If the agent is currently interacting, it will directly discard the incoming text and image content. If not interacting, the agent will send the text and image to the large model for processing and output the result. |
   |ImageConfig |Yes |Configure the image to be provided. |
   

   **Sample request**: Sending a TOS image with an accompanying question.

   ```JSON
   {
       "AppId": "your_app_id",
       "RoomId": "your_room_id",
       "TaskId": "your_task_id",
       "Command": "ExternalTextToLLM",
       "Message": "Summarize the content of this image.",
       "InterruptMode": 1,
       "ImageConfig": {
           "Action": "insert",
           "GroupID": 104,
           "ImageType": "url",
           "Images": ["https://your-tos-bucket.volces.com/summary_image.jpg"]
       }
   }
   ```
   


<span id="f419bd64"></span>
### Delete Specified Image

The agent service temporarily caches the images you upload to associate them with subsequent voice questions. After a round of visual Q&A ends, you can proactively clear the cache to free up resources.


* **Implementation method**: Send an instruction with `Action` set to `delete` and specify the `GroupID` to be deleted.

* **Example**: Delete the image cache with a `GroupID` of `104`.

   **Client implementation**:

   ```JSON
   // The client sends the following JSON via sendUserBinaryMessage
   {
       "Command": "ExternalTextToLLM",
       "Message": "",
       "InterruptMode": 1,
       "ImageConfig": {
           "Action": "delete",
           "GroupID": 104
       }
   }
   ```
   

   **Server implementation**:

   ```JSON
   // The server sends the following JSON via UpdateVoiceChat
   {
       "AppId": "your_app_id",
       "RoomId": "your_room_id",
       "TaskId": "your_task_id",
       "Command": "ExternalTextToLLM",
       "Message": "",
       "InterruptMode": 1,
       "ImageConfig": {
           "Action": "delete",
           "GroupID": 104
       }
   }
   ```
