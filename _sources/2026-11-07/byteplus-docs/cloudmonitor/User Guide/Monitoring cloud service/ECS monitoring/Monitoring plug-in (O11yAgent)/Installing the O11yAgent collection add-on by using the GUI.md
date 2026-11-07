---
title: "Installing the O11yAgent collection add-on by using the GUI"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Installing_O11yAgent_collection_plug-in_in_the_console"
---

This topic describes how to install and upgrade the O11yAgent collection add\-on for Elastic Compute Service (ECS) instances in the Cloud Monitor console, without the need to log in to the ECS instances to use the command\-line interface (CLI).

<span id="982bfb3d"></span>
## Background

The O11yAgent collection add\-on is a new\-generation pipeline used to collect and process observability data, which reduces the complexity of accessing observability systems in cloud environments and allows you to easily benefit more from observability data.

Compared with the cloud\-monitor\-agent add\-on, the O11yAgent collection add\-on provides the following benefits:


* Provides the graphical user interface (GUI) for add\-on installation and upgrade.

* Metrics will be added only based on the O11yAgent collection add\-on.


<span id="95eb37f9"></span>
## Prerequisites

Before you install the collection add\-on for an ECS instance, make sure that the ECS instance is installed with cloud assistant agent (batch job client agent). Otherwise, the installation will fail, and the `CloudAssistantNotInstalled` message will appear. For the method of installing Cloud assistant Agent, refer to [Install Cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, created ECS instances are installed with Cloud assistant Agent. You do not need to manually install it.</div>


<span id="b6d8de5f"></span>
## Automatically install the collection add\-on

You can enable the feature to automatically install the collection add\-on. In this way, created ECS instances will be automatically installed with the O11yAgent collection add\-on.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**.

3. In the top navigation bar, select the target region.

4. At the top of the ECS page, enable Automatically install the collection add\-on for new ECS instances.


<span id="8607c4a1"></span>
## Install the collection add\-on for an ECS instance


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**.

3. In the top navigation bar, select the target region.

4. In the ECS instance list, find the target ECS instance without the collection add\-on installed and click **Install the capture plug\-in** in the Actions column.

5. In the message that appears, click **Confirm** to install the collection add\-on for the ECS instance.

   When the collection add\-on is being installed, **Installing** is displayed in the Capture plugin status column. After the collection add\-on is installed, **Installed** is displayed in the Capture plugin status column, and **Running** is displayed in the Status column.


<span id="d851fa25"></span>
## Install the collection add\-on for multiple ECS instances

You can also install the collection add\-on for all ECS instances without the collection add\-on installed in a region.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can execute only one global installation task at the same time. If you execute multiple global installation tasks at the same time, the system will prompt an error.</div>



1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**.

3. In the top navigation bar, select the target region.

4. Click **Acquisition plug\-in global operation \> Install/upgrade the capture plugin** above the ECS instance list.

5. In the dialog box, select **Only install Cloud as a Service without the Capture plugin installed**, then click **Confirm**.


<span id="8e12498e"></span>
## Upgrade the collection add\-on

You can also upgrade the collection add\-on for a single ECS instance or for multiple ECS instances with the collection add\-on installed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can execute only one upgrade task at the same time. If you execute multiple upgrade tasks at the same time, the system will prompt an error.</div>


<span id="db7872f4"></span>
### Upgrade the collection add\-on for a single ECS instance


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**.

3. In the top navigation bar, select the target region.

4. In the ECS instance list, find the target ECS instance with the collection add\-on installed and click **Upgrade the capture plug\-in** in the Actions column.

5. In the message that appears, click **Confirm** to upgrade the collection add\-on for the ECS instance.


<span id="be30c520"></span>
### Upgrade the collection add\-on for multiple ECS instances


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**.

3. In the top navigation bar, select the target region.

4. Click **Acquisition plug\-in global operation \> Install/upgrade the capture plugin** above the ECS instance list.

5. In the dialog box, select **Upgrade only Cloud as a Service with the Capture plugin installed**, then click **Confirm**.


<span id="adfb7c45"></span>
## Aborting the collection add\-on upgrade

Aborting the collection add\-on upgrade will cancel all add\-on upgrades that are not started. Completed or ongoing upgrades will not be rolled back or stopped.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation bar, click **Cloud Service Monitor**. On the page that appears, click **ECS**.

3. In the top navigation bar, select the target region.

4. Click **Acquisition plug\-in global operation \> Abort acquisition plug\-in upgrade** above the ECS instance list.

5. In the message that appears, view the prompt message and click **Confirm**.
