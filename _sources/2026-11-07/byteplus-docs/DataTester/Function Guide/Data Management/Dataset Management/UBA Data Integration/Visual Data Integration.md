---
title: "Visual Data Integration"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Visual-Data-Integration"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function is supported by versions above V4.2.2 (inclusive). If you need to use it, you need to contact your customer success manager separately to activate it.</div>


<span id="一、概述"></span>
# 1. Overview

In the enterprise, data collection has used other manufacturers of event tracking systems, do not want to repeat the construction of event tracking systems. I hope DataTester can provide data integration program, the historical data assets directly reused. In order to support the requirements of Data Integration, DataTester uses a visual Data Integration to support Kafka subscriptions, and reports UBA data from other plants to Volcano DataTester Data Service by creating and executing Data Integration tasks.


* Create Data Integration Task

   * Connect to data sources by entering information such as Kafka server, topic, etc

   * Parse the metadata in the connected data source, and support customers to perform data field mapping through data mapping configuration

   * Support customers to configure task configuration time/cycle, etc

   * Support customers to set task alarms for tasks

* task operation and maintenance

   * Start/stop the task through the task switch in the task list

   * The execution results of data tasks can be viewed through the task log

   * Task details & emails can view single alarm details


<span id="二、数据集成流程示例"></span>
# 2. Data Integration Process


* Process example: A vendor Kafka\-UBA data access DataTester


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dca51a4f43144a6390c5968e9f85f8be~tplv-goo7wpa0wc-image.image) </span>

<span id="三、与客户平台交互方式说明"></span>
# Description of interaction pattern with customer platform

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ceff85903394d9c932865838e248cb6~tplv-goo7wpa0wc-image.image) </span>

<span id="四、功能介绍"></span>
# 4. Function introduction

<span id="_4-1-创建集成任务"></span>
## 4.1 Create an integration task

DataTester provides two ways to perform Data Integration, namely visual configuration and custom upload configuration. The two methods bring the same effect, and you can choose one of the two (but if there is a function plug\-in appeal: V4.4.0 version needs to use custom configuration upload implementation)

<span id="_4-1-1-可视化配置数据集成"></span>
### 4.1.1 Visually configure Data Integration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd4399d8e0e8450dbad743ca62debd8b~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-基本信息"></span>
#### 1. Basic information


* Create a new Data Integration task, you need to define the basic information of the Data Integration task.

* Select the type of data source to be synchronized: UBA data, user properties.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dc2b5ac3a704e78a0c83b574a55886e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-数据源连接"></span>
#### 2. Data source connection


* When creating a new Data Integration task, you need to enter the consumer group name of the third party/customer that provides the data source, the address of the Kafka server, and the name of the Kafka Topic to test the connection of the data source.

* Clicking Connect Test will try to connect the topic and read the latest data stuffing example.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24f7d8ecb49f446d87d3c7841f148100~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-元数据映射"></span>
#### 3. Metadata mapping


* Data source data field mapping to Tester system field

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48ee3fdba8474ebeb25eaea556dd93e6~tplv-goo7wpa0wc-image.image) </span>


<span id="_4-任务配置"></span>
#### 4. Task configuration


* Support customers to configure task configuration time/cycle, etc

> Kafka tasks do not support timed repetitive commits.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce0b937c42ce4feebb125b319ad6d863~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-配置监控告警"></span>
#### 5. Configure monitoring alarms


* Support customers to add alarm policies to set alarm rules, and receive reminders in emails or view task details after triggering alarms.


<span id="_4-1-2上传配置数据集成"></span>
### 4.1.2 Custom Configuration Data Integration

<span id="_1-自定义配置集成任务"></span>
#### 1. Custom configuration integration tasks


* Select a custom configuration integration task

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3009683813ce4491a9aa350fdd37e933~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-创建集成任务"></span>
#### 2. Create an integration task


* Upload configuration

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33f9f389dc4746dc8412ffc35018e058~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-配置模版"></span>
#### 3. Profile

For the specific file format, please refer to the custom configuration integration.

<span id="_4-2-任务运维"></span>
## 4.2 Task operation and maintenance

<span id="_4-2-1-任务列表"></span>
### 4.2.1 Task list


* Task list

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c4b32fba6e441ee86ba1adf43ab2508~tplv-goo7wpa0wc-image.image) </span>

* Task detail

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/802a2f36dbbe4999989a5562c1ab5742~tplv-goo7wpa0wc-image.image) </span>


<span id="_4-2-2-查看监控告警"></span>
### 4.2.2 View surveillance alerts


* Alarm viewing form (1) You can view the details of the alarm in the task details module

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc18e47eb6744022ae7f341ad558bc30~tplv-goo7wpa0wc-image.image) </span>

* Alarm viewing form (2) Select to receive the alarm email when creating the alarm, and the alarm email will be received after the alarm is triggered.


<span id="_4-3-数据应用"></span>
## 4.3 Application of data

The user behavior data synchronized through the Data Integration can be viewed on the Datatester background [Data Management] page, and event metrics can be created using this part of the event, as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4773e816746e4ce285f31f9fe4bb628c~tplv-goo7wpa0wc-image.image) </span>

<span id="a7307aed"></span>
## 4.4 The integration task failed abnormally and restarted.

> Only versions 4.7 and above support failed restarts.


After the creation of the Shenze and Kafka Data Integration tasks is completed, the fixed delay restart strategy of Flink jobs is configured by default. The maximum restart attempt can be 10 times, and the delay time between the two restarts is 300 seconds. After the task is successfully restarted, the task details output data and failure data monitoring will be cleared.

Check the env default configuration through the download configuration as follows parameters.

```Shell
env {
    execution.restart.attempts = "10"
    execution.restart.delayBetweenAttempts = "300000"
    execution.restart.strategy = "fixed-delay"
}
```


Custom Data Integration tasks can manually add the above failure restart policies in the configuration file env, and can also customize parameter values.
