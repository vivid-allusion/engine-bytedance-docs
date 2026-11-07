---
title: "Creating a notification template"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/lark-alerting-notifacation-template"
---

Vital Managed Service for Prometheus (VMP) allows you to configure custom notification templates. You can specify the structure and fields of alert notifications in notification templates. This topic describes how to create a notification template.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The new Alert Center is available. It provides comprehensive upgrades and optimizations for features such as notification policies, notification templates, aggregation policies, and suppression policies. We recommend configuring notification templates in the new <a href="https://console.byteplus.com/observe/alert/notify/rules">Alert Center</a>.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

When an alert that matches an alert rule is triggered, VMP sends alert notifications by email, Feishu, DingTalk, phone, and webhook. The system has preset notification templates for various notification methods, but if the preset notification templates cannot meet your business requirements, you can configure custom notification templates.

Notification templates allow you to use [Markdown syntax](https://open.feishu.cn/document/common-capabilities/message-card/message-cards-content/using-markdown-tags#abc9b025) and [Go template syntax](https://pkg.go.dev/text/template) to write and render notifications. Before you configure a custom notification template, you need to understand the common Go template syntax.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For variable parameters and sample responses of VMP alerts mentioned in this topic, refer to <a href="https://docs.byteplus.com/en/docs/vmp/variable-structure-and-parameters">Variable structure and parameters</a>.</div>


<span id="98e8b7b1"></span>
## Limits

Up to 100 notification templates can be created within a root user and its Identity and Access Management (IAM) users.

<span id=".Z28tdGVtcGxhdGUt5bi455So6K-t5rOV"></span>
## Common Go template syntax

<span id=".5a2X56ym"></span>
### Character `.`

The `.` character is used to render the specified object within the current scope.

Example 1: Obtain all contents within the top\-level scope, which are all contents in an alert notification.

```bash
{{ . }}
```


The following sample code shows the expected response result: All contents in the alert notification are the output.

Example 2: Obtain the `Region` field in an alert notification.

```bash
{{ .Region }}
```


The following sample code shows the expected response result:

```bash
cn-beijing
```


<span id=".5Y-Y6YeP"></span>
### Variable

Variables are used to store input data, and after data is passed into variables, the entire template can access the data by using the variables. For example, if you use `$alert` as a variable in `{$alert := .Alerts}` to save all contents in an alert notification, you can use `{{$alert}}` to access the variable.

Example: Save the name of an alert rule in `$alertrulename`, and then output `$alertrulename`.

```bash
{{ $alertrulename := .AlertingRuleName }} {{$alertrulename}}
```


The following sample code shows the expected response result:

```bash
CPU utilization exceeds 80%
```


<span id=".5Yik5pat6K-t5Y-l"></span>
### Conditional statement

The conditional statement `if/else` uses `if` to check the data. If the condition is not met, the content of `else` is executed. The `if` statement returns `false` when the evaluation condition is a **null value**, **0**, **nil**, an **empty string**, or a **zero\-length string**.

Example: If the `.Level` value in an alert notification is `P0`, `P0 Alert` is the output.

```bash
{{if eq "P0" .Level }} P0 alert {{ end }}
```


The following sample code shows the expected response result:

```bash
P0 alert
```


<span id=".5q-U6L6D5Ye95pWw"></span>
### Comparison function

The comparison function is used to compare the data size. It is often used together with `if/else` statements to determine the execution of statements. The following table shows commonly used comparison functions.


|Function Name |Descriptions |
|---|---|
|`eq` |Equal to |
|`ne` |Not equal to |
|`lt` |Less than |
|`le` |Less than or equal to |
|`gt` |Greater than |
|`ge` |Greater than or equal to |


Example: If the value of `.Level` is equal to `P0`, `P0 Alert` is the output.

```bash
{{if eq "P0" .Level }} P0 alert {{ end }}
```


The following sample code shows the expected response result:

```bash
P0 alert
```


<span id=".6YC76L6R5Ye95pWw"></span>
### Logical function

Logical functions primarily include `and`, `or`, and `not`, which are used to perform logical **negation**, **conjunction**, and **disjunction** across multiple conditions.

Example: If the value of `Region` is `cn-beijing` and the value of `Level` is `P0`, `Beijing P0 alert` is the output.

```bash
{{if eq "cn-beijing" .Region and eq "P0" .Level }} beijing PO alert {{ end }}
```


The following sample code shows the response result:

```bash
beijing PO alert
```


<span id=".5bi455So5YaF572u5Ye95pWw"></span>
### Common built\-in functions

The following table describes the common Go template built\-in functions.


|Function Name |Descriptions |Example |
|---|---|---|
|len |Obtains the length of an array. |Obtain the length of the Alerts array.<br><br>```bash```<br>```{{ len .Alerts }}```<br><br><br>The following section shows the expected response result:<br><br>```bash```<br>```9```<br> |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* You cannot configure the background colors of titles in notifications, which are automatically specified by the system. Red indicates that an alert is triggered, and green indicates that an alert is cleared.

* You cannot configure the buttons in notifications. The **View details** button is fixed for redirecting to the alert list.

* The title and content of a notification can be up to 16,000 bytes in length in UTF\-8 encoding. If the upper limit is exceeded, the alert notification will be truncated.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [VMP console](https://console.byteplus.com/observe/prometheus).

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Alert Center \> Notification message template**. On the page that appears, click **Create message template**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5b668dbc89b8dba7ada5f92536d3cff.png) </span>

4. Click the **Alerting notification** or **Alerting restoration notification** tab, and specify the parameters of the template.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_abb2a654680826aa41ce0405cd2ab704.png) </span>

   
   |Parameter |Descriptions |
   |---|---|
   |Template type |Select the type of notification template. Supported types include **Email**, **Feishu bot**, **Feishu application bot**, **DingTalk bot, WeCom bot**, and **SMS**. |
   |Template name |Specify the name of the notification template. The name must be unique in a region. |
   |Template description |Specify the description of the notification template. The description can be up to 128 characters in length. |
   |Template configuration |You can configure **alerting notification** and **alert restoration notification** templates by using Markdown syntax and Go template syntax, including the title and content of the notification.<br><br><br>* **Title**: Configure the title of the alert notification. It can contain any UTF\-8 characters.<br><br>* **Content**: Configure the alert notification content. It can contain any UTF\-8 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For the detailed explanation of the preset template, refer to the <a href="https://docs.byteplus.com/en/docs/vmp/lark-alerting-notifacation-template#.5qih5p2_56S65L6L6K-05piO">Template example description</a> section of this topic.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you want to specify custom structure and fields of the template, refer to <a href="https://docs.byteplus.com/en/docs/vmp/variable-structure-and-parameters">Extension functions and variables</a>.</div><br> |
   

5. (Optional) Click **Reset** to restore the template content to the default settings.

6. Click **Submit** to complete the configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After you create a custom Feishu notification template, you can reference this template in an alert notification policy. For details, see [Creating alert notification policies](https://docs.byteplus.com/en/docs/vmp/Creating-alerting-notification-rules).

<span id=".5qih5p2_56S65L6L6K-05piO"></span>
## Template example description

In the notification template console, a sample Feishu notification template is preset for you, which consists of a **title** and **content**. This section uses the preset **alerting notification** template as an example to introduce the parameters and meanings of the sample template.

<span id=".5qCH6aKY6K-05piO"></span>
### Title description

The following sample code shows the title of the sample template:

```markdown
{{ .Region }} Active alerts
```


In the title of the sample template, the `Region` field is used to obtain information about the region where an alert is triggered, and fill the region information in the alert title.

<span id=".5YaF5a656K-05piO"></span>
### Content description

The content of the sample template consists of **alert overview** and **failed resource details**.


* **Alert overview**: displays the alert rule (including link), alert level, alert conditions, and duration. It is implemented by the following code:

   ```markdown
   **🔴Alert Rule**: [{{ .AlertingRuleName }}]({{ .AlertingRuleDetailURL }})
   **🚨Alert Level**: {{ .Level }}
   **🚦Alert Condition**: {{ .PromQL }} {{ .Comparator }} {{ .Threshold }} [ Duration {{ .For }} ]
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In Markdown syntax:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Add <code>**</code> before and after a sentence to indicate that the sentence is in bold format.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>[]()</code> indicates a link, where <code>[]</code> contains the link text and <code>()</code> contains the URL.   </div>
   

* **Failed resource details**: displays the alert details of each failed resource. It is implemented by the following code:

   ```markdown
   {{- $alertCount := len .Alerts }}
   {{- $maxAlerts := 10 }}
   **Fault Resource Details ({{ $alertCount }})**:
   {{- range $idx, $alert := .Alerts }}
     {{- if lt $idx 10 }}
       {{- $labels := "" -}}
       {{- range $k, $v := $alert.Labels }}
         {{- $labels = print $labels $k "=" "\"**" $v "**\"" " " -}}
       {{- end }}
       [{{ $alert.Id }}]({{ $alert.DetailURL }}){{ "{" }} {{ $labels }}{{ "}" }}
         Current Value: {{ $alert.Value }}
         Start Time: {{ $alert.StartsAt.Format "2006-01-02 15:04:05" }}
         
     {{- end }}
   {{- end }}
   
   ---
   
   {{- if gt $alertCount $maxAlerts }}
   **The number of resources exceeds {{ $maxAlerts }}. Go to the console to view the full alerts.**
   {{- end }}
   ```
   

   
   |Template content |Descriptions |
   |---|---|
   |```markdown```<br>```{{- $alertCount := len .Alerts }}```<br>```{{- $maxAlerts := 10 }}```<br> |Specify the `$alertCount` and `$maxAlerts` variables.<br><br><br>* `$alertCount`: The number of failed resources in the alert notification obtained through the `len` function.<br><br>* `$maxAlerts`: The maximum number of resources to display. The default value is 10, which indicates that the details of up to 10 failed resources can be displayed. |
   |```markdown```<br>```**Fault Resource Details ({{ $alertCount }} 个)**:```<br>```{{- range $idx, $alert := .Alerts }}```<br>```  {{- if lt $idx 10 }}```<br>```    {{- $labels := "" -}}```<br>```    {{- range $k, $v := $alert.Labels }}```<br>```      {{- $labels = print $labels $k "=" "\"**" $v "**\"" " " -}}```<br>```    {{- end }}```<br>```    [{{ $alert.Id }}]({{ $alert.DetailURL }}){{ "{" }} {{ $labels }}{{ "}" }}```<br>```      Current Value: {{ $alert.Value }}```<br>```      Start Time: {{ $alert.StartsAt.Format "2006-01-02 15:04:05" }}```<br>```  {{- end }}```<br>```{{- end }}```<br> |When the number of failed resources is less than the value of the `$maxAlerts` parameter (default value: 10), the details of all failed resources are recursively displayed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The details of failed resources are obtained by the <code>.Alerts.Labels</code> field. For parameter meanings and data structure, refer to <a href="https://docs.byteplus.com/en/docs/vmp/variable-structure-and-parameters">Variable structure and parameters</a>. The labels may vary based on different resources.</div><br> |
   |```markdown```<br>```{{- if gt $alertCount $maxAlerts }}```<br>```**The number of resources exceeds {{ $maxAlerts }} ，Jump to console for full alerts**```<br>```{{- end }}```<br> |When the number of failed resources exceeds the value of `$maxAlerts` (10 by default), resource details are not displayed. You are prompted to go to the console for full details. |
   


<span id=".5raI5oGv56S65L6L"></span>
### Message example

The following figure shows the actual result when you use a custom template.
