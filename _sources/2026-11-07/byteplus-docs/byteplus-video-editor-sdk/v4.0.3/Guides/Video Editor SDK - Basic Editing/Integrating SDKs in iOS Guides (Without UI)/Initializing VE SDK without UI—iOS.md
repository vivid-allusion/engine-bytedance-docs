---
title: "Initializing VE SDK without UI—iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-initializing-ve-sdk-without-ui_1"
---

Before using the editing and shooting functions, an initialization step is required to set up the environment. Only after you have performed a function authentication step, the features you have purchased can be put into use. To initiate the process, you need to input the relevant parameters and call the initialization API. For more information, refer to the SetupHelper within the demo project.

<span id="22685e8b"></span>
# **Module description**

The following table introduces classes related to VE SDK integration.


|**Class Name** |**Description** |
|---|---|
|VEAuthorizationCenter |Performs Video Editor SDK authentication. |


**To initialize VE SDK without UI:** 

```Swift

import TTVideoEditor

let path // the license path
let key = 
let token = 
let modelPath // the ModelResource's path

VEAuthorizationCenter.default().register(withVELicense: path,
                                         audioAppkey: key,
                                         audioToken: token,
                                         modelResourcePath: modelPath) { code, message in
    print("current auth code:", code, "about message is:", message ?? "nil")
} sdkLogCallback: { level, message in
    print("current log level is:", level, "about message is:", message ?? "nil")
} customConfiguration: {
    
}
```


In the above code, BytePlus Video Editor SDK uses the `print` function to write logs to the logging platform.

<span id="011d16ff"></span>
# **Parameters**


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|path |String |Yes |The license path that uses `.licbag` as the suffix. |
|key |String |Depends on the type of BytePlus Video Editor SDK you use.<br><br><br>* Standard: Yes.<br><br>* Lite: No. |The license key. |
|token |String |Depends on the type of BytePlus Video Editor SDK you use.<br><br><br>* Standard: Yes.<br><br>* Lite: No. |The license token. |
|modelPath |String |No |The path of ModleResource.bundle for partial features. |
