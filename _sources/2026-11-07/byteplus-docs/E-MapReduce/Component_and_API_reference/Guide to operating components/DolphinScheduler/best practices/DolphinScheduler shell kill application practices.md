---
title: "DolphinScheduler shell kill application practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/DolphinScheduler_shell_kill_application_practices"
---

When using the DolphinScheduler service on Volcano Engine EMR, the optimized shell kill capability is currently supported. This document introduces the application practices for DolphinScheduler shell kill.

<span id="ef22cb23"></span>
# Caution

When using the optimized shell kill capability on Volcano Engine EMR, you need to ensure the following:


* The DolphinScheduler version is 3.1.9.


<span id="f7eacce0"></span>
# Feature updates

Supports configuring the optimized shell kill capability through global or job\-level parameters. The configuration file is `common.properties`. The relevant global and job\-level parameters are as follows.

<span id="33bbdb87"></span>
## shell.kill.enhance.enabled

<span id="2d396067"></span>
### Note


|Parameter name |Parameter meaning |Scope of effectiveness |
|---|---|---|
|`shell.kill.enhance.enabled` |Whether to enable the optimized shell kill capability. The default is false. |* Supports configuration at both global and job levels.<br><br>* Job\-level configuration takes precedence over global configuration. For more details on the logic of parameter effectiveness, see the table below. |


The logic details for the effectiveness of parameter settings are as follows.


|Global configuration |Job configuration |Effective |
|---|---|---|
|true |true |true |
|true |false |false |
|true |/ |true |
|false |true |true |
|false |false |false |
|false |/ |false |
|/ |true |true |
|/ |false |false |
|/ |/ |false |


<span id="271586d3"></span>
### Configuration example


|Global configuration |Job configuration |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd5c9b0d22524b3e89b8dd23321aaccf~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/684dd2e5573a4055a6f82789c542ce9e~tplv-goo7wpa0wc-image.image) </span> |


<span id="006d708e"></span>
## shell.kill.wait.timeout

<span id="d5d39c6f"></span>
### Note


|Parameter name |Parameter meaning |Scope of effectiveness |
|---|---|---|
|`shell.kill.wait.timeout` |The waiting time after each shell kill signal is sent. The default is 10s. |* Supports global configuration.<br><br>* Depends on `shell.kill.enhance.enabled=true`. |


<span id="b1d65576"></span>
### Configuration example

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f5995d118124feea6743b1790d328a8~tplv-goo7wpa0wc-image.image) </span>

<span id="62194c53"></span>
# Upgrade for existing nodes

Starting from EMR software stack version 3.20.0, this feature is supported by default. For existing deployments, it is recommended to upgrade to version 3.17.0 or above. The procedure is as follows.


1. For existing nodes, update the dependency package at the following path: `dolphinscheduler-task-api-3.1.9.jar`.

   * You can click the attachment link below to download the new dependency package.

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98a5cfca1a81446aa9a527bdd2ce615f~tplv-goo7wpa0wc-image.image" name="dolphinscheduler-task-api-3.1.9.jar">dolphinscheduler-task-api-3.1.9.jar</Attachment>
      

   * Update the new dependency package to the following relevant paths.

      * master\-server dependency path

         ```Shell
         /usr/lib/emr/current/dolphin_scheduler/master-server/libs
         ```
         

      * api\-server dependency path

         ```Shell
         /usr/lib/emr/current/dolphin_scheduler/api-server/libs
         ```
         

      * alert\-server dependency path

         ```Shell
         /usr/lib/emr/current/dolphin_scheduler/alert-server/libs
         ```
         

      * worker\-server dependency path

         ```Shell
         /usr/lib/emr/current/dolphin_scheduler/worker-server/libs
         ```
         

2. After replacing the dependency package, restart the service to make the new dependency package take effect.
