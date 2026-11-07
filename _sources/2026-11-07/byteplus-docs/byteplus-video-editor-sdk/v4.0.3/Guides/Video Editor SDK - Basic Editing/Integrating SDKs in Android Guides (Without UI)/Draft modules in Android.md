---
title: "Draft modules in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-draft-modules-in-android"
---

A draft is essentially a JSON string that encapsulates comprehensive information about the entire NLEModel. This JSON representation serves as a structured and complete snapshot of your project's configuration and content.


|**Process** |**Steps** |
|---|---|
|Saving a Draft |1. Call `editor.store()` to obtain the draft information in String format.<br><br>2. Write this draft information into a specific file for later retrieval. |
|Restoring a Draft |1. Retrieve the saved draft information in String format.<br><br>2. Call `editor.restore()` while providing the draft information as an input parameter.<br><br>3. The function will execute, and you will receive the result after restoration is completed. |


<span id="c6b053df"></span>
# Module description

These are some module descriptions in the Draft module.


|**Module** |**Description** |
|---|---|
|NLEMediaSessionPublic |An API for NLE editing |
|NLEEditor |An external common API for NLE |


<span id="5ee7c930"></span>
# Saving drafts

```Kotlin
private val draftPath = AppSingleton.instance.filesDir
private const val draftName = "SimpleEditor-draft.txt"

fun store(nleEditor: NLEEditor): Boolean {
    // Save all data model operations of NLEModel. This prevents data from not being saved after the commit operation is performed to cache data, thus avoiding potential loss of obtained data.
    nleEditor.done()
    // Obtain draft data (String in JSON format).
    val draftString = nleEditor.store()
    if (draftString.isNullOrEmpty()) {
        Log.e("DraftrHelper", "saveDraft failed draftString isNullOrEmpty")
        return false
    }
    // Save draft data to a file. The data of multiple drafts can be written into different files or the same file with custom tags for distinguishing.
    // Obtain and restore a draft. That is, save and restore a string in JSON format.
    return writeToFile(draftString)
}

private fun writeToFile(draftString: String): Boolean {
    try {
        val draftFile = File(draftPath, draftName)
        if (!draftFile.exists()) {
            draftFile.createNewFile()
        } else {
            draftFile.writeText("")
        }

        val fileWriter = FileWriter(draftFile, true)
        fileWriter.write(draftString)
        fileWriter.close()
        return  true
    } catch (e: Exception) {
        e.printStackTrace()
        return false
    }
}
```


<span id="067bb3cf"></span>
# Restoring drafts

```Kotlin
fun restore(nleEditor: NLEEditor, nleMediaSession: NLEMediaSessionPublic): Boolean {
    // Read the saved draft string from a local file or a custom draft storage location.
    val draftString = readFromFile()
    if (draftString.isEmpty()) {
        Log.e("DraftrHelper", "restoreDraft failed draftString isEmpty")
        return false
    }
    // Restore the draft.
    val state = nleEditor.restore(draftString)
    when (state) {
        NLEError.SUCCESS -> {
            // After the draft is restored, reset the player and seek to the beginning of the video, which is 0 second.
            nleMediaSession.playerApi.prepare()
            nleMediaSession.playerApi.seekTime(0, NLESeekFlag.EDITOR_SEEK_FLAG_LastSeek)
            return true
        }
        else -> {
            Log.e("DraftrHelper", "draft restore failed:$state")
            return false
        }
    }
}

private fun readFromFile(): String {
    val draftFile = File(draftPath, draftName)
    if (!draftFile.exists()) {
        return ""
    }
    return draftFile.readText()
}
```


<span id="f93c9837"></span>
# Comparing between NLEModel and Drafts

The provided code snippets represent two different JSON structures, both describing an NLEModel. The first structure includes various object entries with detailed information about resources, tracks, segments, and more. In contrast, the second structure simplifies this information, representing the NLEModel as a set of tracks, each with associated segments and properties.

These representations serve the same purpose but differ in their level of detail and organization. The first structure offers a more comprehensive view of the NLEModel's components, while the second provides a more condensed version. Both structures are valid ways to describe an NLEModel, and the choice between them depends on the specific use case and the need for detailed resource information.

<span id="f7646f92"></span>
## NLEModel

```JSON
{
  "CanvasRatio": 1,
  "Name": "12970367396170357096",
  "Track": {
    "000000000000000": {
      "MainTrack": true,
      "Name": "12970367396170360816",
      "Slot": [
        {
          "EndTime": 3042000,
          "MainSegment": {
            "AVFile": {
              "Duration": 3042000,
              "Height": 720,
              "Name": "12970367395902108464",
              "ResourceFile": "content://media/external_primary/video/media/1000015062",
              "ResourceType": 2,
              "UUID": "169509253076444012970367395902108464",
              "Width": 720,
              "_class": "NLEResourceAV"
            },
            "KeepTone": true,
            "Name": "12970367395902105328",
            "TimeClipEnd": 3042000,
            "TimeClipStart": 0,
            "UUID": "169509253076399112970367395902105328",
            "_class": "NLESegmentVideo"
          },
          "Name": "12970367396170355056",
          "StartTime": 0,
          "UUID": "169509253076324912970367396170355056",
          "_class": "NLETrackSlot"
        }
      ],
      "UUID": "169509253074958212970367396170360816",
      "_class": "NLETrack",
      "_trackType": "2"
    },
    "000000000000001": {
      "MainTrack": false,
      "Name": "12970367396170288240",
      "Slot": [
        {
          "EndTime": 3000000,
          "MainSegment": {
            "Animation": {
              "Loop": false,
              "Name": "12970367395902179920",
              "OutAnim": {
                "Name": "12970367395902169392",
                "ResourceFile": "/storage/emulated/0/Android/data/com.volcengine.ck.sample/files/assets/resource/text_animation.bundle/zhuzixuying_7074738958005993485/zhuzixuying_7074738958005993485",
                "ResourceType": 27,
                "UUID": "169509253349480112970367395902169392",
                "_class": "NLEResourceNode"
              },
              "OutDuration": 1000000,
              "UUID": "169509253349469912970367395902179920",
              "_class": "NLEStyStickerAnim"
            },
            "Content": "Add text",
            "Name": "12970367395902180144",
            "Style": {
              "Background": true,
              "BackgroundColor": 4294309340,
              "Font": {
                "Name": "12970367395902057840",
                "ResourceFile": "/storage/emulated/0/Android/data/com.volcengine.ck.sample/files/assets/resource/NotoSansSC-Regular.otf",
                "ResourceType": 10,
                "UUID": "169509253349433212970367395902057840",
                "_class": "NLEResourceNode"
              },
              "FontSize": 14,
              "Name": "12970367395902078448",
              "Shape": {
                "Name": "12970367395902175664",
                "ResourceFile": "/storage/emulated/0/Android/data/com.volcengine.ck.sample/files/assets/resource/bubble.bundle/zhuangshibeijing50_6945244052808384525/zhuangshibeijing50_6945244052808384525",
                "ResourceType": 33,
                "UUID": "169509253349441112970367395902175664",
                "_class": "NLEResourceNode"
              },
              "TextColor": 4287688336,
              "UUID": "169509253349404612970367395902078448",
              "_class": "NLEStyText"
            },
            "UUID": "169509253349327012970367395902180144",
            "_class": "NLESegmentTextSticker"
          },
          "Name": "12970367396170461904",
          "StartTime": 0,
          "TransformX": 0,
          "TransformY": 0,
          "TransformZ": 1,
          "UUID": "169509253349284912970367396170461904",
          "_class": "NLETrackSlot"
        }
      ],
      "TransformZ": 1,
      "UUID": "169509253349254712970367396170288240",
      "_class": "NLETrack",
      "_trackType": "3"
    },
    "Name": "Track",
    "UUID": "NLENodeGroup_Track",
    "_class": "NLENodeGroup"
  },
  "UUID": "169509253074190712970367396170357096",
  "_class": "NLEModel"
}
```


<span id="1b139a07"></span>
## Drafts

```JSON
{
  "_author": "NLE",
  "_branch": "17",
  "_features": [
    "E"
  ],
  "_objects": {
    "1": {
      "Duration": 3042000,
      "Height": 720,
      "Name": "12970367395902108464",
      "ResourceFile": "content://media/external_primary/video/media/1000015062",
      "ResourceType": 2,
      "UUID": "169509253076444012970367395902108464",
      "Width": 720,
      "_class": "NLEResourceAV",
      "_features": [
        "E"
      ]
    },
    "2": {
      "KeepTone": true,
      "Name": "12970367395902105328",
      "TimeClipEnd": 3042000,
      "TimeClipStart": 0,
      "UUID": "169509253076399112970367395902105328",
      "_class": "NLESegmentVideo",
      "_features": [
        "E"
      ],
      "_objects": {
        "AVFile": "1"
      }
    },
    "3": {
      "EndTime": 3042000,
      "Name": "12970367396170355056",
      "StartTime": 0,
      "UUID": "169509253076324912970367396170355056",
      "_class": "NLETrackSlot",
      "_features": [
        "E"
      ],
      "_objects": {
        "MainSegment": "2"
      }
    },
    "4": {
      "MainTrack": true,
      "Name": "12970367396170360816",
      "UUID": "169509253074958212970367396170360816",
      "_arrays": {
        "Slot": [
          "3"
        ]
      },
      "_class": "NLETrack",
      "_extras": {
        "_trackType": "2"
      },
      "_features": [
        "E"
      ],
      "_objects": {}
    },
    "5": {
      "Name": "12970367395902169392",
      "ResourceFile": "/storage/emulated/0/Android/data/com.volcengine.ck.sample/files/assets/resource/text_animation.bundle/zhuzixuying_7074738958005993485/zhuzixuying_7074738958005993485",
      "ResourceType": 27,
      "UUID": "169509253349480112970367395902169392",
      "_class": "NLEResourceNode",
      "_features": [
        "E"
      ]
    },
    "6": {
      "Loop": false,
      "Name": "12970367395902179920",
      "OutDuration": 1000000,
      "UUID": "169509253349469912970367395902179920",
      "_class": "NLEStyStickerAnim",
      "_features": [
        "E"
      ],
      "_objects": {
        "OutAnim": "5"
      }
    },
    "7": {
      "Name": "12970367395902057840",
      "ResourceFile": "/storage/emulated/0/Android/data/com.volcengine.ck.sample/files/assets/resource/NotoSansSC-Regular.otf",
      "ResourceType": 10,
      "UUID": "169509253349433212970367395902057840",
      "_class": "NLEResourceNode",
      "_features": [
        "E"
      ]
    },
    "8": {
      "Name": "12970367395902175664",
      "ResourceFile": "/storage/emulated/0/Android/data/com.volcengine.ck.sample/files/assets/resource/bubble.bundle/zhuangshibeijing50_6945244052808384525/zhuangshibeijing50_6945244052808384525",
      "ResourceType": 33,
      "UUID": "169509253349441112970367395902175664",
      "_class": "NLEResourceNode",
      "_features": [
        "E"
      ]
    },
    "9": {
      "Background": true,
      "BackgroundColor": 4294309340,
      "FontSize": 14,
      "Name": "12970367395902078448",
      "TextColor": 4287688336,
      "UUID": "169509253349404612970367395902078448",
      "_class": "NLEStyText",
      "_features": [
        "E"
      ],
      "_objects": {
        "Font": "7",
        "Shape": "8"
      }
    },
    "10": {
      "Content": "Add text",
      "Name": "12970367395902180144",
      "UUID": "169509253349327012970367395902180144",
      "_class": "NLESegmentTextSticker",
      "_features": [
        "E"
      ],
      "_objects": {
        "Animation": "6",
        "Style": "9"
      }
    },
    "11": {
      "EndTime": 3000000,
      "Name": "12970367396170461904",
      "StartTime": 0,
      "TransformX": 0,
      "TransformY": 0,
      "TransformZ": 1,
      "UUID": "169509253349284912970367396170461904",
      "_class": "NLETrackSlot",
      "_features": [
        "E"
      ],
      "_objects": {
        "MainSegment": "10"
      }
    },
    "12": {
      "MainTrack": false,
      "Name": "12970367396170288240",
      "TransformZ": 1,
      "UUID": "169509253349254712970367396170288240",
      "_arrays": {
        "Slot": [
          "11"
        ]
      },
      "_class": "NLETrack",
      "_extras": {
        "_trackType": "3"
      },
      "_features": [
        "E"
      ],
      "_objects": {}
    },
    "13": {
      "CanvasRatio": 1,
      "Name": "12970367396170357096",
      "UUID": "169509253074190712970367396170357096",
      "_arrays": {
        "Track": [
          "4",
          "12"
        ]
      },
      "_class": "NLEModel",
      "_features": [
        "E"
      ],
      "_objects": {}
    },
    "14": {
      "Name": "12970367396170296040",
      "UUID": "169509253956111912970367396170296040",
      "Version": 2,
      "_class": "NLECommit",
      "_features": [
        "E"
      ],
      "_objects": {
        "Model": "13"
      }
    },
    "15": {
      "CanvasRatio": 1,
      "Name": "12970367396170357096",
      "UUID": "169509253074190712970367396170357096",
      "_arrays": {
        "Track": [
          "4"
        ]
      },
      "_class": "NLEModel",
      "_features": [
        "E"
      ],
      "_objects": {}
    },
    "16": {
      "Name": "12970367396170377544",
      "UUID": "169509253080988512970367396170377544",
      "Version": 1,
      "_class": "NLECommit",
      "_features": [
        "E"
      ],
      "_objects": {
        "Model": "15"
      }
    },
    "17": {
      "commits": [
        "14",
        "16"
      ],
      "head": 0
    }
  }
}
```
