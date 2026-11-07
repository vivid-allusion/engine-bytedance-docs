---
title: "iOS React Native FAQ"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-ios-react-native-faq"
---

These are some frequently asked questions about React Native projects.

<span id="4aae56e4"></span>
# 1. What should I do if I encounter a prompt after executing the command `npx react-native init XXX`?

If you encounter a prompt asking whether to install CocoaPods, enter `y`. CocoaPods is required to integrate the SDK in this tutorial.

<span id="46e21b86"></span>
# 2. What should I do if I accidentally enter `n` instead of `y` when prompted to install CocoaPods?

If you accidentally enter `n`, you can manually set up CocoaPods later.

**Follow these steps**:


1. Wait for the React Native project creation to complete.

2. Open the terminal and navigate to the `iOS` folder of your project.

3. Run `bundle install` to create the CocoaPods environment.

4. Execute the command `pod install` to install the necessary CocoaPods dependencies.
