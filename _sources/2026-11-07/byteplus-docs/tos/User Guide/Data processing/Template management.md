---
title: "Template management"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Template-management"
---

Template management allows you to create and manage task templates, such as those for audio and video transcoding. A template defines parameters such as container and codec formats, resolution, and bitrate. When creating a transcoding task, you can select a template to automatically configure the task.

<span id="CGWEyO4u"></span>
## Template type


|Type |Description |
|---|---|
|Audio transcoding |Templates that define the following audio output parameters: output format, sample format, sample rate, number of channels, and segment start time and duration.  |
|Video transcoding |Templates that define the following video and audio output parameters: output format, video codec format, bitrate control policy, resolution, frame rate, audio encoding format, sample rate, and number of audio channels.  |
|System default template |Default templates provided by the system. You can select them directly when you create a transcoding task. |
|Custom template |Templates that you create based on your needs. These templates are ideal for scenarios requiring customized output formats, clarity, bitrate, and audio parameters. |


<span id="5mCH5E1o"></span>
## Creating a custom template


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, select **Data processing** \> **Template management**.

6. On the **Template management** page, select the desired tab and create a template.

   
   <Tabs>
   <Tab zoneid="e1UEMh9lz3" title="Audio transcoding">
   <TabTitle>Audio transcoding</TabTitle>
   
   Click **Create audio transcoding template**, and configure the following parameters.
   
   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |Template name |Yes |Enter a name for the audio transcoding template. This name will be used to identify the template in the template list and when you create tasks. The following constraints apply:<br><br><br>* Only uppercase and lowercase letters (A–Z, a–z), numbers (0–9), underscore (_), hyphen (\-), and period (.) are allowed.<br><br>* Length must not exceed 64 characters. |
   |Start time |No |Specify where in the source audio transcoding should begin. If this is not specified, transcoding will start from the beginning of the audio. |
   |Duration |No |Specify how much of the source audio should be transcoded. If this is not specified, the entire audio will be processed. |
   |Output format |Yes |Select an output format for the output audio. Options: WAV, MP3, AAC, FLAC, OGA, AC3, and OPUS. |
   |Sampling format |No |Select a storage format for the audio sample data. Currently, only s16 is available. |
   |Sampling rate |Yes |Select a sample rate for the output audio. The sample rate determines how many samples are captured per second. A higher value yields better quality. Options: 8000, 11025, 12000, 16000, 22050, 24000, 32000, 44100, 48000, 88200, and 96000 Hz. |
   |Channel number |No |Specify the number of output audio channels. If this is not specified, the number of channels will be the same as the source audio. Options: 1 (Mono) or 2 (Stereo). |
   
   
   
   
   
   </Tab>
   <Tab zoneid="hDKbGKEU5i" title="Video transcoding">
   <TabTitle>Video transcoding</TabTitle>
   
   Click **Create video transcoding template** and configure the parameters in the order displayed in the wizard.
   
   <span id="pnsaIl5H"></span>
   ### Basic information
   
   <span id="pzTepn44"></span>
   ### 
   |**Parameter** |**Description** |
   |---|---|
   |Template name |Enter a name for the video transcoding template. This name will be used to identify the template in the template list and when you create tasks. The following constraints apply:<br><br><br>* Only uppercase and lowercase letters (A–Z, a–z), numbers (0–9), underscore (_), hyphen (\-), and period (.) are allowed.<br><br>* Length must not exceed 64 characters. |
   |Transcoding type |Select the transcoding task type. Options: **Video transcoding** and **Audio transcoding**. |
   |Output format |Select a container format for the output file. Options: MP4, TS, and HLS. |
   |Start time |Specify where in the source video transcoding should begin. If this is not specified, transcoding will start from the beginning of the video. |
   |Duration |Specify how much of the source video should be transcoded. If this is not specified, the entire video will be processed. |
   
   
   <span id="3njPgpQG"></span>
   ### Video parameters
   
   
   |**Parameter** |**Description** |
   |---|---|
   |Delete video stream |* On: The output file retains only the audio content and not the video stream.<br><br>* Off: You can continue to configure video parameters. |
   |Video coding format |Select a codec for the output video. Options: H.264 and H.265. |
   |Bitrate control policy |Select a method for managing the video bitrate: **No settings**, **Bitrate control factor**, or **Custom bitrate**.<br><br><br>* **Bitrate control factor**: Enter an integer between 1 and 51. 0 means not set. A lower value yields better quality and a larger file size, and vice versa.<br><br>* **Custom bitrate**: Enter an integer between 10 and 50,000 Kbps. A higher value yields better quality and a larger file size. |
   |Image resolution |Select a resolution mode for the output video. Options:<br><br><br>* **Retain source video image resolution**: The output video will have the same resolution as the source video.<br><br>* **By width settings image resolution**: Specify a custom width and height for the output video. Please note that:<br><br>   * Both the width and height must be even numbers between 128 and 4096.<br><br>   * If you specify only one dimension, the other is automatically scaled proportionally to avoid distortion. |
   |Video color format |Select a color format for the output video to determine how pixel data is represented. Currently, only yuv420p is available. |
   |Video frame rate |Specify the number of frames per second (FPS) for the output video. |
   
   
   <span id="lxTfR52K"></span>
   ### Audio parameters
   
   
   |**Parameter** |**Description** |
   |---|---|
   |Delete audio stream |* On: The output file does not retain the audio stream.<br><br>* Off: You can continue to configure audio parameters. |
   |Audio coding format |Select an encoding format for the output audio. Options: MP3 and AAC. |
   |Audio bitrate |An audio bitrate is only required after an audio codec has been selected<br><br>Enter an integer between 8 and 1000 Kbps. A higher value yields better quality and a larger file size. |
   |Sampling format |Select a storage format for the audio sample data. Options: fltp, s16p, and s32p. |
   |Sampling rate |Select a sample rate for the output audio. The sample rate determines how many samples are captured per second. A higher value yields better quality. Options: 8000, 11025, 12000, 16000, 22050, 24000, 32000, 44100, and 48000 Hz. |
   |Channel number |Specify the number of output audio channels. Options: 1 (Mono) or 2 (Stereo). |
   
   
   
   
   
   </Tab>
   </Tabs>
   

7. Once you have finished configuring, click **OK**.


<span id="QqTqC3Nk"></span>
## Other operations

The **Template management** page shows you the list of created templates and lets you perform operations on them.


|**Operation** |**Steps** |
|---|---|
|Viewing template details |On the audio transcoding or video transcoding tab, click a template to view its details, including **Basic information**, **Video parameters**, and **Audio parameters**. |
|Filter templates |At the top of the list, select either **System default template** or **Custom template** to filter templates by type, or search for a template using its ID. |
|Delete a template |Click **Delete** in the **Actions** column of the template you want to remove. Then, follow the instructions on the page to finish deleting it. |
