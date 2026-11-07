---
title: "Item Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Item_Analysis"
---

<span id="a40cb79f"></span>
# 1. Overview

Business dimension, also known as item. In the underlying EUI model of DataFinder, behavior records are recorded around people, events, and items. In short, a user triggers an event for something within a product. What are some common items? The business dimension in e\-commerce can be commodities, the business dimension in online education can be courses, the business dimension in banking can be financial products, loan products, etc., and the business dimension in short videos can be short videos, etc.

<span id="_2-常见场景"></span>
# 2. Common scenarios

So what common analysis scenarios can item satisfy?

<span id="延展属性"></span>
## Extended attribute

When the event is triggered at the corresponding time, some attribute information cannot be collected, or it requires a large technical cost. The front\-end and back\-end interfaces are connected to each other for transmission. Faced with this situation, you can use the item business dimension.

For example, content class App, you need to view different heat rankings according to the release time of the content, content publisher ID, content publisher tags, etc. However, the front\-end information can only collect limited attribute information such as its own content ID, content classification, and content tags. The information related to the content publisher exists in the background business database, so the content ID can be used as a key associated with the transaction table and the item table. When reporting on the event, only the information that can be collected at the front end such as the content ID is still collected. The attributes that need to be analyzed in the remaining business database are reported as fields of the item table, and the key is used for association analysis.

<span id="变化属性"></span>
## Change attribute

Once the attribute information collected by the transaction table falls into the database, it cannot be changed or changed. However, some attribute information may change at any time, and in this case, it can still be solved using the item business dimension.

For example, in the hotel catering app, the label of each dish changes frequently. For example, "seasonal dishes" will be adjusted according to different times, and the seasonal dishes are different every month, but when analyzing, you only want to view the browsing and consumption of seasonal dishes in the current quarter according to the latest label classification. Therefore, the dish ID can be used as a key to associate the transaction table and the item table. When the event is reported, only the dish ID attribute is still collected, and the rest of the attributes that change at any time are reported as fields of the item table, and the key is used for association analysis.

<span id="_3-item支持情况"></span>
# 3. Item analysis

<span id="6c4b1ddf"></span>
## Prerequisite


* You have created the business dimensions in the DataFinder in **Data Management** \> **Business Dimensions** , see activity details [Item (Business Dimension)](https://docs.byteplus.com/docs/DataFinder/Item_Business_Dimension).

* You have completed the data access operations required before analysis.

   * When accessing business dimension data, ak/sk is required. You need to contact BytePlus technical support staff to obtain ak/sk information, and then perform business dimension data access.


<span id="10023e78"></span>
## Item Analysis operation


* Item Analysis tool

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/378c604b68394f15967f8e260cdb4e4c~tplv-goo7wpa0wc-image.image) </span>

   You can use DataFinder's business dimension analysis tools to perform data analysis at the business dimension level on DataFinder's Analysis Tools \> Advanced Analysis \> Item Analysis page.

   * In the configuration area above, you can select the created business dimension and the grouping properties of data analysis as needed, configure the analysis metrics, and click Query to query and analyze the reported data.

   * In the Query Detailed Data below, you can select the time range for analysis. After clicking Expand by Time, you can query the detailed data of the indicators in the selected time range.

* Other analysis tools

   Since the business nature of item objects is an extension of event attributes, item objects can be directly analyzed in "Advanced Analysis \- Item Analysis", and can also be used in other advanced analysis for attribute filtering and grouping.

   Take the e\-commerce demo scenario provided by DataFinder as an example, the goods dimension is created in the data management, which includes business dimension attributes such as product name and sub\-category. You can use these properties in event analysis tools.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1273471558cb4f90b18667964b69b904~tplv-goo7wpa0wc-image.image) </span>

   The support for each analysis tool module is as follows:
