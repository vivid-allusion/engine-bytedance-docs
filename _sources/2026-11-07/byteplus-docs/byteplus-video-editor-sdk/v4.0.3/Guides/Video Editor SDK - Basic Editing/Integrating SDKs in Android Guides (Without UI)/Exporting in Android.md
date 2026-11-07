---
title: "Exporting in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-exporting-in-android"
---

This module is for the process of saving the edited video to a video file in the app's sandbox.

<span id="67543381"></span>
# Procedure

These are the steps for using the export module:


1. Create a new `NLEMediaSessionPublic` using `NLEModel`.

   ```Kotlin
   val compileNLESession = NLEMediaSessionPublic.create(NLEMediaConfig(), null, NLEEditor())
   compileNLESession.dataSource = nleEditor.model
   ```
   

2. Define the path for the exported file: `outFilePath`.

   ```Kotlin
   val outFilePath = "/mnt/sdcard/exported_video.mp4"
   ```
   

3. Define the composition settings: `compileSettings`.

   ```Kotlin
   val compileSettings = NLEVideoEncodeSettings().apply {
       fps = 30
       outputSize = Pair(1920, 1080) // Output size is 1920x1080 pixels
       resizeMode = 1 // Add black bars if the aspect ratio doesn't match
       enableUploadingWhileCompile = false
       isSupportHWEncoder = true
       // Set other settings as needed
   }
   ```
   

4. Call the export interface to perform the export.

   ```Kotlin
   fun export() {
       val outFilePath = "/mnt/sdcard/exported_video.mp4"
       val curFps = 30
       val supportHWEncoder = true
   
       val compileSettings = NLEVideoEncodeSettings().apply {
           fps = curFps
           outputSize = Pair(1920, 1080)
           resizeMode = 1
           enableUploadingWhileCompile = false
           isSupportHWEncoder = supportHWEncoder
           // Set other settings as needed
       }
       
       compileDialog.show()
       compileNLESession.exporterApi.compile(outFilePath, compileSettings, object : INLEListenerCompile {
           override fun onCompileError(p0: Int, p1: Int, p2: Float, p3: String?) {
               // Handle error
           }
   
           override fun onCompileDone() {
               // Handle successful completion
           }
   
           override fun onCompileProgress(p0: Float) {
               // Update progress
           }
       })
   }
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to create a new NLEMediaSessionPublic object for the composition. Separate NLEMediaSessionPublic instances are advised for video editing and video composition to avoid affecting video editing operations when working with the composition.</div>


<span id="a3b948c3"></span>
# Full sample code

This is the full sample code for exporting in Android:

```Kotlin
private val compileNLESession by lazy {
    NLEMediaSessionPublic.create(NLEMediaConfig(), null, NLEEditor()).apply {
        dataSource = nleEditor.model
    }
}

fun export() {
    val outFilePath = getExportVideoPath()
    val curFps = 30
    val supportHWEncoder = true

    val compileSettings = NLEVideoEncodeSettings().apply {
        // Video composition frames per second
        fps = curFps
        // Output size of the composed video
        outputSize = calculateOutputSize()
        // Video aspect ratio adjustment mode: 1 for adding black bars, 2 for cropping
        resizeMode = 1
        // Keep this setting fixed at 'false'
        enableUploadingWhileCompile = false
        // Hardware encoding support
        isSupportHWEncoder = supportHWEncoder
        mVideoCompileEncodeSetting.useHWEncoder = supportHWEncoder
        mVideoCompileEncodeSetting.isSupportHWEncoder = supportHWEncoder

        // Set bitrate
        bps = DEFAULT_BPS
        // Maximum bitrate for software encoding
        swMaxrate = DEFAULT_SW_MAX_RATE
        // Set software encoding CRF (Constant Rate Factor) value; smaller values result in larger files and higher quality
        swCRF = DEFAULT_SW_CRF
        // Set GopSize
        gopSize = DEFAULT_GOP_SIZE

        swQPOffset = DEFAULT_SW_QP_OFFSET
        /**
         * Set video bitrate control mode. Depending on the bitrate control mode, different fields will work together. For example:
         * <ul>
         * <li>1. builder.setVideoBitrateMode(ENCODE_BITRATE_MODE.ENCODE_BITRATE_ABR).setBps(4096000) Supports software and hardware encoding.</li>
         * <li>2. builder.setVideoBitrateMode(ENCODE_BITRATE_MODE.ENCODE_BITRATE_CRF).setSWCRF(15).setHWEnc(false) Supports software encoding only, recommended.</li>
         * <li>3. builder.setVideoBitrateMode(ENCODE_BITRATE_MODE.ENCODE_BITRATE_QP).setQP(15).setHWEnc(false) Supports software encoding only.</li>
         * <li>4. builder.setVideoBitrateMode(ENCODE_BITRATE_MODE.ENCODE_BITRATE_VBR) Not supported at the moment.</li>
         * </ul>
         */
        bitrateMode = NLE_ENCODE_BITRATE_MODE.ENCODE_BITRATE_CRF
    }

    compileDialog.show()
    compileNLESession.exporterApi.compile(outFilePath, compileSettings, object : INLEListenerCompile {
        override fun onCompileError(p0: Int, p1: Int, p2: Float, p3: String?) {
            runOnUiThread {
                Toast.makeText(context, "Error during export: $p3", Toast.LENGTH_SHORT).show()
                compileDialog.dismiss()
            }
        }

        override fun onCompileDone() {
            runOnUiThread {
                Toast.makeText(context, "Export completed successfully", Toast.LENGTH_SHORT).show()
                compileDialog.dismiss()
                // Play the exported video using Android's built-in player
                PreviewUtils.previewExportVideo(context, outFilePath)
            }
        }

        override fun onCompileProgress(p0: Float) {
            runOnUiThread {
                compileDialog.setProgress((p0 * 100).toInt())
            }
        }
    })
}
```
