---
title: "Template syntax"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Template_syntax_overview"
---

Cloud Monitor supports custom notification templates, where you can define the structure and fields of alert notifications. This topic provides basic information about notification templates.

<span id="stYislaY"></span>
## Background

When an event matched by an alert policy or event rule is triggered, Cloud Monitor sends alert notifications or event notifications via email, Feishu, DingTalk, phone call, Webhook, or other channels. The system has preset notification templates for various notification methods. However, if the preset notification templates do not meet your requirements, you can create custom notification templates.

Notification templates use [Markdown syntax](https://open.feishu.cn/document/common-capabilities/message-card/message-cards-content/using-markdown-tags#abc9b025) and [Go Template syntax](https://pkg.go.dev/text/template) to write and render notification content. Before configuring a custom notification template, you need to first understand basic Go Template syntax.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the extension functions and variables mentioned in the Cloud Monitor notification templates in this topic, see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Extension_functions_and_variables">Extension functions and variables</a>.</div>


<span id="hddzX8e6"></span>
## Common Go template syntax

<span id="zazWTOkP"></span>
### Character `.`

The `.` character is used to render the specified object within the current scope.

Example 1: Obtain all contents within the top\-level scope, which are all contents in an alerting notification.

```bash
{{ . }}
```


The following sample code shows the expected response result: The output contains all content in the alert notification.

Example 2: Query the `Region` field of the alert policy.

```bash
{{ .Region }}
```


The following sample code shows the expected response result:

```bash
cn-beijing
```


<span id="NpzWEcXI"></span>
### Variable

Variables are used to store input data, and after data is passed into variables, the entire template can access the data by using the variables. For example, in `{{$rulename := .RuleName}}`, use `$rulename` as a variable to store the alert policy name, and then use `{{$rulename}}` to access the variable.

Example: Store the alert policy name in `$rulename` and then output `$rulename`.

```bash
{{ $rulename := .RuleName }} {{$rulename}}
```


The following sample code shows the expected response result:

```bash
This is an alert policy demo
```


<span id="GFBSvUhL"></span>
### Conditional statement

The conditional statement `if/else` uses `if` to check the data. If the condition is not met, the content of `else` is executed. The `if` statement returns `false` when the evaluation condition is a **null value**, **0**, **nil**, an **empty string**, or a **zero\-length string**.

Example: If the value of `.Level` in the alert information equals `warning`, the output is `Warning`.

```bash
{{if eq "warning" .Level }} Warning alert {{ end }}
```


The following sample code shows the expected response result:

```bash
Warning alert
```


<span id="nLzzTz20"></span>
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


Example: If the value of `.Level` is equal to `warning`, the output is `Warning`.

```bash
{{if eq "warning" .Level }} Warning alert {{ end }}
```


The following sample code shows the expected response result:

```bash
Warning alert
```


<span id="ruQxTwPJ"></span>
### Logical function

Logical functions primarily include `and`, `or`, and `not`, which are used to perform logical **negation**, **conjunction**, and **disjunction** across multiple conditions.

Example: If the value of `Region` is `cn-beijing` and the value of `Level` is `warning`, the output is `Warning level alert from Beijing`.

```bash
{{if eq "cn-beijing" .Region and eq "warning" .Level }} Beijing Warning Alert {{ end }}
```


The following sample code shows the response result:

```bash
Beijing Warning Alert
```


<span id="HLGPkqlq"></span>
### Common built\-in functions

The following table describes the common Go template built\-in functions.


|Function Name |Descriptions |Example |
|---|---|---|
|len |Obtains the length of an array. |Obtain the length of the Alerts array.<br><br>```bash```<br>```{{ len .Region }}```<br><br><br>The following section shows the expected response result:<br><br>```bash```<br>```10```<br> |


<span id="7Aozdr6Y"></span>
## Related document


* [Extension functions and variables](https://docs.byteplus.com/en/docs/cloudmonitor/Extension_functions_and_variables)

* [Creating notification templates](https://docs.byteplus.com/en/docs/cloudmonitor/Creating_a_notification_template)
