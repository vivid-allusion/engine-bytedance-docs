---
title: "Frame extraction"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-frame-extraction"
---

BytePlus VOD provides a frame extraction feature that allows you to extract frames from videos using flexible strategies, including time intervals, specified timestamps, specified frame numbers, and scene change detection. The extracted frames are persisted as media assets, enabling long\-term retrieval and cross\-run aggregation. This article covers the key features, use cases, and a step\-by\-step guide to completing frame extraction tasks.

<span id="edcba59d"></span>
## Key features


* **Multiple extraction strategies**: Supports time interval, specified time, specified frame number, and scene change extraction strategies to meet diverse business requirements.

* **Output resolution control**: Allows you to specify the long edge and short edge of the output images. The system automatically scales proportionally while preserving the original aspect ratio.

* **Sprite image generation**: Supports combining extracted frames into a single sprite image for efficient preview and storage.

* **Long\-term asset persistence**: Frame extraction results are stored as media assets. You can retrieve them across task runs using `ListFrameExtractions`, even after individual task results expire.

* **User tag grouping**: Each extraction task can carry a user\-defined tag (`UserTag`), which serves as a grouping key for organizing and filtering results across multiple runs on the same video.


<span id="caf5810c"></span>
## Use cases


* **Content moderation**: Extract key frames from videos and submit them to a content review system (such as TnS) for compliance checks, reducing the computational cost of reviewing full video content.

* **Cover image generation**: Extract the first frame, last frame, or frames at specific timestamps to generate video thumbnails and cover images.

* **AI training data preparation**: Batch\-extract frames from video libraries to create image datasets for training computer vision or multimodal AI models.

* **Video preview**: Generate sprite images from extracted frames to provide users with a quick visual overview of video content.

* **Scene change detection**: Automatically detect scene transitions in videos and extract key frames at each scene change point for editing or analysis.


<span id="73bd81f2"></span>
## Pricing

Using the frame extraction feature incurs a fee based on the number of extracted frames. For pricing details, refer to [Frame extraction pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#9625d442).

<span id="1abfbcab"></span>
## How it works

Frame extraction supports four core extraction types, each addressing a different way of selecting frames from a video. The following table maps each core type to its corresponding OpenAPI strategy (`Strategy.Type`) and key parameters.


|Frame extraction type |Description |Strategy (`Strategy.Type`) |Key parameters |
|---|---|---|---|
|Fixed time interval |Extracts frames at a fixed time interval from the start of the video, optionally capped by a maximum frame count. |`TimeInterval` |`Interval` (interval in milliseconds), `Limit` (max frames) |
|Fixed position |Extracts frames at specific positions within the video, defined as absolute timestamp offsets. |`SpecifiedTime` |`Times` (array of timestamp offsets in milliseconds) |
|Scene change |Extracts frames only when a scene change is detected above a configurable threshold. |`SceneChange` |`Threshold` (detection threshold, range `(0, 1)`), `Limit` (max frames) |
|First and last frame |Extracts the first frame, the last frame, or both. |`SpecifiedFrames` |`Frames` (frame numbers; only `0` for the first frame and `-1` for the last frame are supported) |


The following diagram illustrates the data flow of a frame extraction task:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/123e974f2cc44dd48c253399c07508cb) </span>

<span id="dc9793cd"></span>
## Prerequisites


* Create a [BytePlus account](https://console.byteplus.com/auth/signup/) and sign in to the BytePlus console.

* Enable the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started) and create a space.

* [Upload video files](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to the target space and obtain the Vid or FileName.


<span id="2de82d56"></span>
## Procedure

You can initiate and manage frame extraction tasks programmatically via the BytePlus VOD OpenAPI.

<span id="4c3e0bef"></span>
### Step 1: Submit a frame extraction task

Call the [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-frame-extraction) API to submit a frame extraction task. Set `Operation.Type` to `Task` and `Task.Type` to `Snapshot`, then configure the extraction strategy and target parameters.

<span id="2f37f6ff"></span>
#### **Example 1: Extract frames at a fixed time interval**

```JSON
{
  "Input": {
    "Type": "Vid",
    "Vid": "v0d25cg10001c****vqljht8dj05mde0"
  },
  "Operation": {
    "Type": "Task",
    "Task": {
      "Type": "Snapshot",
      "Snapshot": {
        "Strategy": {
          "Type": "TimeInterval",
          "TimeInterval": {
            "Interval": 1000,
            "Limit": 10
          }
        },
        "Target": {
          "ScaleLong": 1280,
          "ScaleShort": 720
        },
        "Mode": "Files"
      }
    }
  }
}
```


<span id="c5f87b1d"></span>
#### **Example 2: Extract frames at specified timestamps**

```JSON
{
  "Input": {
    "Type": "Vid",
    "Vid": "v0d25cg10001c****vqljht8dj05mde0"
  },
  "Operation": {
    "Type": "Task",
    "Task": {
      "Type": "Snapshot",
      "Snapshot": {
        "Strategy": {
          "Type": "SpecifiedTime",
          "SpecifiedTime": {
            "Times": [0, 5000, 10000]
          }
        },
        "Target": {
          "ScaleLong": 1920
        },
        "Mode": "Files"
      }
    }
  }
}
```


<span id="5a6736bd"></span>
#### **Example 3: Extract the first and last frames**

```JSON
{
  "Input": {
    "Type": "Vid",
    "Vid": "v0d25cg10001c****vqljht8dj05mde0"
  },
  "Operation": {
    "Type": "Task",
    "Task": {
      "Type": "Snapshot",
      "Snapshot": {
        "Strategy": {
          "Type": "SpecifiedFrames",
          "SpecifiedFrames": {
            "Frames": [0, -1]
          }
        },
        "Target": {
          "ScaleLong": 1280
        },
        "Mode": "Files"
      }
    }
  }
}
```


<span id="b60a4c00"></span>
#### **Example 4: Extract frames on scene change**

```JSON
{
  "Input": {
    "Type": "Vid",
    "Vid": "v0d25cg10001c****vqljht8dj05mde0"
  },
  "Operation": {
    "Type": "Task",
    "Task": {
      "Type": "Snapshot",
      "Snapshot": {
        "Strategy": {
          "Type": "SceneChange",
          "SceneChange": {
            "Threshold": 0.1,
            "Limit": 50
          }
        },
        "Target": {
          "ScaleLong": 1280
        },
        "Mode": "Files"
      }
    }
  }
}
```


<span id="1026743c"></span>
#### **Example 5: Generate sprite images**

```JSON
{
  "Input": {
    "Type": "Vid",
    "Vid": "v0d25cg10001c****vqljht8dj05mde0"
  },
  "Operation": {
    "Type": "Task",
    "Task": {
      "Type": "Snapshot",
      "Snapshot": {
        "Strategy": {
          "Type": "TimeInterval",
          "TimeInterval": {
            "Interval": 5000,
            "Limit": 100
          }
        },
        "Target": {
          "ScaleLong": 1280,
          "SpriteConfig": {
            "Enable": true,
            "ImgXLen": 10,
            "ImgYLen": 10
          }
        },
        "Mode": "Files"
      }
    }
  }
}
```


<span id="e0ec9e90"></span>
### Step 2: Retrieve task results

You can retrieve frame extraction results through two approaches depending on your use case:


|Approach |API |Scope |Retention |
|---|---|---|---|
|Task\-level |[GetExecution](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getexecution) |Results from a single task run (by `RunId`) |30 days |
|Asset\-level |[ListFrameExtractions](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listframeextractions?lang=en) |All extraction results for a video (by `Vid`), aggregated across runs |Long\-term |


<span id="e6a156c9"></span>
#### Get task results by RunId

Call the `GetExecution` API with the `RunId` returned by `StartExecution` to check the task status and retrieve the extraction results for that specific run.

```JSON
{
  "RunId": "hb:ebd05bee****"
}
```


The response includes the task status and the extraction output under `Output.Task.Snapshot`:

```JSON
{
  "Output": {
    "Type": "Task",
    "Task": {
      "Type": "Snapshot",
      "Snapshot": {
        "Number": 10,
        "Mode": "Files",
        "Files": [
          {
            "Size": "2519064",
            "FileName": "9301da082a0a4003b76bd217cbc8e2ee"
          }
        ]
      }
    }
  }
}
```


<span id="6e731619"></span>
#### Query frame extraction results by Vid

Call the `ListFrameExtractions` API with the `Vid` to retrieve all frame extraction results persisted as media assets, aggregated across multiple runs and grouped by `UserTag`.

```JSON
{
  "Action": "ListFrameExtractions",
  "Version": "2023-01-01",
  "SpaceName": "test",
  "Vid": "v0dc24g10***s1v0ipljnh4h0"
}
```


The response includes frame extraction snapshots grouped by `UserTag`:

```JSON
{
    "ResponseMetadata": {
        "Action": "ListFrameExtractions",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Vid": "v0dc24g10001cm***pljnh4h0",
        "SpaceName": "test",
        "FrameExtractionSnapshots": [
            {
                "RunId": "3732f0bd7565494d8faf7956d4f99f31",
                "Width": 1920,
                "Format": "jpeg",
                "Height": 1080,
                "UserTag": "tag1",
                "Duration": 600,
                "UserData": "test",
                "Snapshots": [
                    {
                        "Url": "https://console-image-my.byteplusvod.com/tos-vod-bp-mya-v-xxx/01snapshot.jpg",
                        "Size": 251906,
                        "FrameNo": 5,
                        "StoreURI": "tos-vod-bp-mya-v-xxx/01snapshot.jpg",
                        "StartTime": 5000,
                        "SceneChangeRate": 0.85
                    }
                ]
            }
        ]
    }
}
```


You can filter results by `UserTag` or `RunId`:

```JSON
{
  "Action": "ListFrameExtractions",
  "Version": "2023-01-01",
  "SpaceName": "test",
  "Vid": "v0dc24g10***s1v0ipljnh4h0",
  "UserTag": "review_v1",
  "RunId": "3732f0bd7565494d8faf7956d4f99f31"
}
```


<span id="delete-frame-extraction-results"></span>
### Step 3: Delete frame extraction results

Call the [DeleteFrameExtractions](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteframeextractions) action to delete persisted frame extraction results while retaining the source video. The request must include `SpaceName` and `Vid`. You can also specify `UserTag`, `RunId`, or both to narrow the deletion scope.

Only one `UserTag` and one `RunId` can be specified in each request. If an optional filter is omitted, the deletion is not filtered by that field.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This action deletes both the matching result records and their stored extracted\-frame files. Verify the <code>Vid</code>, <code>UserTag</code>, and <code>RunId</code> before sending the request.</div>


The following example deletes results that match both the specified `UserTag` and `RunId`:

```JSON
{
  "Action": "DeleteFrameExtractions",
  "Version": "2023-01-01",
  "SpaceName": "test",
  "Vid": "v0dc24g10***s1v0ipljnh4h0",
  "UserTag": "review_v1",
  "RunId": "3732f0bd7565494d8faf7956d4f99f31"
}
```


The response contains only the common response metadata:

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202606111230406131E13B603A9C364A09",
    "Action": "DeleteFrameExtractions",
    "Version": "2023-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  }
}
```


<span id="2eb9e920"></span>
## API reference


|API |Description |
|---|---|
|[StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-frame-extraction) |Submits a frame extraction task. |
|[GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution) |Queries the status and results of a frame extraction task by RunId. |
|[ListFrameExtractions](https://docs.byteplus.com/docs/byteplus-vod/reference-listframeextractions) |Queries frame extraction results by Vid, aggregated across runs and grouped by UserTag. |
|[DeleteFrameExtractions](https://docs.byteplus.com/docs/byteplus-vod/reference-deleteframeextractions) |Deletes some or all persisted frame extraction results while retaining the source video. |
