---
title: "Draft module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-draft-module-in-ios"
---

A draft is essentially a JSON string that encapsulates comprehensive information about the entire NLEModel. This JSON representation serves as a structured and complete snapshot of your project's configuration and content.

<span id="49c2dd45"></span>
# Module description

The following table introduces data classes related to the draft module.


|**Class Name** |**Description** |
|---|---|
|NLEInterface_OC |The universal interface for NLE. |
|NLEEditor_OC |The interface used to provide editing capability for NLE. |


<span id="3ea8e0aa"></span>
# Primary functions

The following section provides a step\-by\-step guide on how to use the primary functions in draft module.

<span id="f5c99c81"></span>
## Saving a draft

This section introduces how to save a draft.

**To save a draft**:


1. To return draft content, call `nle.editor.store()`.

2. Write the draft content to a specific document.

3. If you need to write a relative path in the draft, set `nle.draftFolder`. NLE can use the relative path to produce the complete path of all resources.


```Swift
public func store(to path: String) -> Bool {
    let jsonStr = nle.editor.store()
    guard !jsonStr.isEmpty,
          let data = jsonStr.data(using: .utf8) else {
        return false
    }
    
    let draftDir = URL(fileURLWithPath: path).deletingPathExtension().deletingLastPathComponent()
    _create(dir: draftDir)
    
    do {
        try data.write(to: URL(fileURLWithPath: path))
        return true
    } catch {
        print(error)
    }
    return false
}

func _create(dir: URL) {
    do {
        try FileManager.default.createDirectory(atPath: dir.path, withIntermediateDirectories: true)
    } catch {
        print(error)
    }
}
```


<span id="d7b77b53"></span>
## Restoring a draft

Before restoring a draft, ensure that you have obtained the draft content, which is a JSON string. Then, you can proceed to restore the draft content by calling `nle.editor.restore()`. An operation result will be returned by your requested function.

```Swift
public func restore(with path: String) -> Bool {
    do {
        let url = URL(fileURLWithPath: path)
        let d = try Data(contentsOf: url)
        guard let str = String(data: d, encoding: .utf8) else {
            return false
        }
        return nle.editor.restore(str) == .SUCCESS
    } catch {
        print(error)
    }
    return false
}
```


<span id="4298f8d0"></span>
# Comparing between NLEModel and draft module

The provided code snippets represent two different JSON structures, both describing an NLEModel. The first structure includes various object entries with detailed information about resources, tracks, segments, and more. In contrast, the second structure simplifies this information, representing the NLEModel as a set of tracks, each with associated segments and properties.

These representations serve the same purpose but differ in their level of detail and organization. The first structure offers a more comprehensive view of the NLEModel's components, while the second provides a more condensed version. Both structures are valid ways to describe an NLEModel, and the choice between them depends on the specific use case and the need for detailed resource information.

<span id="90d35327"></span>
## NLEModel

```JSON
{
  "Track" : {
    "000000000000000" : {
      "_class" : "NLETrack",
      "RelativeHeight" : 0.60126203298568726,
      "Slot" : [
        {
          "TransformZ" : 0,
          "Name" : "10768487448",
          "StartTime" : 0,
          "UUID" : "169450704953528010768487448",
          "_class" : "NLETrackSlot",
          "MainSegment" : {
            "AVFile" : {
              "ResourceType" : 2,
              "Duration" : 13100000,
              "HasAudio" : true,
              "_class" : "NLEResourceAV",
              "UUID" : "169450704952229210769580056",
              "Name" : "10769580056",
              "ResourceFile" : "file:\/\/\/var\/containers\/Bundle\/Application\/20B59373-99D6-4A71-92C1-D12BA2E298F3\/SimpleEditor.app\/CKResource-SimpleEditor.bundle\/video1.mp4"
            },
            "TimeClipEnd" : 13100000,
            "Volume" : 1,
            "_class" : "NLESegmentVideo",
            "UUID" : "169450704953460810769655192",
            "Name" : "10769655192",
            "TimeClipStart" : 0
          }
        }
      ],
      "MainTrack" : true,
      "TransformZ" : 0,
      "UUID" : "169450704953424410768486936",
      "Name" : "10768486936",
      "RelativeWidth" : 1,
      "_trackType" : "2"
    },
    "Name" : "Track",
    "UUID" : "NLENodeGroup_Track",
    "_class" : "NLENodeGroup"
  },
  "Name" : "10768484632",
  "UUID" : "169450704786599610768484632",
  "CanvasRatio" : 1.0689102411270142,
  "_class" : "NLEModel"
}
```


<span id="73a81817"></span>
## Draft module

```JSON
{
  "_author" : "NLE",
  "_branch" : "11",
  "_objects" : {
    "7" : {
      "Version" : 4,
      "Name" : "10779338136",
      "UUID" : "169459038056357110779338136",
      "_class" : "NLECommit",
      "_features" : [
        "E"
      ],
      "_objects" : {
        "Model" : "5"
      }
    },
    "3" : {
      "_class" : "NLETrackSlot",
      "StartTime" : 0,
      "TransformZ" : 0,
      "UUID" : "169450704953528010768487448",
      "Name" : "10768487448",
      "_features" : [
        "E"
      ],
      "_objects" : {
        "MainSegment" : "2"
      }
    },
    "11" : {
      "commits" : [
        "6",
        "7",
        "8",
        "9",
        "10"
      ],
      "head" : 0
    },
    "4" : {
      "_arrays" : {
        "Slot" : [
          "3"
        ]
      },
      "_class" : "NLETrack",
      "RelativeHeight" : 0.60126203298568726,
      "_extras" : {
        "_trackType" : "2"
      },
      "TransformZ" : 0,
      "MainTrack" : true,
      "UUID" : "169450704953424410768486936",
      "Name" : "10768486936",
      "RelativeWidth" : 1,
      "_features" : [
        "E"
      ],
      "_objects" : {

      }
    },
    "8" : {
      "Version" : 3,
      "Name" : "10769580536",
      "UUID" : "169450709335172810769580536",
      "_class" : "NLECommit",
      "_features" : [
        "E"
      ],
      "_objects" : {
        "Model" : "5"
      }
    },
    "9" : {
      "Version" : 2,
      "Name" : "10769530904",
      "UUID" : "169450709167738910769530904",
      "_class" : "NLECommit",
      "_features" : [
        "E"
      ],
      "_objects" : {
        "Model" : "5"
      }
    },
    "5" : {
      "_arrays" : {
        "Track" : [
          "4"
        ]
      },
      "_class" : "NLEModel",
      "CanvasRatio" : 1.0689102411270142,
      "UUID" : "169450704786599610768484632",
      "Name" : "10768484632",
      "_features" : [
        "E"
      ],
      "_objects" : {

      }
    },
    "1" : {
      "ResourceType" : 2,
      "Duration" : 13100000,
      "HasAudio" : true,
      "_class" : "NLEResourceAV",
      "UUID" : "169450704952229210769580056",
      "Name" : "10769580056",
      "_features" : [
        "E"
      ],
      "ResourceFile" : "file:\/\/\/var\/containers\/Bundle\/Application\/20B59373-99D6-4A71-92C1-D12BA2E298F3\/SimpleEditor.app\/CKResource-SimpleEditor.bundle\/video1.mp4"
    },
    "6" : {
      "Version" : 5,
      "Name" : "10779296008",
      "UUID" : "169459038132217810779296008",
      "_class" : "NLECommit",
      "_features" : [
        "E"
      ],
      "_objects" : {
        "Model" : "5"
      }
    },
    "10" : {
      "Version" : 1,
      "Name" : "10769637848",
      "UUID" : "169450704961066710769637848",
      "_class" : "NLECommit",
      "_features" : [
        "E"
      ],
      "_objects" : {
        "Model" : "5"
      }
    },
    "2" : {
      "Volume" : 1,
      "TimeClipEnd" : 13100000,
      "_class" : "NLESegmentVideo",
      "_objects" : {
        "AVFile" : "1"
      },
      "UUID" : "169450704953460810769655192",
      "Name" : "10769655192",
      "_features" : [
        "E"
      ],
      "TimeClipStart" : 0
    }
  },
  "_features" : [
    "E"
  ]
}
```
