---
title: "Running the iOS React Native project"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-running-the-ios-react-native-project"
---

You can run the React Native (RN) project on a simulator or real device.

<span id="40aab108"></span>
# **Prerequisities**

Before you begin with creating RN projects, ensure that the following requirements have been met:


* Downloaded Xcode.

* Add the dependencies using Cocoapods. For details, refer to [Managing dependencies using Cocoapods](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-dependencies-using-cocoapods).

* Retrieve your SDK package from your BytePlus representatives. For more information, refer to the [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/150-ios-package-deliverables-list).

* Set up your RN environment. For more information, refer to the [RN developers guide](https://reactnative.dev/docs/set-up-your-environment?platform=ios).

* Completed the steps in: [Creating React Native projects in iOS](https://docs.byteplus.com/docs/video-editor-sdk/140-creating-react-native-projects-in-ios).


<span id="d4c31688"></span>
# Running on simulators

Navigate to the root directory of your React Native project in the terminal and execute:

```Plain
npx react-native run-ios 
```


Or, if you have `yarn` installed:

```Plain
yarn react-native run-ios 
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Do not connect a physical device while running on the simulator, as it may cause the operation to fail.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d11f098970ee44b680122f1e82484043~tplv-goo7wpa0wc-image.image) </span>

<span id="9705d21b"></span>
# Running on real devices

To run on a physical device, configure a developer certificate. Once the certificate is set up, navigate to the `ios` folder of your React Native project, double\-click the `xxx.xcworkspace` file to open the project in Xcode, and run the project. For more information on configuring a developer certificate, refer [here](https://reactnative.dev/docs/running-on-device).
