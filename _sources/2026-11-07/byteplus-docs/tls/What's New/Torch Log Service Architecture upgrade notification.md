---
title: "Torch Log Service Architecture upgrade notification"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/structure-upgrade-notification"
---

In order to enhance service performance and improve product stability, Torch Log Service (TLS) will gradually upgrade the backend service Architecture for all users in the near future.

<span id="60904457"></span>
### Upgrade content

TLS is BytePlus's self\-developed observable storage engine. Its new generation architecture 2.0 has been officially released, which has been refined through extensive use in various BytePlus applications, providing enhanced search performance and richer query and analysis capabilities.


* TLS supports PB\-level log elastic writing, large\-scale data storage and efficient data writing.

* TLS supports querying tens of billions of logs in seconds for fast data processing and analysis.

* TLS supports more than 200 SQL functions to provide more powerful data analytics and processing capabilities.

* TLS supports multi\-data source correlation query, which is convenient for you to comprehensively analyze different data sources.

* TLS supports richer query and analysis features, such as phrase query and reconstructed index, to improve query efficiency and accuracy.


<span id="5cd0b697"></span>
### Upgrade Process

Starting today, users who activate TLS for the first time will use new generation architecture 2.0 by default. The architecture for the existing users will be gradually upgraded to new generation architecture 2.0. During the upgrade process, there might be a small amount of data duplication in Kafka protocol consumption scenarios. Once the upgrade is complete, you will receive an in\-site message notification confirming the successful upgrade to the new architecture 2.0.

<span id="50fb9025"></span>
### Upgrade Impact

You will not perceive the upgrade process. However, a very few query and analysis syntax may be incompatible, which could result in the same query and analysis statements returning inconsistent results after the upgrade. If you are using syntax such as fuzzy queries, it is recommended to refer to the product documentation and adjust your query and analysis statements to avoid any changes in syntax meaning affecting the query and analysis results.

If you have any questions or problems, please contact the product managers of TLS. Thank you for your support and understanding of BytePlus.
