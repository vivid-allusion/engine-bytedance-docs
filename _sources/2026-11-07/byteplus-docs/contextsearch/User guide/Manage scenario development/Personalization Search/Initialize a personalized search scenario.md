---
title: "Initialize a personalized search scenario"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Basic_configuration"
---

This topic describes how to initialize the personalized search scenario through basic configuration.

<span id="FVBbKygF"></span>
## Prerequisites

A personalization search scenario has been created. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario).

<span id="N5PJcBJF"></span>
## Procedure


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. On the target personalized search scenario page, configure the following parameters, then click  **→** .

   
   |Parameter |Description |
   |---|---|
   |Database type |Currently, only **Cloud Search** is supported. |
   |Instance name/ID |Select the target OpenSearch instance from the dropdown list. Supports fuzzy search based on keywords in the instance name. If a new OpenSearch instance is needed, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only OpenSearch 2.9.0 or later instances support ContextSearch.</div><br> |
   |User name |Enter the username of the instance. |
   |Password |Enter the instance password. |
   |Private network |To ensure smooth intranet access, it is recommended to select the VPC in the region where your existing cloud services are located. Subnets in different availability zones within the same VPC can communicate with each other. If you want to create a VPC, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |The system automatically filters available subnets based on the region, availability zone, and VPC that you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Select model/inference service |Select the model and inference service used by the scenario from the dropdown list. Currently supporting **Public model** and **Ark model**.<br><br>If you need a new inference service, click **Create an inference service**. For detailed steps to create a common model, see [Create a custom inference service](https://docs.byteplus.com/en/docs/contextsearch/Create_a_custom_inference_service).  |
   |API Key |Select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key). |
   |TOS bucket |Select the bucket to store the model. If there are no available buckets, create one. For more information, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket). |
   |Path |Select the path to store the model. |
   

   After saving, the scenario enters the **Initializing** state. When the scenario status changes to **Running**, the scenario initialization is completed.

&nbsp;
