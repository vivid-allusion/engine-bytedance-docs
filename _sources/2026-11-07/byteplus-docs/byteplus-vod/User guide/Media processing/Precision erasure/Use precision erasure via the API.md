---
title: "Use precision erasure via the API"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/precision-erasure-api"
---

This guide walks you through using the BytePlus VOD precision erasure API to remove hardcoded subtitles and text from videos. It covers a quickstart for common subtitle erasure scenarios, as well as advanced configurations for fine\-grained control over erasure areas, text types, and time segments.

<span id="e2cd8060"></span>
## Prerequisites


* Ensure you [have created a BytePlus account](https://console.byteplus.com/auth/signup/) and sign in to the BytePlus console.

* Ensure you have enabled the BytePlus VOD service and created a space.

* Ensure you have uploaded video files to the target space, and obtained the Vid or FileName.


<span id="15a7113a"></span>
## Quickstart: **Short\-form drama subtitle erasure**

The following steps guide you through using minimal configuration to quickly implement automatic subtitle detection and erasure for Chinese and English short\-form drama scenarios.

<span id="979ef372"></span>
### Step 1: Submitting a subtitle erasure task

Call `StartExecution` to submit a subtitle erasure task. The following core parameters are required. For details on the request parameters, see [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-precision-erasure).


* `Input`: Specify the input video file.

   * `Type`: Set to `Vid` or `DirectUrl`.

   * `Vid` / `DirectUrl`: Provide the Vid or FileName of the file to be processed.

* `Operation.Task`: Specify the task to be performed.

   * `Type`: Set to `Erase` to perform the subtitle erasure task.

   * `Erase.Mode`: Set to `Auto`. The system will automatically enable OCR and perform erasure based on the recognition results.

   * `Erase.Auto.Type`: Set to `Subtitle`. This limits the erasure to subtitles only.

   * `Erase.Auto.SubtitleFilter`: Set to an empty JSON object `{}`.

   * `Erase.NewVid`: Set to `true` to generate a new Vid for the processed video.


In this configuration, the system automatically erases subtitles that meet the following criteria:


* **Position:**  Located within the bottom 50% of the video, and horizontally centered.

* **Size:**  The vertical character height is between 1% and 10% of the total video height.

* **Color:**  White.


Sample request:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The following HTTP example displays only core parameters and omits authentication details, such as the signature calculation in the <code>Authorization</code> header.</div>


```JSON
POST https://vod.byteplusapi.com?Action=StartExecution&Version=2025-07-01
{
    "Input": {
        "Type": "Vid",
        "Vid": "v0325cg10001*****"
    },
    "Operation": {
        "Type": "Task",
        "Task": {
            "Type": "Erase",
            "Erase": {
                "Mode": "Auto",
                "Auto": {
                    "Type": "Subtitle",
                    "SubtitleFilter":{}
                },
                "WithEraseInfo": true,
                "NewVid": true
            }
        }
    }
}
```


<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c21273764ee54495a04993b478dc97a6~tplv-goo7wpa0wc-image.image" controls></video>


<span id="step-2-getting-the-task-result"></span>
### Step 2: Getting the task result

After you submit the task, the system will process the task asynchronously. You can get the result through the following methods:


* **Active query:**  Call [GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution) and pass the `RunId` to retrieve the task result.

   ```HTTP
   GET https://vod.bytedanceapi.com?Action=GetExecution&Version=2025-07-01&RunId=hb:ebd05bee1f3873*****
   ```
   

* **Event notification:** 

   1. Add a callback subscription address and select [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete). For details, please refer to [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).

   2. When the task is completed, you will receive an HTTP POST request whose `EventType` is `ExecutionComplete`.

* **Console:**  You can check the execution status through the console.

   1. [Sign in to the VOD console](https://console.byteplus.com/vodpaas) and enter the specific space.

   2. Navigate to **Media processing** \> **Tasks** in the left navigation bar to check the status of the target task.


A status of "Success" indicates that the task has completed. You can get information about the processed file from the `Output.Task.Erase` field. The following sample shows the core response parameters:

```JSON
{
  "ResponseMetadata": {
    // ... Common metadata
  },
  "Result": {
    "RunId": "hb:e3eb1668d43fa761420ac95057****",
    "Status": "Success",
    // ... Task metadata, information of input and operation
    "Output": {
      "Type": "Task",
      "Task": {
        "Type": "Erase",
        "Erase": {
          "Duration": 57.099,
          "File": {
            "Size": "152295931",
            "FileName": "0b7c1420fee342e39792b847b8a****.mp4",
            "Vid": "v0ccfeg7007acsg***fog65ubr7niqng"
          },
          "Info": {
            "Width": 1080,
            "Height": 1920,
            "Areas": [
              {
                "Start": 0,
                "End": 57.08,
                "PixelRectangle": [
                  {
                    "TopLeftX": 108,
                    "TopLeftY": 960,
                    "BottomRightX": 1067,
                    "BottomRightY": 1919
                  }
                ]
              }
            ]
          }
        }
      }
    }
  }
}
```


<span id="63bc62d2"></span>
### Step 3: Obtaining the URL of the processed video

After obtaining the Vid of the processed video (returned only when you set `NewVid: true` in the request) and its FileName in [Step 2: Getting the task result](https://docs.byteplus.com/en/docs/25/104306#66af20a1), you need to generate a public URL for playback and download.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Before retrieving the public URL, you must <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-domain-name-configuring">add and configure a domain name</a> for the specified VOD space. All URLs generated are based on this domain name.</div>


<span id="bfec3ff4"></span>
#### Method 1: Calling GetPlayInfo

Call the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) API and pass the Vid. Upon a successful call, the system will return the URL in the `Result.PlayInfoList` field of the response body.

<span id="f94ac9af"></span>
#### Method 2: Manually constructing the URL using the FileName

A public URL consists of the following components: `[Protocol]://[PlaybackDomain]/[FileName]`


* `[Protocol]`: Generally `https` or `http`, depending on whether you [have configured an SSL certificate](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-ssl-certificates).

* `[PlaybackDomain]`: The playback domain name that you have configured in the VOD console.

* `[FileName]`: The FileName of the processed file retrieved from the task result.


Example: If your domain name is `play.example.com` and the `FileName` is `video.mp4`, the basic URL is `https://play.example.com/video.mp4`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To prevent unauthorized hotlinking, VOD supports URL signing. If you have enabled URL signing in the console, the basic URL will not grant access. You must append a dynamically calculated signing parameter (such as <code>auth_key</code>) to the URL.</div>



* <div data-tips="true" data-tips-type="tip"><strong>How to generate signing parameters:</strong> The URL signing follows a strict signing algorithm. For details, please see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview">URL signing overview</a>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Example of a full URL with signing:</strong><code>https://play.example.com/video.mp4?auth_key=1732529334-0-0-a1b2c3d4e5f6...</code></div>



<span id="617250f3"></span>
## Advanced usage

<span id="4e3c0ed0"></span>
### Erasing subtitles and other text

In `Auto` mode, if you want to erase subtitles and other text (such as text watermarks and video titles), you can set `Type` to `Text`.

<span id="a98ade82"></span>
#### Example: Erasing subtitles and other text

```JSON
{
    "Input": { ... },
    "Operation": {
        "Type": "Task",
        "Task": {
            "Type": "Erase",
            "Erase": {
                "Mode": "Auto",
                "Auto": {
                    "Type": "Text" // Change this parameter to Text.
                }
            }
        }
    }
}
```


<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46a65a1be1c4484bb8ff4254258daf7b~tplv-goo7wpa0wc-image.image" controls></video>


<span id="specifying-erasure-areas"></span>
### Specifying erasure areas

For more precise erasure control, you can define the scope of the operation by specifying one or more rectangular areas. Both Manual and Auto modes support specifying rectangular erasure areas, though their underlying logic differs.

<span id="79fb449e"></span>
#### Specifying the erasure area in manual mode

In Manual mode, the system directly erases all text within your specified areas that matches basic visual characteristics (such as white color) without performing OCR recognition. This mode is primarily recommended for the following scenarios:


* **Handling less common language subtitles**: When the OCR model in Auto mode does not support the specific language in the video, you can define a box around the subtitle area for erasure.

* **Avoiding accidental erasure**: When Auto mode might mistakenly erase non\-subtitle elements (such as in\-scene text), Manual mode allows you to precisely limit the scope of the operation.

* **Forced erasure**: If Auto mode fails to identify or remove certain text, you can use this mode to perform a forced removal.


<span id="5bb43d0f"></span>
##### Configurations


1. Set `Erase.Mode` to `Manual`.

2. Define one or more rectangular erasure areas in the `Erase.Manual.Locations` parameter.


You can define the location of each area by the coordinates of its top\-left and bottom\-right corners. All coordinate values are normalized ratios relative to the video's total width and height (ranging from 0.0 to 1.0).

For example, if you want to set the orange area in the figure below as the erasure area, configure the parameters as follows:


* `TopLeftX`: The X\-coordinate of the top\-left corner (b1 in the diagram).

* `TopLeftY`: The Y\-coordinate of the top\-left corner (a1 in the diagram).

* `BottomRightX`: The X\-coordinate of the bottom\-right corner (b2 in the diagram).

* `BottomRightY`: The Y\-coordinate of the bottom\-right corner (a2 in the diagram).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/166213c4d45145fcbae7c7b03aeb90d3~tplv-goo7wpa0wc-image.image) </span>

<span id="373c74ca"></span>
##### Example: Erasing all text in the specific area

The following example shows how to configure the API to erase all text in the area ranging from 60%\-85% of the video height, with a 10% horizontal margin on both sides.

```JSON
{
    "Input": {
        "Type": "Vid",
        "Vid": "your_video_id"
    },
    "Operation": {
        "Type": "Task",
        "Task": {
            "Type": "Erase",
            "Erase": {
                "Mode": "Manual",
                "Manual": {
                    "Locations": [
                        {
                            "RatioLocation":{
                                "TopLeftX":0.10,
                                "TopLeftY":0.60,
                                "BottomRightX":0.90,
                                "BottomRightY":0.85
                            }
                        }
                    ]
                },
                "WithEraseInfo": true,
                "NewVid":true
            }
        }
    }
}
```


<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bc990f1b11245a893e112da390d5f4e~tplv-goo7wpa0wc-image.image" controls></video>


<span id="specifying-the-erasure-area-in-auto-mode"></span>
#### Specifying the erasure area in Auto mode

In Auto mode, the system first erases all OCR\-recognized text. If you also specify an erasure area, the system restricts the erasure to only the OCR\-recognized text that falls within that area.

<span id="eb36be4e"></span>
##### Configurations


1. Set `Erase.Mode` to `Auto`.

2. Set `Erase.Auto.Type` to `Subtitle` (only subtitles) or `Text` (all text).

3. Define one or more rectangular erasure areas in the `Erase.Manual.Locations` parameter.


<span id="2f1387ef"></span>
##### Known issues

To achieve optimal erasure results, the specified area should encompass the entire text. Otherwise, parts of the text may not be erased, as shown below:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f60d7c3257844e0fbd0540d2da396372~tplv-goo7wpa0wc-image.image" width="273px" /></div>


<span id="6786d05c"></span>
##### Example: Erasing subtitles in the lower half of the screen

The following example demonstrates how to configure the API to erase all subtitles identified by OCR within the lower half of the video frame (Y\-coordinates 0.5–1.0).

```JSON
{
    "Input": {
        "Type": "Vid",
        "Vid": "your_video_vid"
    },
    "Operation": {
        "Type": "Task",
        "Task": {
            "Type": "Erase",
            "Erase": {
                "Mode": "Auto",
                "Auto": {
                    "Type": "Subtitle",
                    // Add Locations parameter to specify the erasure area in Auto mode
                    "Locations": [
                        {
                            "RatioLocation": {
                                "TopLeftX": 0.0,
                                "TopLeftY": 0.5,
                                "BottomRightX": 1.0,
                                "BottomRightY": 1.0
                            }
                        }
                    ]
                }
            }
        }
    }
}
```


<span id="b1474949"></span>
### Specifying time segments to erase/skip

In scenarios where subtitle erasure is only required for specific segments of a video (such as the main content) while preserving subtitles in others (such as opening or closing credits), the `EraseOption.ClipFilter` parameter can be used. This allows you to define one or more time segments and apply specific actions:


* `Selected`: Erase subtitles only within the defined segments.

* `Skip`: Exclude the defined segments and erase the remainder of the video.


<span id="3d69f57a"></span>
#### Example 1: Erasing subtitles within the 10s\-60s segment

```JSON
{
    "Input": { ... },
    "Operation": {
        "Type": "Task",
        "Task": {
            "Type": "Erase",
            "Erase": {
                "Mode": "Auto",
                "Auto": {
                    "Type": "Subtitle",
                    "SubtitleFilter":{}
                },
                "EraseOption": {
                    "ClipFilter": {
                        "Mode": "Selected",
                        "Clips": [
                            {
                                "Start": 10.0,
                                "End": 60.0
                            }
                        ]
                    }
                }
            }
        }
    }
}
```


<span id="e749cfb3"></span>
#### Example 2: Skipping the opening credits (the first 15 seconds)

```JSON
{
    "Input": { ... },
    "Operation": {
        "Type": "Task",
        "Task": {
            "Type": "Erase",
            "Erase": {
                "Mode": "Auto",
                "Auto": {
                    "Type": "Subtitle",
                    "SubtitleFilter":{}
                },
                "EraseOption": {
                    "ClipFilter": {
                        "Mode": "Skip",
                        "Clips": [
                            {
                                "Start": 0.0,
                                "End": 15.0
                            }
                        ]
                    }
                }
            }
        }
    }
}
```


<span id="42fa1054"></span>
## FAQ

<span id="0dc18799"></span>
### What should I do if non\-subtitle text is accidentally erased?

If `Auto` mode removes text that should be retained (such as in\-scene text), use the `Locations` feature:


* **Auto mode +**  `Locations`: (Recommended) The system only erases the subtitles recognized by the OCR in the specified area.

* **Manual mode +**  `Locations`: Use this if OCR fails to identify \*\*\*\* the text (such as unsupported languages). It forces erasure within the area regardless of OCR results.
