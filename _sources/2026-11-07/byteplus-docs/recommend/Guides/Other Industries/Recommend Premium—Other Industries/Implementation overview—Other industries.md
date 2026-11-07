---
title: "Implementation overview—Other industries"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-other_premium_implementation_overview"
---

For BytePlus Recommend Premium, there are five main steps for BytePlus to understand the use case and provide the service.


|**Step** |**Description** |
|---|---|
|[Setting up](https://docs.byteplus.com/recommend/docs/other_premium_setting_up) |Identify recommendation use case(s) to collaborate on, align data requirement and obtain BytePlus credentials. |
|[Importing and validating data](https://docs.byteplus.com/recommend/docs/other_premium_importing_and_validating_data) |Upload trial, historical, and incremental data on User, Product and UserEvent to BytePlus. |
|[Training models](https://docs.byteplus.com/recommend/docs/other_premium_training_models) |Choose your recommendation scene, its optimization metrics and post\-processing rule, then the BytePlus Recommend team will build the model. |
|[Getting predictions](https://docs.byteplus.com/recommend/docs/other_premium_getting_predictions) |Integrate with BytePlus APIs to get real\-time recommendation results, followed by conducting allowed list testing and load testing to prepare for A/B testing. |
|[Measuring performance](https://docs.byteplus.com/recommend/docs/other_premium_measuring_performance) |Launch BytePlus Recommend with A/B testing to compare BytePlus recommend performance with a control group. |


<span id="Data"></span>
# Data

In BytePlus Recommend, we require three types of data from your users to proceed with our recommendations:


* **User**—The users who use your platform.

* **Product**—The products your platform offers.

* **UserEvent**—The interaction between users and products.


<span id="ece551ea"></span>
# APIs in BytePlus Recommend Premium

The BytePlus Recommend team provides three types of APIs:


* **Data Synchronization APIs**

   * [WriteUsers](https://docs.byteplus.com/recommend/reference/retail_writeusers)—To upload historical and incremental User data.

   * [WriteProducts](https://docs.byteplus.com/recommend/reference/retail_writeproducts)—To upload historical and incremental Product data.

   * [WriteUserEvents](https://docs.byteplus.com/recommend/reference/retail_writeuserevents)—To upload historical and incremental UserEvent data.

* **Recommendation Result APIs**

   * [Predict](https://docs.byteplus.com/recommend/reference/retail_predict)—To retrieve real\-time recommendation results for a given user under a specific scene.

   * [AckServerImpressions](https://docs.byteplus.com/recommend/reference/retail_ackserverimpressions)—To send back to the server the actual products shown to the user. The actual products may differ from the model recommendations returned by the Predict API due to additional conditions applied by your platform, such as filter, insert, and keep. BytePlus Recommend uses this data to improve model logic and performance.
