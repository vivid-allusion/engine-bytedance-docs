---
title: "Explanation of DataFinder Proper Nouns"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Explanation_of_DataFinder_Proper_Nouns"
---

<span id="一、产品名及产品概念："></span>
### 1. Product name and product concept:

DataFinder = BytePlus Growth Analysis refers to BytePlus' **user behavior analysis** product, sometimes referred to simply as "Finder" in this series of documents


* **User behavior**: \*\*\*\* User behavior is composed of five simple elements, namely: time, place, person, interaction, and interactive content.

* **User behavior data**: \*\*\*\* The simplest form of existence is the log, which records the user's various behaviors, such as total page browsing, purchases, clicks, ratings, comments, and so on. These data can be analyzed horizontally for the common characteristics of a certain type of client base, such as: analyzing the click through rate of all users for a certain page; it can also be analyzed vertically for the details and processes of a user's behavior, such as a user's behavior.

* **User behavior analysis**: \*\*\*\* Collect, organize, and count all the data (including downloads, usage frequency, visits, access rate, retention, etc.) in the process of using the product by users, and then analyze the rules of user use of the product. Provide strong data support for the follow\-up development, optimization or marketing activities of the product.


<span id="二、火山引擎增长分析中涉及的相关专业概念："></span>
### 2. Relevant professional concepts involved in BytePlus DataFinder:


1. **Event**: refers to one or a type of behavior of the user, such as: user watching videos, user comments, etc.

2. **Virtual events**: It is a combination of multiple events, for example: user forwarding or commenting or liking events constitute user interaction events, and any event that occurs by the user is counted as an interaction event.

3. **Event attributes** (also known as Params): used to describe the dimensional information when the event occurs, including user information (user_id), device information (app version, device number...), etc.

4. **Event public properties** (also known as headers): It refers to the general properties that each event will report.

5. **Bits** : It can refer to in\-app resource bits, operational activities, etc., which may be used in attribution analysis functions; however, if you want to use "bits" for attribution analysis, you need to pre\-define "bits" on the web page. For specific methods, see [Attribution Analysis](https://docs.byteplus.com/docs/DataFinder/Attribution_Analysis).

6. **indicators**: refers to the event or virtual event quantitative value (is the specific value); such as the number of visitors, page views, stay time are common indicators;

7. **Confidence interval**: the proportion of the data contained in the threshold range to all the data; the larger the confidence interval value, the higher the tolerance.

8. **Event tracking**: It refers to the process of writing event logic into the code through the development of the SDK.

9. **Full event tracking**: also known as "no event tracking", "no trace event tracking" and "automatic event tracking". Full event tracking is to automatically collect and report the browsing of standard pages and the clicking of standard elements.

10. **Touchpoint**: It refers to the medium through which users come into contact with your products/services, such as websites, APPs, Mini Programs, official accounts, etc., which can be called touchpoints.

    &nbsp;


<span id="_3-specific-english-concepts-involved-in-byteplus-datafinder"></span>
### 3. Specific English concepts involved in BytePlus DataFinder:


1. **touchpoint_click**: user click behavior touchpoint

2. **app_launch**: application start, app start, open app

3. **LTV**: life time value (life time value), which is the sum of the economic benefits obtained by the enterprise from the interaction behavior of users in the product

4. **id\-mapping**: identity association recognition

5. **Session** (also called session): refers to a series of behaviors (such as browsing, clicking, placing an order) when the user is continuously active on your website/H5/Mini Program /APP.
