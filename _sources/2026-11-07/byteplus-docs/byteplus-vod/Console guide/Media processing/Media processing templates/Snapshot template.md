---
title: "Snapshot template"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-snapshot-template"
---

This guide provides step\-by\-step instructions for creating and configuring templates for static, sampled, dynamic, and sprite snapshots.

## Snapshot types

BytePlus VOD offers a range of snapshot options to enhance your video experience. Take a look at the following types of snapshots supported:

* **Static snapshots**: Capture still frames from your video, which can be used as candidates for video covers or thumbnails.

* **Sampled snapshots**: Extract multiple images at regular time intervals or evenly spaced frames throughout the video. This allows you to create a sequence of snapshots that provide a visual representation of the video's content.

* **Dynamic snapshots and looped dynamic snapshots**: Transform a segment of your video into animated GIFs or looped GIFs. These dynamic snapshots can be shared and used to add visual interest or highlight specific moments within your content.

* **Sprite snapshots**: Combine multiple snapshots into a single image, commonly known as a sprite. Sprites are particularly useful for previewing the video content when users drag the player progress bar. They provide a visual overview of the video's key frames, enabling users to quickly navigate through the content.

## Creating a snapshot template

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar.

3. On the **Spaces** page, click **Enter space**.

4. Click **Media processing \> Templates**.

5. Click the **Snapshot** tab.

6. Click **Add snapshot template**.

7. In the dialog box that appears, configure the basic information and snapshot parameters based on your specific business requirements. For details, see the following documentation:

   * [Configuring basic information](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template#6ae09037)

   * [Configuring static snapshot parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template#2ecbec03)

   * [Configuring sampled snapshot parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template#2d8975ef)

   * [Configuring dynamic snapshot parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template#181cd5f4)

   * [Configuring looped dynamic snapshot parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template#68a032ec)

   * [Configuring sprite snapshot parameters](https://docs.byteplus.com/docs/byteplus-vod/docs-snapshot-template#7b61b3c1)

8. Click **Save**.

## Configuring the basic information

|**Parameter** |**Description** |
|---|---|
|Template name |The length of the template name cannot exceed 64 characters. It is recommended to use a name that can identify the content of the template. |
|Template description |The length of the template description cannot exceed 140 characters. |
|Snapshot type |This parameter offers the following options:<br><br><br>* Static snapshots<br><br>* Sampled snapshots<br><br>* Dynamic snapshots<br><br>* Looped dynamic snapshots<br><br>* Sprite snapshots |

## Configuring static snapshot parameters

|**Parameter** |**Description** |
|---|---|
|Image format |For static snapshots, the supported image format is JPEG. |
|Image size |This parameter offers the following options:<br><br><br>* **Specify width**: With this option, you are required to specify the desired width of the snapshots. The height will be automatically set based on the aspect ratio of the input video to ensure that the snapshots maintain the correct proportions. The acceptable value range for the width is from 1 to 4096.<br><br>* **Specify width and height**: With this option, you are required to specify both the width and height of the snapshots. BytePlus VOD will crop the snapshots from the center of the input video to match the specified dimensions. The acceptable value range for both the width and height is from 1 to 4096. Specifying the width and height as 0 means maintaining the size of the input video. |
|Snapshot time |The specific time within the video where a snapshot is taken. |

## Configuring sampled snapshot parameters

|**Parameter** |**Description** |
|---|---|
|Image format |For sampled snapshots, the supported image format is JPEG. |
|Image size |This parameter offers the following options:<br><br><br>* **Specify width**: With this option, you are required to specify the desired width of the snapshots. The height will be automatically set based on the aspect ratio of the input video to ensure that the snapshots maintain the correct proportions. The acceptable value range for the width is from 1 to 4096.<br><br>* **Specify width and height**: With this option, you are required to specify both the width and height of the snapshots. BytePlus VOD will crop the snapshots from the center of the input video to match the specified dimensions. The acceptable value range for both the width and height is from 1 to 4096. Specifying the width and height as 0 means maintaining the size of the input video. |
|Snapshot method |This parameter offers the following options:<br><br><br>* **Take snapshots at specified intervals**: With this option, you can specify a time interval at which snapshots should be taken. For example, you can set snapshots to be captured every 10 seconds.<br><br>* **Take a specified number of snapshots**: This option allows you to specify the exact number of snapshots you want to capture from the video. For example, you can choose to capture 5 snapshots evenly distributed throughout the video. |
|Snapshot interval |Specify the time interval at which snapshots should be taken. The default value is 10 seconds. The maximum number of snapshots is 50. |
|Number of snapshots |Specify the exact number of snapshots you want to capture from the video. The default value is 10. The maximum number of snapshots is 50. |
|Random snapshot |By default, when taking snapshots in BytePlus VOD, they are evenly distributed throughout the video. However, if you enable random snapshot, the snapshots will be taken randomly. |

## Configuring d**ynamic** snapshot parameters

|**Parameter** |**Description** |
|---|---|
|Image format |For dynamic snapshots, the supported image formats are:<br><br><br>* GIF<br><br>* WebP |
|Image size |This parameter offers the following options:<br><br><br>* **Specify width**: With this option, you are required to specify the desired width of the snapshots. The height will be automatically set based on the aspect ratio of the input video to ensure that the snapshots maintain the correct proportions. The acceptable value range for the width is from 1 to 4096.<br><br>* **Specify width and height**: With this option, you are required to specify both the width and height of the snapshots. BytePlus VOD will crop the snapshots from the center of the input video to match the specified dimensions. The acceptable value range for both the width and height is from 1 to 4096. Specifying the width and height as 0 means maintaining the size of the input video. |
|Snapshot time |The specific time within the video where the dynamic snapshot begins. |
|Segment duration |Specify the duration of the segment of the video that is used to create the dynamic snapshot. The default value is 5000 ms. It must be set as a positive integer, with a maximum value of 100,000 ms. |
|Frame rate |A higher frame rate for dynamic snapshots results in smoother animations but also larger output files. The default frame rate is 10 frames per second. The unit is frames per second (fps), and the valid range is [10, 60]. |
|Playback speed |The default playback speed is 1. It can be adjusted within the range of [0.5, 2]. A higher speed value accelerates the playback of dynamic snapshots, while a lower value slows down the playback. |

## Configuring looped d**ynamic** snapshot parameters

|**Parameter** |**Description** |
|---|---|
|Image format |For looped dynamic snapshots, the supported image format is WebP. |
|Image size |This parameter offers the following options:<br><br><br>* **Specify width**: With this option, you are required to specify the desired width of the snapshots. The height will be automatically set based on the aspect ratio of the input video to ensure that the snapshots maintain the correct proportions. The acceptable value range for the width is from 1 to 4096.<br><br>* **Specify width and height**: With this option, you are required to specify both the width and height of the snapshots. BytePlus VOD will crop the snapshots from the center of the input video to match the specified dimensions. The acceptable value range for both the width and height is from 1 to 4096. Specifying the width and height as 0 means maintaining the size of the input video. |
|Snapshot time |The specific time within the video where the dynamic snapshot begins. |
|Number of snapshots |Specify the exact number of snapshots you want to capture from the video. The default value is 9. The maximum number of snapshots is 100. |
|Frame rate |A higher frame rate for dynamic snapshots results in smoother animations but also larger output files. The default frame rate is 10 frames per second. The unit is frames per second (fps), and the valid range is [10, 60]. |

## Configuring sprite snapshot parameters

|**Parameter** |**Description** |
|---|---|
|Image format |For sprite snapshots, select `jpeg` or `webp`. The default is `jpeg`. |
|Image size |Specify both the width and height of the snapshots. BytePlus VOD will crop the snapshots from the center of the input video to match the specified dimensions. The acceptable value range for both the width and height is from 1 to 4096. Specifying the width and height as 0 means maintaining the size of the input video. |
|Number of snapshots |Specify the exact number of snapshots you want to capture from the video. |
|Snapshot interval |Specify the time interval at which snapshots should be taken.<br><br>> **Note**<br><br><br><br>* > You are required to provide either the number of snapshots or the snapshot interval.<br><br><br>* > If you specify only the number of snapshots, snapshots are evenly distributed throughout the video.<br><br><br>* > If you specify only the snapshot interval, the number of snapshots varies based on the duration of the video.<br> |
|Sprite arrangement |Configures the arrangement of snapshots in a sprite. For example, if the total number of snapshots is 10 and you want them to be arranged in a 2\-row by 2\-column grid, it will result in 3 sprites. The first two sprites will contain 4 snapshots each, and the last sprite will contain 2 snapshots. In the last sprite sheet, the remaining 2 empty slots will be filled with black bars. |
