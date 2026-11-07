---
title: "Preset alerting rule templates"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Predefined-alerting-rule-templates"
---

Vital Managed Service for Prometheus (VMP) provides preset alert rule templates for commonly used cloud services. This topic describes how to view and use the preset alerting rule templates.

<span id=".5p-l55yL5qih5p2_"></span>
## View a template


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. On the left navigation bar, click **Alert center \> Alerting rule template**. Click the **Preset template** tab.

4. On the **Preset template** tab, click a service name to view the preset alerting rule templates of the service. The tab displays information such as the template name, ID, version, description, number of associated alerting rule groups, and time.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_991e372b0ab5c700249f42e3b115606e.png) </span>

<span id=".5bqU55So5qih5p2_"></span>
## Apply a template

On the **Preset template** tab, find the target template and click **Apply template** in the **Actions** column to create an alerting rule group based on the template.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_21ca5a12d7c4df1dedc084103ea1961d.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed configuration of the alerting rule group, refer to <a href="https://docs.byteplus.com/en/docs/vmp/Creating-alerting-rule-groups">Creating an alerting rule group</a>.</div>


<span id=".5a-85Ye65qih5p2_"></span>
## Export a template

On the **Preset template** tab, find the target template and click **Export** in the **Actions** column to export the YAML configuration file of the template. You can modify the parameters in the configuration file in your local environment and create a custom alerting rule template based on the modified configuration file. For more details, refer to [Creating a custom alerting rule template](https://docs.byteplus.com/en/docs/vmp/Customizing-alerting-rule-templates).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_58fb04272bfbc46e5fe0a5b0f4bfb02e.png) </span>

&nbsp;
