---
title: "Data Asset"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Asset"
---

The data asset configuration is used for the range of data that the agent can retrieve during use and analysis. After the configuration is completed, the system will update the asset content according to the T + 1 cycle, and preferentially retrieve the data within the configured range when used.

<span id="4498fd7c"></span>
# Background Information

The current agent's data source configuration supports two data sources:


* Add the created dataset as a data source for the agent.

* Add a visualization chart created in Datawind (DataWind) as a data source for the agent. This approach has been supported since version 3.2.0, and you need to combine the DataWind products.


This article describes the activity details for configuring an agent data source based on a created dataset; DataWind for creating a data source based on a chart.

<span id="3a733bdb"></span>
# Prerequisite

Before configuring the data source of the agent, you need to create the corresponding data as a dataset of the DataAgent to complete the data preparation operation. For details, please refer to: [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview_).

<span id="bc510d7b"></span>
# Operation Steps

With this configuration, users can flexibly delineate the data access boundaries of the agent, thus enhancing the relevance and accuracy of the Q & A results. Here are the steps to configure a data asset:


1. On the agent list page, select the corresponding agent and click the **agent configuration** button to enter the agent configuration page.

2. Side navigation Click **Data Assets** , and click the **Add Dataset** button at the top right of the dataset list to add the dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8facd1a2220403b903958077779a762~tplv-goo7wpa0wc-image.image) </span>

3. Add a list of successful data asset display datasets, which can be turned on or off for datasets, and support deletion of datasets.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04126c8487b6495bba841f338879ba6b~tplv-goo7wpa0wc-image.image) </span>


<span id="d11cf313"></span>
# Turn Dataset Vectorization On/Off

After the initialization of the dataset is completed, the vectorization of the dataset is turned on by default. If the subsequent dataset does not need to be used by the current agent query, you can click "Completed" in the status column, jump to the initialization configuration page, and turn off the vectorization.

After closing, the configuration of the dataset is preserved, but subsequent use of the agent will no longer query the data in the corresponding dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42ec803c341e466baf8fee7fbf10c9bb~tplv-goo7wpa0wc-image.image) </span>
