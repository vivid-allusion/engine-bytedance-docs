---
title: "Customizing Windows process configuration"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/customizing-windows-process-configuration"
---

When you add a Windows custom application in the application control and block sections, you must configure the Windows process. This article introduces how to get the process information of the application.

<span id="9d325286"></span>
# Application description

Custom applications have restrictions on the source channel, which currently only supports drag and drop, copy\-paste, and file open dialog scenarios. Other source channel methods, such as double\-clicking file uploads via FileZilla or other FTP software, are not supported.

<span id="901b06a7"></span>
# Version compatibility description

Custom applications generally do not differentiate between software versions. However, this is not always the case. In practice, compatibility depends on whether there have been changes in the software implementation, which can be verified through actual testing.

<span id="d8bc25ea"></span>
# Application feature extraction

Currently, custom applications only require the application process name. You simply need to extract and configure this information. You can obtain the process name information through the task manager, and it is not case\-sensitive.

The Task Manager displays the process name information for WeCom, which includes multiple process names such as WXWork.exe and WXWorkWeb.exe. Typically, WXWork.exe is the main configuration used, as most software currently adopts this multi\-process architecture. As a result, the accurate process name needs to be identified.

<span id="13048c2e"></span>
# Extraction of multi\-process application process information

When an application has multiple process name information, it is first necessary to identify the actual outgoing process name. This can be done using the procmon software following these steps:


1. Prepare a test file in advance, with the agreed filename as **Test File.docx.** 

2. Open the procmon software, then configure the file path filter, which includes **Test File.docx**, and set up a file read filter.

3. Send out **Test File.docx** through the application.

4. Observe the procmon output, find the process name column, and extract the process name information.


The following video demonstrates using WeCom.

During the actual process, there will be many process names reading files, and it is necessary to find the process name belonging to the application.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fc061cd300148d0816398d106dac1b0~tplv-goo7wpa0wc-image.image" width="1824px" /></div>


<span id="a36749bb"></span>
# A quick test of custom application

After updating the custom application configuration, you need to wait for the client environment to reflect these changes. To expedite testing, manually set a process name first. Then, manually update the process names of all other applications to this pre\-configured name to quickly check application support.
