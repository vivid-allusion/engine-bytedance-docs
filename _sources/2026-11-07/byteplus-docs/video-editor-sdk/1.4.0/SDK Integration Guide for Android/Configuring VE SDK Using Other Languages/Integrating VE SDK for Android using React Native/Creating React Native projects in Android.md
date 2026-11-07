---
title: "Creating React Native projects in Android"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/140-creating-react-native-projects-in-android"
---

Integrate the Video Editor SDK with React Native (RN) to add powerful video editing features to your app. Use the following steps to handle tasks like video capture, editing, and saving efficiently. Follow the integration guidelines for a seamless setup. Call a command and set up the necessary files and folders for a RN project, including the configuration files, a `package.json` file, and a template code for starting your app.

**Prerequisities**

Before you begin with creating React Native projects, ensure that the following requirements have been met:


* Downloaded Android Studio.

* Retrieve your SDK package from your BytePlus representatives. For more information, refer to [Android sample SDK deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/140-android-sample-sdk-deliverables-list).

* Set up your RN environment. For more information, refer to the [RN developers guide](https://reactnative.dev/docs/set-up-your-environment?platform=ios).


**To create an RN project:** 


1. Open the terminal.

2. Navigate to the desired directory to create an RN project.

3. Run the following command: `npx react-native init XXX`

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>XXX</code> refers to the directory you want to create the RN project in.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca0e0256f96a4471a9d2df44ad6c28c5~tplv-goo7wpa0wc-image.image) </span>

   The RN project is created in the directory.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fb90de79f754880ae5b9aa10ec37c26~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a71b060f0254790a69fac189a983997~tplv-goo7wpa0wc-image.image) </span>

4. Run `npm install` to install the project dependencies.
