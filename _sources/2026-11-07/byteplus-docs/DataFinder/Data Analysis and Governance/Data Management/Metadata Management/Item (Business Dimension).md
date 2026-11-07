---
title: "Item (Business Dimension)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Item_Business_Dimension"
---

If you need to expand the data scope of event analysis through dimensional data, you need to first create dimensional information that may be used in subsequent analysis data in the DataFinder, and then access the corresponding dimensional data during subsequent data collection. If the dimensional data is successfully reported, you can query and analyze the dimensional related data in the DataFinder. This article shows you how to create a business dimension in DataFinder.

<span id="02c0a6a0"></span>
# Background information

Business dimension, also known as item. In DataFinder, behavior records are recorded around people, events, and items. In short, a user triggers an event for something within a product. What are some common items? The business dimension in e\-commerce can be commodities, the business dimension in online education can be courses, the business dimension in banking can be financial products, loan products, etc., and the business dimension in short videos can be short videos, etc.

You can define the items involved in the way of business dimension according to the needs of subsequent data analytics, and add the business dimension information to the data management of DataFinder first, which is convenient for subsequent data collection and data analytics.

<span id="e1da742b"></span>
# Usage restrictions

At present, DataFinder places some restrictions on the business dimension, as follows:


* Each app/project currently **can create up to 20** business dimensions.

* Each business dimension **can create up to 50** properties.


<span id="8128143e"></span>
# Create/edit business dimensions


1. After logging into the DataFinder console, go to the `Data Management > Metadata Management > Business Dimensions`page where you can view a list of all business dimensions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c34990247c9a4f1fab75f705789cec25~tplv-goo7wpa0wc-image.image) </span>

   The picture above is our e\-commerce industry demo, in which "goods" and "videos" are our pre\-defined business dimensions.

2. In your own project, you can click the `Create business dimension`button to start creating the business dimension you need to use, and configure the name, properties and other configuration parameters of the business dimension in the pop\-up page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b0b4a10b0574e40b2519dddf49a3103~tplv-goo7wpa0wc-image.image) </span>


<span id="6bf89522"></span>
# Next steps


1. dimensional data access

   * When accessing business dimension data, ak/sk is required. You need to contact BytePlus technical support staff to obtain ak/sk information, and then perform business dimension data access.

2. Using dimensional data for data analytics .
