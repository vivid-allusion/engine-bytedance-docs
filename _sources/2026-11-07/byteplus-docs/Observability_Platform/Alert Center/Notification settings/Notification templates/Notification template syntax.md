---
title: "Notification template syntax"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Notification_template_syntax"
---

When a matched rule in a notification policy or event is triggered, a notification message is sent via email, Feishu, DingTalk, phone, Webhook, and other methods based on the content defined in the notification template. The system provides a preset notification title and content for each notification type by default. If the preset templates do not meet your requirements, you can customize a notification template based on your actual scenario. This topic describes the syntax supported for writing notification templates.

<span id="VQi75hfB"></span>
## Background

The notification title and content in a notification template are written and rendered using [Markdown](https://open.feishu.cn/document/common-capabilities/message-card/message-cards-content/using-markdown-tags#abc9b025) and [Go Template](https://pkg.go.dev/text/template) syntax. Before configuring a custom notification template, you need to first understand basic Go Template syntax.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The template writing syntax is universal, but the supported extension functions and variables vary by notification type. For more information, see:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables_for_Cloud_Monitor">Extension functions and variables for Cloud Monitor and cloud service events</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables_for_VMP">Extension functions and variables for VMP</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/Observability_Platform/Extension_functions_and_variables_for_Server-side_Monitoring">Extension functions and variables for Server\-side Monitoring</a></div>



<span id="NpfsC2nn"></span>
## Common Go template syntax

<span id="3ZbqFTtQ"></span>
### Character `.`

The `.` character is used to render the specified object within the current scope.

Example 1: Obtain all contents within the top\-level scope, which are all contents in an alerting notification.

```bash
{{ . }}
```


Expected response result: The output contains all content in the alert notification.

Example 2: Query the `Region` field of the alert policy.

```bash
{{ .Region }}
```


The following sample code shows the expected response result:

```bash
cn-beijing
```


<span id="QQuheN6W"></span>
### Variable

Variables are used to store input data, and after data is passed into variables, the entire template can access the data by using the variables. For example, in `{{$rulename := .RuleName}}`, use `$rulename` as a variable to store the alert policy name, and then use `{{$rulename}}` to access the variable.

Example: Store the alert policy name in `$rulename` and then output `$rulename`.

```bash
{{ $rulename := .RuleName }} {{$rulename}}
```


The following sample code shows the expected response result:

```bash
This is a alarm strategy demo
```


<span id="sKQjJwTV"></span>
### Conditional statement

The conditional statement `if/else` uses `if` to check the data. If the condition is not met, the content of `else` is executed. The `if` statement returns `false` when the evaluation condition is a **null value**, **0**, **nil**, an **empty string**, or a **zero\-length string**.

Example: If the value of `.Level` in the alert information equals `warning`, the output is `Warning`.

```bash
{{if eq "warning" .Level }} Warning alarm {{ end }}
```


The following sample code shows the expected response result:

```bash
Warning alarm
```


<span id="dnA55lXU"></span>
### Comparison function

The comparison function is used to compare the data size. It is often used together with `if/else` statements to determine the execution of statements. The following table shows commonly used comparison functions.


|Function name |Description |
|---|---|
|`eq` |Equal to |
|`ne` |Not equal to |
|`lt` |Less than |
|`le` |Less than or equal to |
|`gt` |Greater than |
|`ge` |Greater than or equal to |


Example: If the value of `.Level` is equal to `warning`, the output is `Warning`.

```bash
{{if eq "warning" .Level }} Warning alarm {{ end }}
```


The following sample code shows the expected response result:

```bash
Warning alarm
```


<span id="y6J7PswX"></span>
### Logical function

Logical functions primarily include `and`, `or`, and `not`, which are used to perform logical **negation**, **conjunction**, and **disjunction** across multiple conditions.

Example: If the value of `Region` is `cn-beijing` and the value of `Level` is `warning`, the output is `Warning level alert from Beijing`.

```bash
{{if eq "cn-beijing" .Region and eq "warning" .Level }} Beijing Warning Alarm {{ end }}
```


The following sample code shows the response result:

```bash
Beijing Warning Alarm
```


<span id="hP2xXAiZ"></span>
### Common built\-in functions

The following table describes the common Go template built\-in functions.


|Function name |Description |Example |
|---|---|---|
|len |Obtains the length of an array. |Obtain the length of the Alerts array.<br><br>```bash```<br>```{{ len .Region }}```<br><br><br>The following section shows the expected response result:<br><br>```bash```<br>```10```<br> |
