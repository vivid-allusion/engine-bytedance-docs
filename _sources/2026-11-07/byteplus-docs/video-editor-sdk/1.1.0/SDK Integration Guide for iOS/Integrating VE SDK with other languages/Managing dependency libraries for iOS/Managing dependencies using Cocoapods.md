---
title: "Managing dependencies using Cocoapods"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-managing-dependencies-using-cocoapoads_1_1_0"
---

Learn how to integrate BytePlus Video Editor SDK into iOS through CocoaPods. In CocoaPods, you can integrate the SDK through remote configurations and local configurations.

<span id="faf4de31"></span>
# Remote integration

To remotely integrate the Video Editor SDK through CocoaPods, you only need to add the following code to your Podfile:

```Plain
pod 'EffectOneKit', '1.1.0', :source =>'https://github.com/volcengine/volcengine-specs'
```


<span id="1180a12a"></span>
# Local integration

To locally integrate Video Editor SDK through CocoaPods, you can use the following steps:

<span id="424d77bb"></span>
## Step 1: Import dependencies

You can choose one of the following methods to import dependencies into your project.

<span id="28ea8493"></span>
### Method 1: Importing dependencies without reusing the code of EffectOneKit's export function

There are two methods to locally import dependencies without reusing the code of EffectOneKit's export function:


* CocoaPods

* xcframework


<span id="9aa159a5"></span>
#### **Locally importing dependencies using CocoaPods**

You can locally import your dependencies using CocoaPods.

**Locally importing dependencies using CocoaPods**:


1. Copy and paste the `EffectOneKit.podspec` and `EffectOneKit.xcframework` files obtained from the demo SDK package into the root directory of your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">These two files need to be placed at the same level as your Podfile.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5676fc415f524afca542c272c2abc69e~tplv-goo7wpa0wc-image.image) </span>

2. Add the following to your Podfile:

   ```Java
   pod 'EffectOneKit', :path => './'
   ```
   

3. Run the following command on the command line:

   ```Java
   pod install 
   ```
   


<span id="167dcacc"></span>
#### **Locally importing dependencies using** **xcframework**


1. Copy and paste the `EffectOneKit.xcframework` obtained from the demo SDK package into the root directory of your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This file needs to be placed at the same level as your Podfile.   </div>
   

2. Open your Xcode project.

3. In the project navigator, select your target document folder.

   After you click on your target folder, the page automatically jumps to the **General** tab.

4. Under the **Frameworks, Libraries, and Embedded Content** section, click the expand button.

5. In the pop\-up dialog box, select **Add Other** \> **Add Files**.

6. Select the EffectOneKit.xcframework file and click **Open**.

7. In the **Frameworks, Libraries, and Embedded Content** section, locate the newly added EffectOneKit.xcframework file and click on the **Embed** column.

8. In the drop\-down list that appears, select **Embed & Sign**.


<span id="ca3019ba"></span>
### Method 2: Importing dependencies by reusing the code of the EffectOne export function


1. Copy and paste the `EffectOneKit.xcframework`, `EOExportUI`, and `EOExportUI.podspec` files obtained from the demo SDK package into the root directory of your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">These files need to be placed at the same level as your Podfile.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c3ec19704fb4c16acbff2070f9be25e~tplv-goo7wpa0wc-image.image) </span>

2. Add the following to your Podfile:

   ```Java
   pod 'EOExportUI', :path => './'   
   ```
   

3. On the `Build Settings` tab, search for `User script sandboxing` and set it to **No** for the `targets`.

4. Run the following command on the command line:

   ```Java
   pod install 
   ```
