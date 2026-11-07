---
title: "Video transcoding"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-transcoding"
---

Video transcoding allows you to process video files stored in TOS by converting their format, codec, resolution, bitrate, and other parameters. The feature produces output files based on specific templates, which makes it easier to adapt playback, reduce file size, and distribute files across multiple devices.

<span id="mZGBwoFr"></span>
## Billing notes

Video transcoding is currently free. We will announce in advance if it becomes a paid feature. To avoid unexpected costs due to changes in billing rules, please stay tuned to our announcements.

<span id="3CgJgmZc"></span>
## Prerequisites

Before you begin, make sure that you have completed the following:


|Item |Description |
|---|---|
|Cross\-service authorization |You have authorized TOS to access the files in the bucket so that it can read the source video and write the transcoded one. |
|KMS authorization |If the source or transcoded video file involves server\-side encryption, you have authorized TOS to access Key Management Service (KMS). This enables TOS to read, process, or write encrypted files. |
|Source video file |The video file to be transcoded has been uploaded to the bucket and is in MP4, TS, or HLS format. |
|Save path |You have chosen a save path for the transcoded video file in order to prevent overwriting existing files or writing to the wrong directory. |


<span id="QQ9X9pIZ"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, select **Data processing** \> **task processing**.

6. On the **task processing** page, click **Create task** on the **Video transcoding** tab.

7. In the **Create video transcoding task** dialog box, configure the following parameters.

   
   |Parameter |Required |Description |
   |---|---|---|
   |Source file path |Yes |Select the source video file to be transcoded. |
   |Target bucket |Yes |Select the bucket where you want to save the transcoded video file. |
   |Target file path |No |Enter the path where you want to store the transcoded video file. If this field is left empty, the file will be saved to the root directory of the bucket by default. |
   |Target file name |Yes |Enter the name of the output file after transcoding. |
   |Transcoding template type |Yes |Select the template type for the transcoding task. The options include **System default template** and **Custom template**. |
   |Transcoding template |Yes |Select a transcoding template. This template defines the output parameters, including the video codec, resolution, and bitrate.<br><br>For more information about templates, see [Creating custom templates](https://docs.byteplus.com/en/docs/tos/Template-management?lang=en) for instructions. |
   

8. Once you have finished configuring, click **OK**.


<span id="MisdkBPR"></span>
## Managing video transcoding tasks

The **Video transcoding** tab on the **task processing** page shows you the list of created tasks and lets you perform operations on them.


|Operation |Steps |
|---|---|
|View task details |Click the ID of the task you want to check. This will take you to the details page, where you can find the **Basic information**, **Enter information**, and **Output information**. |
|Search for a task |At the top of the task list, select a time range to filter tasks or search for a task using its ID. |
