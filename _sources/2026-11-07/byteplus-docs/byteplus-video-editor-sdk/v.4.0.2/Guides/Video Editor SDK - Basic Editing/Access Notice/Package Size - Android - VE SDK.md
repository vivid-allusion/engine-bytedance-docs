---
title: "Package Size - Android - VE SDK"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-package-size-android-ve-sdk-v.4.0.2"
---

<span id="Size statistics on the package of Version 960:"></span>
# Size statistics on the package of Version 960:

<span id="VE SDK"></span>
# VE SDK

The total size of the .aar package is 38.9 MB, including the following items:


* arm64\-v8a: 20.1 MB

* armeabi\-v7a: 17 MB

* Others: 2.2 MB

* If the package is integrated only into a framework.so with a 64\-bit CPU, the size increment is approximately 22 MB.

* If the package is integrated only into a framework.so with a 32\-bit CPU, the size increment is approximately 19 MB.

* If the package is integrated into both of the above frameworks.so, the size increment is approximately 40 MB.


<span id="NLE"></span>
# NLE

The size of the nleeditor.aar file is approximately 2.3 MB.


* arm64\-v8a: 994 KB

* armeabi\-v7a: 850 KB

* Others: 570 KB


<span id="Minimize the package size"></span>
# Minimize the package size


* If you don¡¯t need the model files in the SDK, you can complete relevant configurations so that these files are not packaged into the APK file. The path of the model files is assets/model.


```Plain
android {
    buildTypes {
        release {
            aaptOptions {
                ignoreAssetsPattern '!model:'
            }
        }

        debug {
            aaptOptions {
                ignoreAssetsPattern '!model:'
            }
        }
        
    }
}
```



* Deliver assets through a server and download the assets only when you need them.
