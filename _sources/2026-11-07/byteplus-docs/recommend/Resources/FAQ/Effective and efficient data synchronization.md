---
title: "Effective and efficient data synchronization"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/resources-effective_and_efficient_data_synchronization"
---

This section provides answers to frequently\-asked questions about effective and efficient data synchronization.

<span id="There are too many data fields—what should I send?"></span>
# There are too many data fields—what should I send?

Each field is marked as either Required or Optional. Providing more data will improve the recommendation performance, thus we recommend sending as much information as possible, even if the fields are optional.

The User and Product data fields, in particular, are crucial for optimizing the recommendation performance, as they provide information about what users may like. Such data is especially important if the availability of UserEvent data is sparse.

**EXAMPLE**


* People living in certain areas are more likely to buy certain items. For example, people living in Seattle are more likely to buy umbrellas. Thus, knowing the location of a user helps with personalized recommendations.

* Some users are attracted by a promotion or clearance sale and are likelier to click on products with a promotion tag on the listing page. Thus, knowing which products are on sale helps with personalized recommendations.


<span id="How do I format free format string field inputs?"></span>
# How do I format free format string field inputs?

The actual value of free format string fields is not important to the system, which only keeps track of identical values across different entries. Therefore, take note of the following for free format string fields:


* The input value itself does not matter. For example, it does not matter if you use "new user" or "New" to represent a new user for fields like User.tags.

* However, a consistent value should be used to represent the same meaning across different entries. For example, do not use "new user" in some cases and use "New" in some other cases.


<span id="What should I use as a stable user identifier?"></span>
# What should I use as a stable user identifier?

A user identifier, known as user_id, can be any component depending on your business needs. In order to achieve effective recommendation performance, the user_id must be stable. The table below provides examples of what to use as a stable identifier:


|**Business case** |**Stable identifier to use** |
|---|---|
|You use an ID\-mapping service to map device\-id, cookie\-id, user\-id, and visitor\-id to a globally\-consistent ID. |globally\-consistent ID |
|You have a mobile app. |device_id |
|You have a web app, and the app requires a login status. |login user_id |
|You have a web app, and the app has a visitor status. |cookie\-id<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To maximise recommendation performance, try to extend the cookie lifecycle as much as possible. Alternatively, you can also use UserEvent.extra to send login/logout status.</div><br> |


<span id="How do I send extra data?"></span>
# How do I send extra data?

We provide a field called extra in almost all requests. It is a catch\-all field where you can send additional information as key\-value pairs to us. To send extra data, put them in this field and inform the BytePlus Recommend team about the definitions of the extra data.

<span id="How do I send data efficiently?"></span>
# How do I send data efficiently?

There are several ways to send data efficiently so that it is less time\-consuming. You can send multiple data records in one API request. For WriteAPIs, you can send up to 2,000 records in one request.

Alternatively, you can create parallel API requests, up to 10,000 records. However, you should avoid high parallelism to prevent throttling. If you get throttled (error code 429), you can manually retry with an exponential backoff.

<span id="Can I carry out historical and real-time data synchronization in parallel?"></span>
# Can I carry out historical and real\-time data synchronization in parallel?

For Recommend Standard, historical data should be uploaded using GCS, S3, or WriteAPIs first before users can proceed with real\-time data synchronization using WriteAPIs.

For Recommend Premium, real\-time data synchronization can take place in parallel with historical data upload if needed. If you choose to upload historical data using WriteAPIs, the BytePlus Recommend team will provide you with a mock tenant_ID to use while conducting the historical data import. The mock tenant_ID allows users to carry out concurrent real\-time data synchronization, which requires the user's own tenant_ID.

In both cases, there should be no gaps in data between the last day of the uploaded historical data and the first day of synchronized real\-time data. To enable a more comprehensive view of the data for model training, it is recommended to ensure an overlap in the data timeframes for historical and real\-time data.
