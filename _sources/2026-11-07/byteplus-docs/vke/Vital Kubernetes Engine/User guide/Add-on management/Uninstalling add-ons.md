---
title: "Uninstalling add-ons"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Uninstalling-an-add-on"
---

This topic mainly describes how to uninstall add\-ons that you no longer use. When you uninstall some add\-ons, you can optionally delete the custom resource definition (CRD) resources at the same time.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An add\-on has been installed. For instructions, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you uninstall the add\-on, some features of the cluster may become unavailable. Proceed with caution.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the cluster that you need to configure.

3. On the cluster management page, click **Addons** in the left navigation bar.

4. Find the add\-on that you want to uninstall and click `...` \> **Uninstall**.

5. You need to perform a secondary confirmation when you uninstall an add\-on. For some add\-ons, an option is provided to delete CRD resources at the same time.

6. Click **Uninstall** to uninstall the add\-on.
