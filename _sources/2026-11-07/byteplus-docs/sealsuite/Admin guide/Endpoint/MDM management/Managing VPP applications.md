---
title: "Managing VPP applications"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/managing-vpp-applications"
---

SealSuite allows you to centrally manage applications purchased through the **Apple Volume Purchase Program (VPP)** . Within the Admin Console, you can synchronize application and license data, track installation progress across devices, and initiate application distribution tasks.

<span id="d8f88e2a"></span>
## Prerequisites

Before using these features, you must successfully configure a **VPP Token** in the **Endpoints** \> **MDM Management** \> **Apple Configuration** page. For detailed instructions, see [Configuring VPP Tokens](https://docs.byteplus.com/docs/sealsuite/configuring-apple-mdm-services#a559b10b).

<span id="7639ef29"></span>
## The VPP App Library

The VPP App Library displays all applications purchased by your organization. Using the configured VPP Token, SealSuite automatically pulls application metadata and license information from your **Apple Business Manager (ABM)**  or **Apple School Manager (ASM)**  account.

<span id="2072ec2c"></span>
### Synchronizing Data

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07ac6ccdc59d4dc5b7fd7202d77d08ca~tplv-goo7wpa0wc-image.image) </span>


* **Automatic Sync**: The system performs a daily synchronization to ensure application and license data are up to date.

* **Manual Sync**: If you have recently purchased new apps or adjusted license counts in ABM/ASM and need them to appear in SealSuite immediately, click **Sync Apps & Licenses** in the top right of the list.


<span id="e9f99423"></span>
### Viewing the App List

Navigate to **Endpoint** \> **MDM** \> **VPP Application** to view your library:


|Column |Description |
|---|---|
|**App ID** |The unique identifier for the application. |
|**Name** |The name and icon of the application. |
|**Compatibility** |The supported operating systems (e.g., macOS, iOS, iPadOS). |
|**Location** |The VPP Token location associated with the app. |
|**Version** |The latest version available in the App Store. |
|**Genre** |The official App Store classification (e.g., Productivity, Business). |
|**Allocated/Available** |The number of allocated licenses versus the total number of licenses purchased. |
|**Actions** |* **Details**: Access the data dashboard and device\-level management.<br><br>* **Distribute**: Create a one\-time deployment task for the app. |


<span id="c598543c"></span>
## Application Insights and Device Management

Clicking **Details** for a specific app opens a management dashboard focused on deployment health and granular device control.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c756da4c9904f5392450bb6a061954a~tplv-goo7wpa0wc-image.image) </span>

<span id="eca8f391"></span>
### Installation Dashboard

This tab provides a high\-level overview of the app's footprint:


* **Licenses Summary**: An overview of license consumption.

* **Install Count & Rate**: The total number of successful installs and the percentage of assigned devices that have completed the installation.

* The number of installations managed by SealSuite MDM.

* **Managed Ratio**: The percentage of installed apps that are "Managed".

* **Version Distribution**: A visual breakdown (donut chart) of the different versions currently running on devices.


<span id="f119d60c"></span>
### Detailed Device List

Below the dashboard is a list of all devices assigned a license for this app. You can perform the following targeted actions:


|Action |Condition |Description |
|---|---|---|
|**Install App** |Status: "Not Installed" |Pushes an MDM command to trigger the installation on the device. Does not affect license assignment. |
|**Revoke License** |Status: "Not Installed" |Reclaims the assigned license from the device via Apple VPP services, making it available for other users. |
|**Remove App & License** |Status: "Installed" |A two\-step process: First, the license is revoked; second, an MDM command is sent to uninstall the app from the device. |


<span id="a0ec1c84"></span>
### App Information

By switching to the **Information** tab, you can view the detailed metadata for the selected VPP application. All information in this section is synchronized directly from the App Store, providing a comprehensive overview of the application’s specifications, including version history, developer details, and supported features.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f55682881704ac18bee26e5159bf186~tplv-goo7wpa0wc-image.image) </span>

<span id="59f7078a"></span>
## Distributing VPP Applications

The **Distribution** feature is used to create one\-time installation tasks for specific device groups. This is ideal for rapid, ad\-hoc deployments.

> **Note**: For mandatory, long\-term application management (e.g., ensuring an app is permanently installed on all Department A devices), please use the **VPP App Installation** feature. See [Configuring and managing MDM policies](https://docs.byteplus.com/docs/sealsuite/configuring-and-managing-mdm-policies).


<span id="8e6af320"></span>
### Creating a Distribution Task


1. Navigate to the **VPP App Library** and click **Distribute** next to an app, or go to the **Application Distribution** tab and click  **+ Add Distribution Job**.

2. Configure the following four modules:

   
   |Module |Parameter |Description |
   |---|---|---|
   |**General** |**Name & Description** |Identifiers for the distribution task. |
   |**Application** |**Import from App Library** |Filter by location and select the target VPP app for distribution. |
   |**Distribution Configuration** |**Expire in** |Sets the task's duration (Default: 7 days). The task expires automatically after this period. |
   ||**MDM Advanced Management** |Enable for granular enforcement:<br><br><br>* **Disable manual removal of the app**: Prevents users from manually uninstalling the app.<br><br>* **Disable automatic app backup to iCloud**: Prevents app data from syncing to the cloud.<br><br>* **Remove the app upon MDM unenrollment**: Uninstalls the app if the device is removed from SealSuite MDM.<br><br>* **Custom XML configuration**: Upload configuration profiles for specialized app settings. |
   |**Scope** |**Assignment** |Choose the target audience by **User** or **Device**. |
   ||**Exclude object** |Specify users or devices that should be exempt from this policy. |
   

3. Click **Distribute Now** to launch the task.


<span id="2a5e03e8"></span>
## Monitoring and Managing Tasks

All distribution tasks are listed under the **Application Distribution** tab.


* **Task List Management**

   * **Track Status**: Monitor real\-time progress (**In Progress**, **Completed**, or **Canceled**).

   * **View Details**: Access device\-specific execution data.

   * **Cancel Task**: Manually terminate any task that is currently **In Progress**.

* **Task Details and Troubleshooting**

   Click **View** in the Actions column to open the **Details** page, which allows you to drill down into the performance of a specific task.

* **Distribution Status**

   * **Status Overview**: A chart showing the distribution of results: **Pending** (pending device response), **Success**, **Failure**, or **Canceled**.

   * **Detailed Device List**: A per\-device breakdown of the task status.

      * Use filters to locate specific devices.

      * Click **View Log** in the Actions column to diagnose specific installation failures and review MDM command history.

* **Distribution Task Review**

   The **Distribution Job** tab allows you to review the original parameters (apps, advanced controls, and scope) used when the task was created.
