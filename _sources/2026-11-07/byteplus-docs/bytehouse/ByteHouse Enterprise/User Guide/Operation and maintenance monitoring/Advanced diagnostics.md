---
title: "Advanced diagnostics"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/advanced-diagnostics"
---

**Advanced Diagnosis Mode** is a configuration that collects more granular information, including behaviours such as CPU/memory flame graphs, which can help Users analyze the use of memory and CPU within the Cluster. This document explains how to Activate/Terminate Advanced Diagnosis Mode and the related advisories to consider.

<span id="afb0afa7"></span>
## Cautions


* Activating Diagnosis Mode will result in about a 10% performance loss in CPU/memory load;

* Activating/Terminating Diagnosis Mode requires a Cluster Restart, during which the Service will be Not Available; please operate with caution.


<span id="ef42f8ee"></span>
## Enable advanced diagnosis


1. Visit **ByteHouse Console \> Manage Clusters \> List \> Cluster Details**, then Click on the “Load & Resource Group” tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83123c42b7b44a4b8d73a2bff872c66d~tplv-goo7wpa0wc-image.image) </span>

2. Activate the "Advanced Diagnosis Mode" button on the right side of the tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21cadf33420b4817af128e5de7a6fd92~tplv-goo7wpa0wc-image.image) </span>

3. The system will prompt you to select the configuration to activate the diagnosis mode.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d147cec3e5bb470698eb5f5e5aa785de~tplv-goo7wpa0wc-image.image) </span>

   1. Diagnosis Strategy:

      1. The default threshold to generate flame graphs is **80%** , with a frequency of **every 5min.** 

      2. You can click the customize button to set the thresholds and timing separately for CPU and memory flame graphs.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf66ef3f033f4e4189eba08b86e84b72~tplv-goo7wpa0wc-image.image) </span>

   2. Activating advanced diagnostic mode requires restarting the cluster. Please choose to restart immediately or later according to the current business usage.

      <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="2">danger      </div>
      

      <div data-tips="true" data-tips-type="danger" data-wrapper-indent="2">If you restart the cluster immediately, it may cause the service to be unavailable and will lead to running missions failing. Please proceed with caution.      </div>
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb7e05ef4caa4c6685c83178b5ccda8f~tplv-goo7wpa0wc-image.image) </span>

4. After clicking confirm, a system prompt "Advanced diagnostic mode activated successfully" indicates the completion of settings.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If "Restart later" was selected during configuration, the system will continue to remind you that a restart is needed to activate the settings. Please proceed to restart the cluster from the cluster list or cluster detail page subsequently.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70f627e6c07845f88b11822420a34aa2~tplv-goo7wpa0wc-image.image" width="1366px" />   </div>
   

<span id="85cb1489"></span>
## Disable advanced diagnosis


1. Access the **BytePlus Console \> Manage Clusters \> Cluster List** page, and all clusters that have started the “Advanced Diagnosis” feature will be marked as “Diagnostics on ” in their status bar.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8c40e05d4e848c3a967e3c61448ae58~tplv-goo7wpa0wc-image.image) </span>

2. Click on the cluster name to enter the cluster's detail page, access the “Load & Resource Group” tab, and click the button at the location shown in the image below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ba14f81787d4413a35824c6231c83ee~tplv-goo7wpa0wc-image.image) </span>

3. The system will prompt a second time to confirm whether to turn off the Advanced Diagnosis Mode. Click OK.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef0ceb1f25904115ab54cadd9762981a~tplv-goo7wpa0wc-image.image) </span>

4. If the system prompt indicates "Disabling Advanced Diagnostic Mode Successful," it means the settings are complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4baea778e5d40e3a5299d40d6336536~tplv-goo7wpa0wc-image.image) </span>
