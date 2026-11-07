---
title: "Alert Task"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Alert-Task"
---

<span id="一-概述"></span>
# 1. Overview

After the release of Features and Experiments, it is equivalent to releasing a new version, even a low\-traffic test, which means that it may have an impact on online business. This module provides the ability to monitor the alarm, allowing for the monitoring of functions after the launch. When business indicators or technical indicators change, the alarm task will reach the corresponding person in charge in a timely manner.

<span id="二-创建报警"></span>
# 2. Create an alarm

<span id="_1-新建报警任务"></span>
## 1. **New alarm task**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3ff019fd8bf40de9b9655d867378b43~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-选择报警类型"></span>
## 2. **Select alarm type**

There are two types of alarms in total: large\-scale alarms and experimental alarms


* Large market alarm: The system will trigger an alarm according to the overall large market data

* Experimental alarm: The system will integrate all the experimental related data under a combination to count indicators and provide targeted alarms


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f99c7b11f40349ca83b66905a10c1b06~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-报警任务-基本配置"></span>
## 3. **Alarm task \- basic configuration**


* Basic information: fill in the task name, task description, etc

* Alarm level: You can choose the corresponding alarm level (attention, warning, critical).

* Task interval: 1 hour, 24 hours, the calculation of the alarm strategy will be completed every selected interval to determine whether to alarm

* Associated scenario: Corresponds to the selected alarm scenario


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b63642774f07449096d9131940aa3c77~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-报警任务-设置报警策略"></span>
## 4. Alarm Task \- Set Alarm Policy


|configuration parameters |Large disk alarm configuration instructions |Experimental alarm configuration instructions |
|---|---|---|
|interface example |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc539a55d6da4a30bda57a2d1748e423~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ccc41baff4d4650a04fe785bbfda60c~tplv-goo7wpa0wc-image.image) </span> |
|Alarm rules |Select the alarm rule:<br><br><br>* **At the same time, the following rules are met**: it means that the alarm will only be triggered if all alarm policies are met.<br><br>* **Meet the following rule**: represents as long as one of the alarm policies triggers an alarm. ||
|Alarm strategy |* Indicator Name: Select the indicator to be monitored.<br><br>* Alarm strategy: support absolute value, year\-on\-year, month\-on\-month alarm strategy.<br><br>* It supports adding multiple alarm policies, and the influence of multiple alarm policies on the final alarm triggering is determined by the configuration results of the above alarm rules. |* Indicator Name: Select the indicator to be monitored.<br><br>* Alarm strategy: Only alarm strategies that compare control groups are supported.<br><br>   * You need to configure the percentage change value of the metric against the control group based on your business monitoring needs.<br><br>   * Support check the alarm when the change is significant. After checking, only the concept of statistically significant data changes will trigger the alarm.<br><br>* It supports adding multiple alarm policies, and the influence of multiple alarm policies on the final alarm triggering is determined by the configuration results of the above alarm rules. |


<span id="_5-报警任务-通知方式配置"></span>
## 5. Alarm task \- notification method configuration

Alarm method: Lark, DingTalk, WeCom, email


* [Lark: ](https://www.feishu.cn/hc/zh-CN/articles/360024984973)Enter the Lark group, open the session settings, find the swarm robot, and click Add Robot. Select, customize the robot, join the group.

* [WeCom: ](https://work.weixin.qq.com/api/doc/90000/90136/91770)Enter the WeChat group chat, open the session settings, find the group robot, and click Add in the upper right corner, select Robot, Add to Group Chat.

* [DingTalk: ](https://developers.dingtalk.com/document/robots/custom-robot-access)Open the robot management page. Take the PC side as an example, open DingTalk on the PC side, click on the avatar, and select Robot Management. Select Custom Robot on the Robot Management page. When configuring security settings, select a custom keyword and fill in the alarm as a keyword, otherwise the alarm information may be lost.

* After completing the robot configuration, copy the corresponding WebHook address into the corresponding text box, and save this address properly to avoid being maliciously called to send spam messages after the address is leaked


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99b15bc1da304b559d4277ea134f608d~tplv-goo7wpa0wc-image.image) </span>

<span id="三-报警任务管理"></span>
# 3. Alarm task management

Click on the task name to enter the task details and modify it.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/237aa09687964a18a95b8b56ccba7d3f~tplv-goo7wpa0wc-image.image) </span>

<span id="四-接收组管理"></span>
# 4. Receiving group management

In the receiving group, you can create, edit, and delete receiving groups

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abe5dfb119f04294a07dd9d90329a570~tplv-goo7wpa0wc-image.image) </span>
