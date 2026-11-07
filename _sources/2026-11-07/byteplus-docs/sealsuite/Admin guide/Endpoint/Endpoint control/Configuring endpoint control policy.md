---
title: "Configuring endpoint control policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-control-rules"
---

By using the device baseline's control policy function, you can establish monitoring policies for employee devices within the company. SealSuite actively monitors in real\-time according to the policy, quickly identifying risk events and providing robust support for security compliance within the enterprise.

<span id="22166090"></span>
# Adding control policies


1. Log in to the SealSuite Admin Console.

2. In the left sidebar, select **Endpoint** \> **Endpoint Control** \> **Endpoint Baseline**.

3. In the **Policy Management** tab, click **New Policy**.

4. On the **New Baseline Scanning Policy** page, complete the following configurations and click **Confirm**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Policy Name |Custom name for identifying the current policy. |
   |Priority |Set the priority level for the policy to be activated. The value range is 0 to 100, with higher numbers indicating higher priority. You can enable multiple policies at the same time. SealSuite, when detecting devices, matches policies in order of priority value, stopping once a policy is hit. If there is no hit, it will stop after executing all policies. If there are two policies with the same priority value, the one with the most recent edit time will be executed first. |
   |Detection Item |Supports setting **Endpoint Baseline Scanning**, **Application Security Scanning**, and **Backend Process Scanning**. Selecting one or more of these detection items will display specific configuration areas on the current page, where you will need to complete configurations for each selected item. Detailed descriptions are as follows:<br><br><br>* **Endpoint Baseline Scanning**: After enabling, click **Add New Item**, and in the **Configure Scan Items and Alerts** dialog box, you can manually set the required detection items for each operating system and their risk levels (**High Risk**, **Medium Risk**, **Low Risk**).<br><br>* **Application Security Scanning**: After enabling, click **Add New Application**, and then click **Non\-Compliant Application** or **Mandatory Application**. If non\-compliant application is selected, this policy will be used to monitor whether the specified non\-compliant application is installed on enterprise devices. If mandatory application is selected, this policy will be used to monitor whether the required mandatory application is installed on enterprise devices. In the **Select Non\-Compliant Application** dialog box or the **Select Mandatory Application** dialog box, select the specified application and set the application's risk level (**High Risk**, **Medium Risk**, **Low Risk**).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The application list allows for custom addition or removal of applications. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/sealsuite/docs-configure-detection-items">Configuring device scanning items</a>.   </div><br>   <br><br>* **Backend Process Scanning**: After enabling, click **Add Process Group**, and then click **Non\-compliant process group** or **Mandatory process group**. If non\-compliant process group is selected, this policy will be used to monitor whether the specified non\-compliant process is running on enterprise devices. If mandatory process is selected, this policy will be used to monitor whether the required mandatory process is installed on enterprise devices. In the **Configure Non\-Compliant Process Groups** dialog box or the **Configure the required process group** dialog box, set process information and risk levels (**High Risk**, **Medium Risk**, **Low Risk**) for different operating systems. |
   |Detection Methods |Select one or all of the two methods, **Scheduled Scanning** or **Triggered Scanning**.<br><br><br>* **Scheduled Scanning**: SealSuite will perform periodic scans of device risk events according to the set time conditions. After selecting **Scheduled Scanning**, you need to set the **Scanning frequency** and **Effective time period** in the displayed **Scheduled Scanning** area.<br><br>* **Triggered Scanning**: After selecting **Triggered Scanning**, you need to set the **Trigger Method** in the **Trigger event** area. SealSuite will scan risk events when the user operates in a specified way on the devices. |
   |Scope |Support specifying the scope by **User** or **Device**.<br><br><br>* When selecting **User**, you need to restrict user scope through **Department** or **Role**.<br><br>* When selecting **Device**, you need to restrict device scope through **Device**, **OS**, and **Device Group**. |
   


<span id="e37e932d"></span>
# Managing control policies


1. Log in to the SealSuite Admin Console.

2. In the left sidebar, select **Endpoint** \> **Endpoint Control** \> **Endpoint Baseline**.

3. On the **Policy Management** page, locate the specified policy; the following operations are supported.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0db561c9cc3945898485e33b832b0a86~tplv-goo7wpa0wc-image.image) </span>

   * As shown in area ① in the figure above, you can set the policy's effective status.

      * When the switch is turned on, the current policy takes effect, and SealSuite will detect each device event according to the policy configuration.

      * When the switch is turned off, the current policy does not take effect, and SealSuite will not detect the device through this policy.

   * As indicated in area ② above, the policy settings allow you to **Copy**, **Edit**, or **Delete**.

      Once the management policy is deleted, it cannot be recovered. SealSuite will no longer monitor device events through this policy, but previously detected events will still be recorded in the event list.
