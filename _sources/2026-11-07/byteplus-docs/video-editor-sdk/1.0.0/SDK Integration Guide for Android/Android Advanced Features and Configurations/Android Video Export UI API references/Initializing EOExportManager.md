---
title: "Initializing EOExportManager"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-initializing-EOExportManager"
---

This topic introduces how to initialize BytePlus Video Editor SDK's video export function, `EOExportManager` in your Android project.

<span id="3ead818e"></span>
# Prerequisites

You have integrated the SDK into your project by following the instructions provided in the [Getting started with Android](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-android) topic.

<span id="31ebd5a5"></span>
# Initializing EOExportManager

Use the following code to initialize the EOExportManager:

```Kotlin
fun init(
    activity: ComponentActivity,
    surfaceView: SurfaceView? = null,
    previewSurfaceImage: Bitmap? = null,
    eoExportInitConfig: EOExportInitConfig = EOExportInitConfig(),
    callback: (suc: Boolean) -> Unit,
): EOExportManager
```


**Parameters**

The following table contains a detailed description for each parameter required for initialization:


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|activity |ComponentActivity |N/A |Yes |It requires reference to a`ComponentActivity`, specifying the context for the manager. It is essential for managing the lifecycle of the component. |
|surfaceView |SurfaceView |null |No |Used for video preview during editing. This is optional in scenarios where video preview is not required. |
|previewSurfaceImage |Bitmap |null |No |Sets the preview frame, which is mainly used for first frame optimization. Set to `null` if not needed. |
|eoExportInitConfig |EOExportInitConfig |EOExportInitConfig() |No |```Kotlin```<br>```/**```<br>``` * Export function initializati9on configuration，```<br>``` * @property previewCompileFinishPage Preview and export functions, finish the page after the export is completed, SurfaceView cannot be empty```<br>``` * @property autoReleaseCompileDone Whether to automatically release memory after exporting is completed```<br>``` */```<br>```data class EOExportInitConfig(```<br>```var previewCompileFinishPage :Boolean = false,```<br>```var autoReleaseCompileDone :Boolean = true```<br>```)```<br> |


<span id="1cc8ef2c"></span>
# Response parameters


|**Parameter** |**Description** |
|---|---|
|EOExportManager |Editing examples, all edit\-related interfaces are in this Manager |


<span id="a936a71e"></span>
# Sample response code

This is the sample response code after initializing `EOExportManager`:

```Kotlin
private lateinit var eoExportManager:EOExportManager

override fun onViewCreated(
    view: View,
    savedInstanceState: Bundle?,
) {
    super.onViewCreated(view, savedInstanceState)
    // Step 1: Initialize EOExportManager
    eoExportManager.init(requireActivity(), view.findViewById<SurfaceView>(R.id.export_cover_preview)) { suc ->
        if (!suc) {
            requireActivity().finish()
        }
    }
}
```
