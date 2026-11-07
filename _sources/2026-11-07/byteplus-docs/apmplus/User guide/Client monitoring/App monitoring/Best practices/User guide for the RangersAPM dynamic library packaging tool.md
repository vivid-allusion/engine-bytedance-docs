---
title: "User guide for the RangersAPM dynamic library packaging tool"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/User_guide_for_the_RangersAPM_dynamic_library_packaging_tool"
---

RangersAPMDylibTool is a macOS desktop tool designed to package multiple static library submodules of RangersAPM/APMPlus into a single XCFramework, which can be integrated with iOS projects as a dynamic library.

The tool supports the following output formats:


|**Output format** |**Description** |
|---|---|
|SPM |Generates XCFramework files, which can be manually dragged into the project or referenced via the local Swift Package Manager. |
|CocoaPods |Generates XCFramework and podspec files, which can be integrated via a private pod repository or a local source. |


<span id="EismVqDC"></span>
## Prerequisites


* The macOS system environment has been prepared.

* The network connection is stable. This ensures that GitHub can be accessed to download static libraries during the build process.

* RangersAPMDylibTool has been downloaded and trusted in **System Settings** \> **Privacy & Security**.

* If the project already integrates RangersAPM/APMPlus add\-ons as static libraries via CocoaPods or SPM, remove them before integrating the dynamic library version to prevent symbol conflicts.


<span id="k5E2mBaE"></span>
## Procedure


1. Download RangersAPM

   Download and decompress the compressed package. You can then launch RangersAPMDylibTool.

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_22ce04c2a2f8fbc0cff49b91f8812ff4.zip" name="RangersAPMDylibTool.zip">RangersAPMDylibTool.zip</Attachment>
   

2. Select a version number

   After starting the tool, select the desired RangersAPM version number (such as 5.2.15), then click **Obtain available add\-ons**.

3. Select the sub‑libraries and output format

   Select the desired sub‑libraries (such as Crash and WatchDog) and select an output format. Then, click **Generate dynamic libraries**. For details about sub‑libraries, see [Sub‑library descriptions](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app?lang=en).

4. Build the dynamic library

   The tool automatically builds the dynamic library and generates build logs. If the build fails, click **Copy error message** to obtain the complete error log for troubleshooting. For details, see [FAQs](https://docs.byteplus.com/en/docs/apmplus/User_guide_for_the_RangersAPM_dynamic_library_packaging_tool?lang=en#2UVE81s6).

5. Export the output

   After the dynamic library is built, click **Select directory and export**. The tool will export the final output to the specified directory.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The final output is a single dynamic framework called RangersAPMDylib, which includes all the selected sub‑libraries.   </div>
   

<span id="2UVE81s6"></span>
## FAQ

<span id="O3lPq0bf"></span>
### Which architectures does RangersAPM support?


* Physical device: arm64

* Simulator: arm64/x86_64 (simulators on Apple Silicon Macs are supported)


<span id="ATZzrzY9"></span>
### **How do I handle build failures?** 

Click **Copy error message** and send logs to technical support for troubleshooting. Common failure reasons and descriptions are as follows:


|**Failure reason** |**Description** |
|---|---|
|Network timeout |The build process requires pulling dependencies from GitHub. Check the network connection and proxy settings. |
|Version number does not exist |The entered version number does not exist in the remote repository. Check whether the version number is correct. |
|Missing system framework dependencies |The new version may introduce system framework dependencies that are not covered. Contact technical support. |


&nbsp;

&nbsp;

&nbsp;

&nbsp;
