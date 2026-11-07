---
title: "Configure network monitoring"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-network-monitoring"
---

SealSuite network monitoring helps employees and administrators understand network quality and troubleshoot issues such as slow application access. This document describes how to configure monitored applications, alerts, and notifications, and shows the client\-side result.

## Overview

When employees access business applications, issues such as lag, high latency, or unstable connections may be related to the local network, VPN connection, or the access path to application services. SealSuite network monitoring continuously checks the network quality from the client to services. It helps employees and IT administrators understand the status of each path segment and narrow the troubleshooting scope.

administrators specify the business applications to monitor through **Application Configuration**. The client monitors access quality based on the application address and port. administrators set packet loss rate and latency thresholds through **Alert Configuration**. When the corresponding threshold is exceeded, the client marks the exception in red and triggers a network monitoring alert. administrators can also specify users or devices in scope and control whether monitoring data is displayed in the client.

The following figure shows how application configuration and alert parameters map to the client. The latency and packet loss rate in the figure are sample values.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/monitor-guide.png)

Network monitoring provides the following features:

* **Monitor network quality for business applications**: Detect the network quality of client access to intranet applications and internet applications based on the configured application addresses and ports. This helps identify application access exceptions that affect daily work.

* **Display quality data for each path segment**: Display data such as packet loss rate and latency from the device to the router, VPN, and application services. This helps determine which path segment to check first. For example, if employees access internal applications slowly, they can compare data for the local network, VPN, and application paths to further determine the troubleshooting direction.

* **Trigger network alerts based on thresholds**: If the packet loss rate or latency of a path segment exceeds the threshold set by an administrator, a network monitoring alert is triggered on the client. This helps employees detect network quality exceptions promptly. administrators can also configure report notifications (optional) to receive alert information through associated third\-party bots.

* **View network quality details**: When monitoring data is displayed in the client, employees can view real\-time data, network latency trends, and monitoring details for each application. This provides evidence for describing faults and subsequent troubleshooting.

Network monitoring applies to the following enterprise scenarios:

* **Many branch offices or remote work locations**: Employees access business systems from different regions. IT teams need to understand access quality at different office locations and troubleshoot local network issues.

* **Key business systems have high network stability requirements**: Lag during business system access affects daily work, so the network quality of related applications must be monitored continuously.

* **Network issues occur intermittently**: Faults may have recovered by the time employees report them. IT teams need to analyze issues based on monitoring data and latency trends.

## Configuration steps

To configure network monitoring, specify the business applications to monitor first. Then set alert thresholds, users or devices in scope, and the client display mode.

Before configuration, note the following:

> **说明**

* > When configuring monitored applications, add business applications that employees use frequently or that are sensitive to network quality first. Enter the actual addresses and ports that provide services. Set **Application type** and **Effective area** based on where the application is deployed. Then set alert thresholds for each path segment based on business requirements. This aligns monitored objects and alert conditions with enterprise office requirements.

* > Network monitoring supports only TCP applications. For intranet applications, latency is detected only after the VPN is connected. If employees need to view monitoring data, set **Whether to hide the client display** to **Do not hide**.

Configure and enable network monitoring as follows:

1. Log in to Admin Console. In the left navigation pane, choose **Settings** \> **IT Tools**.

2. In the **Network Utilities** area, click the **Network monitoring** card.

3. Configure monitored applications.

   Monitored applications are business applications whose network quality needs to be checked, such as internal office systems or internet applications commonly used by employees. After application addresses and ports are added, the client detects network quality to application services based on this information.

   In the **Application Configuration** area, click **Add New Application** and complete the following configuration.

   |Configuration item |Description |
   |---|---|
   |**Application icon** |Used to identify the application in the monitoring list and client. Use the default icon, or click **Re\-upload** to set a custom icon. |
   |**Software name** |Used to identify the application in the monitoring list and client. Enter a name that employees can easily recognize, up to 30 characters. |
   |**Application address** |Specifies the application service address to detect. Enter a single domain name or IP address. Only TCP applications are supported. |
   |**Application type** |Used to distinguish intranet applications from internet applications. Select **Intranet application** or **Internet application** based on the actual deployment of the application. For intranet applications, latency is detected only after the VPN is connected. |
   |**Application port** |Specifies the service port to detect. Enter the port on which the application actually provides services. The valid range is 1–65535. |
   |**Effective area** |Specifies the geographic scope for application monitoring. Select **Effective globally**, or select **Effective in specified geographic locations** and select one or more regions. |

   Click **Confirm** to add the application to the monitoring list. To make changes, click **Edit** or **Delete** in the operation column of the corresponding application.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/monitor-apps.png)

4. Configure **Alert Configuration**.

   Alert parameters define the criteria for identifying network quality exceptions. When the packet loss rate or latency of a path segment exceeds the corresponding threshold, the client triggers a network monitoring alert. Configure thresholds for the following three path segments:

   |Configuration item |Description |
   |---|---|
   |**Device to router** |Used to determine whether the network quality of the path between the device and the router is abnormal. Set thresholds for packet loss rate (%) and latency (ms). |
   |**Device to VPN** |Used to determine whether the network quality of the path from the device to the VPN is abnormal. Set thresholds for packet loss rate (%) and latency (ms). |
   |**Device to software** |Used to determine whether the network quality of the path from the device to the application service is abnormal. Set thresholds for packet loss rate (%) and latency (ms). |

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/monitor-thresholds.png)

5. Configure **Scope** and client display.

   Effective objects determine which employees or devices use network monitoring. The client display option determines whether monitoring data is displayed to employees. Complete the following configuration:

   |Configuration item |Description |
   |---|---|
   |**Function scope** |Specifies which employees or devices enable network monitoring. Select **User** or **Device**, and add the corresponding departments, roles, employees, devices, or groups. |
   |**Exclude object** |Specifies objects within the scope that do not need network monitoring enabled. To exclude objects, enable this option and select the objects. |
   |**Whether to hide the client display** |Controls whether employees can view network quality values and monitoring data in the client. By default, the current network quality value is displayed in the client. Select **Do not hide** to display the content, or select **Hide** to hide it. |

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/monitor-scope-live.png)

6. Click **Confirm** to save the configuration, and confirm that the **Network monitoring** switch is enabled on the IT tools page.

## Configure report notifications (optional)

After report notifications are configured, administrators can receive alert notifications through associated third\-party bots when the client detects that an application's network quality is worse than the configured alert threshold and matches the selected notification issue type. After the notification frequency limit is enabled, at most one notification is sent every X hours, where X is the configured number of hours.

Set the notification type, receiving bot, and notification content as follows:

1. In Admin Console, choose **Enterprise Settings** \> **Admin Center** \> **User Feedback**, and click **Notifications**.

2. In **Notification type**, select **Report notice** or **Disposal notice**. Multiple selections are supported.

3. Complete the configuration for each selected notification type.

   |Configuration item |Description |
   |---|---|
   |**Type of issue notified** |Specifies the issue types for which notifications need to be sent. Select **All notifications**, or select **Partial type notification** and then select multiple issue types that require notifications. |
   |**Select Third\-Party IM** |Select the bot used to receive notifications. To create a bot, click **New Integration**. For detailed operations, see [Manage third-party IM](https://docs.byteplus.com/docs/sealsuite/docs-overview-of-notifications#7e2d6168). |
   |**Third\-party notification content** |Set the notification title, and fill in the notification content defined with number signs (#) based on the template. The default title of report notifications is **Issue feedback notification**. The default title of remediation notifications is **Problem Handling Notice**. |
   |**Limit notification frequency** |Used to limit the sending frequency of report notifications. After selecting this option, set the number of hours X. At most one notification is sent every X hours. |

   > **说明**

   > To restore the default notification title and content, click **Reset content** in the upper\-right corner.

4. Click **Confirm**.

## Client\-side result

After network monitoring is enabled and **Do not hide** is selected, employees within the scope can view network quality and monitoring details through the following entry points. The following table describes the information available in each view:

|View |What employees can see |
|---|---|
|**Overview page entry** |View the current network quality and go to monitoring details. |
|**Lab entry** |Open **Network monitoring** in **Lab**. |
|**Network monitoring details** |Compare the path status from the device to the router, VPN, and applications, and view real\-time data and network latency trends. |
|**Application monitoring details** |Open application details and view the monitoring result of each application. |
