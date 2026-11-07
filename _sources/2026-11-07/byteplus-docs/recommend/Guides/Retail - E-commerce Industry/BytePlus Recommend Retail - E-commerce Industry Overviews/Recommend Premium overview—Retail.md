---
title: "Recommend Premium overview—Retail"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-retail_premium_overview"
---

BytePlus Recommend Premium is dedicated to clients who have complicated data requirements or unique business objectives and require a customized solution for their businesses.

We provide a range of expert services to help you meet your needs. With extensive technical knowledge and expertise, our Premium team is able to help clients streamline their projects and deliver results.

Our team consists of algorithm engineers, data engineers, and data analysts that will work by your side to provide any assistance required during the entire process. We will strive to enhance your integration process as well as explore new and more effective solutions for you and your business.

<span id="21a61c58"></span>
# Data required in BytePlus Recommend Premium

In BytePlus Recommend, we require three types of data from your users to proceed with our recommendations:


* **User**—The users who use your platform.

* **Product**—The products your platform offers.

* **UserEvent**—The interaction between users and products.


<span id="2edd239a"></span>
# APIs in BytePlus Recommend Premium

The BytePlus Recommend team provides two types of APIs:


* **Data Synchronization APIs**

   * [WriteUsers](https://docs.byteplus.com/en/recommend/reference/retail_writeusers)—To upload historical and incremental User data.

   * [WriteProducts](https://docs.byteplus.com/en/recommend/reference/retail_writeproducts)—To upload historical and incremental Product data.

   * [WriteUserEvents](https://docs.byteplus.com/en/recommend/reference/retail_writeuserevents)—To upload historical and incremental UserEvent data.

* **Recommendation Result APIs**

   * [Predict](https://docs.byteplus.com/en/recommend/reference/retail_predict)—To retrieve real\-time recommendation results for a given user under a specific scene.

   * [AckServerImpressions](https://docs.byteplus.com/en/recommend/reference/retail_ackserverimpressions)—To send back to the server the actual products shown to the user. The actual products may differ from the model recommendations returned by the Predict API due to additional conditions applied by your platform, such as filter, insert, and keep. BytePlus Recommend uses this data to improve model logic and performance.
