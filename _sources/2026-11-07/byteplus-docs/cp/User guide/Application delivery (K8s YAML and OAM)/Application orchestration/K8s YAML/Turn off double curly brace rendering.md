---
title: "Turn off double curly brace rendering"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Turn_off_double_curly_brace_rendering"
---

Application orchestration supports flexibly enabling or disabling the rendering of double curly braces `{{}}`, allowing you to control the actual value of variables in YAML files in specific scenarios to meet different business and configuration requirements.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

When the user turns on the **turn off rendering** switch, all expressions enclosed in double curly braces `{{}}` in the specified YAML file will not be rendered, but will instead be displayed as plain code.

For example, when default rendering is enabled, `{{.Values.namespace}}` represents the specified namespace. After turning off rendering, you need to replace the placeholder with a specific namespace name, for example, `namespace-a`.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

When **rendering** is turned off, if you need to use the actual value of these variables (including all types of system preset variables), you must manually substitute them with the specific values you require. For example,


* `{{.AppDeliver.appName}} - {{.AppDeliver.envName}}`: Indicates the combination of application name and environment name.

* `{{.Values.namespace}}`: Used to represent a namespace.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the current application.

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter it.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

   5. In application management, select **K8s YAML**.

   6. Click the target application card to open the application.

2. Click **Application Orchestration**, and switch to the Application Orchestration tab.

3. Click **edit** to enter the application orchestration page.

4. Click **turn off rendering** to complete the operation.
