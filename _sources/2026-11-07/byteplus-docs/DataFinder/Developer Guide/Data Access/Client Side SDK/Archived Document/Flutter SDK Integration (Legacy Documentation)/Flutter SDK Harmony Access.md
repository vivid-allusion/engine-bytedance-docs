---
title: "Flutter SDK Harmony Access"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Flutter_SDK_Harmony_Access"
---

<span id="17404c71"></span>
# 1. Access to Harmony

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">First confirm that the host side has been connected to Harmony flutter according to Huawei's official documents: https://gitee.com/openharmony\-sig/flutter_flutter</div>


<span id="9859a03a"></span>
## 1.1 Introduction of Harmony event tracking SDK

Please refer to [HarmonyOS Next SDK Integration](https://docs.byteplus.com/docs/DataFinder/HarmonyOS_Next_SDK_Integration_) the dependencies of the native SDK and add the corresponding permissions

<span id="10409c7e"></span>
## 1.2 Integrated flutter plugin

Add `rangers_applog_flutter_plugin`dependencies in `pubspec.yaml`for Flutter project

```yaml
dependencies:
  ......
  rangers_applog_flutter_plugin: 1.4.1
```


And install the plugin

```shell
flutter packages get
```


Harmonynative project adds plugins (generally it will be automatically linked after installing dependencies, you need to check it yourself)

```TypeScript
import RangersApplogFlutterPlugin from 'rangers_applog_flutter_plugin';
// GeneratedPluginRegistrant.ets
export class GeneratedPluginRegistrant {

  static registerWith(flutterEngine: FlutterEngine) {
    try {
      //Add RangersApplogFlutterPlugin here
      flutterEngine.getPlugins()?.add(new RangersApplogFlutterPlugin());
    } catch (e) {
      Log.e(
        TAG,
        "Tried to register plugins with FlutterEngine ("
          + flutterEngine
          + ") failed.");
      Log.e(TAG, "Received exception while registering", e);
    }
  }
}
```


<span id="477db700"></span>
## 1.3 For other integration steps, please refer to the main document.

See [Flutter SDK Integration and Event Tracking](https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Integration_and_Event_Tracking).

<span id="cc41657e"></span>
# 2 Frequently Asked Questions

<span id="1b24eefe"></span>
## Q1 run times' @volcengine/applog@1.3.0\-rc 'package not found

Because the Harmony version is still in rapid iteration and has not been released to Huawei's official warehouse for the time being, you need to contact BytePlus technical support staff to obtain the offline package.

After getting the offline package, add the offline package of @volcengine/applog in the root directory/ohos/har/, and then add overrides in the root directory/ohos/oh\-package.json5.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/708e8db72679434d802affc38ce72c6f~tplv-goo7wpa0wc-image.image) </span>
