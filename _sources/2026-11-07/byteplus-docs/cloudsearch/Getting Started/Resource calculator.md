---
title: "Resource calculator"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Resource_calculator"
---

Before using Cloud Search, you need to estimate the required computing resources to ensure system stability and optimize costs. Cloud Search offers a resource calculator that helps you understand how to estimate the needed resource scale based on sample data, allowing adjustments during actual deployment according to test results. This article explains how to use the resource calculator.

<span id="jSyjFmzK"></span>
## Procedure


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **Resource calculator** on the left navigation bar.

4. On the **Resource calculator** page, choose **General scenario** or **AI scenario** according to your needs, then configure the following parameters.

   
   <Tabs>
   <Tab zoneid="mWhYhGAY5x" title="General scenarios">
   <TabTitle>General scenarios</TabTitle>
   
   
   |Parameter |Description |
   |---|---|
   |Source data |Set your source data size, ranging from 1 GiB to 1000 TiB. |
   |Daily incremental data |Set your daily incremental data size, ranging from 0 GiB to 1000 TiB. |
   |Data retention period |Set the retention period for your data from 0 days to 3 years. |
   |Replicas |Set the number of replicas for your data from 0 to 10. |
   |Write throughput |Set your data write throughput, ranging from 0 to 1000 MB/s. |
   |Complex aggregation query |Select whether your business includes complex aggregation queries. |
   
   
   
   </Tab>
   <Tab zoneid="OFGUomRcAX" title="AI scenarios">
   <TabTitle>AI scenarios</TabTitle>
   
   
   |Parameter |Description |
   |---|---|
   |Type |Select your instance type as needed; currently supports **Performance** and **Capacity**. |
   |Data count |Set your data count, ranging from 1 to 10,000, in units of millions. |
   |Data dimension |Set your data dimension, ranging from 1 to 16000. |
   |Replicas |Set the number of replicas for your data, ranging from 0 to 10. |
   
   
   
   </Tab>
   </Tabs>
   

5. In the **Recommended configuration** section, view the instance configurations recommended by the system based on your business needs. You can click **Create instance** to go to the instance creation page and create an instance according to the recommended configuration.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your data volume is too large and the Resource calculator cannot recommend a suitable configuration, you can <a href="https://console.byteplus.com/workorder/create?step=1&SubProductID=P00000255">submit a ticket</a> to contact technical support for assistance with resource estimation and deployment plans.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you select <strong>AI scenario</strong>, the recommended configuration applies to DiskANN + RabitQ index. If you use other indexes and vector types, additional resources from 1 to 5 times the current recommended configuration are required depending on the specific situation.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For detailed logic and principles of resource calculation, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/Estimating_instance_resources">Instance resource estimation</a>.   </div>
