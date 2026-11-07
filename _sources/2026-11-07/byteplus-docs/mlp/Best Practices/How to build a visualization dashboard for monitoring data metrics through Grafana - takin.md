---
title: "How to build a visualization dashboard for monitoring data metrics through Grafana - taking configuring the total GPU resources dashboard as an example"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/grafana"
---

<span id="前言"></span>
# Preface

This document takes creating a total GPU resources dashboard as an example to introduce the best practices for MLP to visually display monitoring data metrics through Grafana

> Some official documentation for reference:

> * Prometheus Monitoring \- [Monitoring--Machine Learning Platform-Byteplus](https://docs.byteplus.com/en/docs/mlp/Monitoring_configuration_instructions)

> * Deploy Grafana \- [Deploy Grafana in a container service cluster and connect to the workspace--Managed Prometheus-Byteplus](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster)


<span id="步骤一：新建dashboard"></span>
# Step 1: Create a new Dashboard


1. Obtain administrator permissions and create a new folder to manage dashboards


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_702399bd38fb799b58c2d26404265a80.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec0d8bf3d1fb7d5baba85594e7212d4f.png) </span>


2. Create a Dashboard and visualization dashboard in the folder


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dcb205ee4286ee2b5279d8d054afa191.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81d68d0cd3b6e7a3fec879788d7169ab.png) </span>

<span id="步骤二：配置资源组、队列、实例等筛选选项"></span>
# Step 2: Configure filter options such as resource groups, queues, and instances

<span id="_2-1-新增筛选变量"></span>
## 2.1 Add new filter variable


1. Click dashboard settings, navigate to variables and add a variable


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90e8f249949feaacebc44e6eef7d165c.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_837478069ed2a9c994167bb87bd4eda4.png) </span>

<span id="_2-2-配置资源组变量"></span>
## 2.2 Configure resource group variable


1. Define the name of the resource group filter item

2. Select the data source to be visualized.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df9b9cf7657049d6ba3287749002cc7b~tplv-goo7wpa0wc-image.image) </span>


3. Query configuration Where Query Type selects Label values, Label selects `mlp_resource_group`, and Metric selects `mlp_resourcegroup_info`

> For the selection of Label and Metric, refer to the [Resource Group Metrics]\-[Metric Description] section in the [Monitoring--Machine Learning Platform-Byteplus](https://docs.byteplus.com/en/docs/mlp/Monitoring_configuration_instructions) Documentation


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/066f89dc3f4e497388fe3bfde469ce57~tplv-goo7wpa0wc-image.image) </span>


4. Run result Click Run query. If configured successfully, you can see the resource group ID with data in Preview of values


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4b2d82b93ac4772be5e42cd9b527364~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-配置队列变量"></span>
## 2.2 Configure Queue Variables

Specific operations are generally the same as the "Resource Group" configuration; refer to the following best practices.


1. Add variable.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_99c1f67c8a21ac788bd3181f58a775b4.png) </span>


2. Define the queue filter name.

3. Select the data source to be visualized.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_426348c9b06d640f2b48792d2fe5e8ac.png) </span>


4. Query configuration. In this step, we need to associate the queue with its resource group, so select Query result for Query Type and enter `mlp_resourcequeue_info{mlp_resource_group=\"$ResourceGroup\"}` for Query.

5. Regular expression configuration. Enter the regular expression `/.*mlp_resource_queue=\\\"(.*?)\\\".*/`.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f48efe48ae66412ea7140c6ec1ffd4ab~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-自定义任务实例配置"></span>
## 2.3 Custom Task Instance Configuration

The specific operations are roughly the same as the "Queue" configuration; refer to the following best practices.


1. Add a new variable.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64d85958bfb9a1e2b471bbbaec40c25c.png) </span>


2. Define the name of the resource group filter item.

3. Select the data source to be visualized.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e42a9dc6553f44d965cd4537bc80c834.png) </span>


4. Query configuration. In this step, we need to associate the custom task with its queue, so select Query result for Query Type and enter `mlp_customtask_info{mlp_resource_group=\"$ResourceQueue\"}` for Query.

5. Regular expression configuration. Enter the regular expression `/.*mlp_resource_queue=\\\"(.*?)\\\".*/`.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_51cf553f29028c2fb94e7dae4d8f099a.png) </span>

<span id="_2-4-保存dashboard"></span>
## 2.4 Save Dashboard


1. After configuring the three variables (resource group, queue, and custom task), click the upper right corner to save the current dashboard variable settings.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_92564637d6c7e69d188774ce74beca8a.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f50cdfc648e9eb3492b0a7125d485bd.png) </span>


2. Return to the Dashboard interface, where you can see 3 variable filter components at the top and a visual dashboard template at the bottom.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_953866e1539813e18c66b330f769169a.png) </span>

<span id="步骤三：最佳实践——以配置gpu资源总量看板为例"></span>
# Step 3: Best Practice \- Take configuring a total GPU resource dashboard as an example


1. Customize the dashboard title settings.

2. Select the data source to be visualized.

3. Enter the PromQL query statement and execute the command. You can find the PromQL query statements corresponding to the metrics for the dashboard you need to create in the [Monitoring -- Machine Learning Platform - Byteplus](https://docs.byteplus.com/en/docs/mlp/Monitoring_configuration_instructions) Documentation. Paste it into the code section below and click Run queries to execute the command.

4. Customize the caption title settings. In the best practice, the line in the figure represents the changes in the number of cards used at each moment for the custom task = "t\-20240902200928" under the queue = "q\-20240305193945" under the resource group = "r\-20231013212037\-vvmhb".

5. Click save to save the current dashboard settings. If you need to add more dashboards for Monitoring indicators, you can return to the Dashboard page and click the Add button in the top\-right corner to add more.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aac1e5bedf15586f4f0e31bf04ade9f4.png) </span>
