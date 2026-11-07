---
title: "Global variables"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Global_variables"
---

When configuring data queries or query variables, you can use global variables for interpolation. This topic describes how to use global variables.

<span id="4MEO4fBU"></span>
## Create global variables


1. Log in to the [Observability Platform ](https://console.byteplus.com/observe/dashboard/dashboard)console, and in the left navigation bar, select **Custom Dashboard**.

2. On the dashboard management page, click the name of the target dashboard to go to the dashboard details page.

3. Click the **edit** button, then click **settings**, and select the **global variable** tab.

4. Click **Add Variable** to add global variables based on your requirements. Currently, three types of variables are supported: Query, Custom, and Textbox.



|Variable type |Description |
|---|---|
|Query variable |Query variables enable dynamic retrieval of variable values via data source API queries. You can also apply regular expressions to process variable values.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, Query variables support variable queries from VMP and Cloud Monitor data sources.</div><br> |
|Custom variable |Custom variables support custom variable lists. When you enter multiple variables, separate them with commas. |
|Text box variable |Provides a text input box for the variable. Any character can be entered. |


<span id="ap8XM8cg"></span>
## Use global variables

In data query or query variable configuration, variable interpolation is supported via`$variable_name`. For example, `$Variable1` will be replaced with the currently selected value of the `Variable1` variable. Example:

<span id="AKqk7Pvt"></span>
## Manage global variables

You can perform the following lifecycle management operations on global variables:


|Actions |Description |
|---|---|
|Copy |Copy a new variable based on an existing global variable. |
|Delete |Delete global variables that you no longer use.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Global variables cannot be restored after deletion. Proceed with caution.</div><br> |


&nbsp;
