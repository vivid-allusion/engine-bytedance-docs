---
title: "Configure extension files"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Configuring_extension_files"
---

When you need to define driver files in the Logstash configuration files for Cloud Search, you can use the extension file configuration feature to upload the required driver files. The extension file configuration feature also provides management capabilities for all extension files. This topic describes how to configure extension files.

<span id="rScqkOsm"></span>
## Prerequisites

Created Logstash instance. For detailed operations, see [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

<span id="sxVvbf5b"></span>
## Add extension files


1. Log in to the[Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation, select **Data processing** \> **Logstash**.

3. In the Logstash instances list, click the target instance's name to enter the **Basic information** tab.

4. Select the **Instance configuration** tab on the left, then choose the **Extension file configuration** sub\-tab.

5. In the **Extension file configuration** sub\-tab, click **Add file**.

6. In the **Add file** panel, select the driver file to add, then click **OK**.


<span id="XNZyZeQJ"></span>
## Remove extension file

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Removing extension files may cause dependent pipelines to run with exceptions. Only proceed if it does not affect business operations.</div>



1. Log in to the[Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation pane, select **Data processing** \> **Logstash**.

3. In the Logstash instances list, click the target instance's name to enter the **Basic information** tab.

4. Select the **Instance configuration** tab on the left, then choose the **Extension file configuration** sub\-tab.

5. In the **Extended file configuration** tab, locate the extended file to remove, click **Remove** in the Actions column, or select multiple extended files to remove, then click **Batch remove**.

6. In the popup dialog, click **OK**.
