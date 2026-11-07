---
title: "Initializing VE SDK without UI"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-initializing-ve-sdk-without-ui"
---

Before using the editing and shooting functions, an initialization step is required to set up the environment. To initiate the process, you need to input the relevant parameters and call the initialization API. For more information, refer to the SDKInitHelper within the demo. The initialization sequence involves VESDK followed by NLESDK.

**To initialize VE SDK without UI:** 


1. Initialize VESDK.

2. Initialize NLESDK.

3. Access the authentication files through the following file path: `editor/src/main/assets/resource/LicenseBag.bundle/labcv_test_20230831_20240930_com.volcengine.ck.sample_4.0.4.0_158.licbag`.

   ```Kotlin
   fun initSDK(context: Context) {
       initVESDK(context)
       initNLESDK()
   }
   
   private fun initVESDK(context: Context) {
       AppSingleton.bindInstance(context)
       CKGlobalConstant.apply {
           veLicensePath = "Name of the authentication file"
           veAppKey = APP_KEY
           veToken = TOKEN
       }
       VEInit.init(context)
       // Return true for successful authentication
       // Return false for authentication failure
       VEInit.initAuth(context)
   }
   
   private fun initNLESDK() {
       NLE.loadNLELibrary()
       // Optional: Insert a logger listener
       NLE.logger = object : NLELoggerListener() {
           override fun onLog(level: LogLevel?, message: String?) {
               // Print the message
           }
       }
       NLE.logLevel = LogLevel.LEVEL_DEBUG
   }
   ```
   


**Parameters**


|**Parameter Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|veLicensePath |String |Yes |editor/src/main/assets/resource/LicenseBag.bundle/labcv_test_20230831_20240930_com.volcengine.ck.sample_4.0.4.0_158.licbag |Name or path of your authentication file. |
|veAppKey |String |Yes |APP_KEY |Authentication key. |
|veToken |String |Yes |TOKEN |Authentication token. |
