---
title: "Overview"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Overview_"
---

<span id="_1-功能概述"></span>
# 1. Functional Overview

IDMapping is a functional module that uses **association rules and fusion algorithms** to identify and connect the same users from different channels, serving as the foundational base of VeCDP data.

For example, a user's data pool includes order or behavioral data from WeChat Official Account, Enterprise WeChat, Tiktok Mall, and multiple proprietary apps. Each channel acquires user data with inconsistent identifiers (such as WeChat's UnionID, External_UserID, and the proprietary apps' DeviceID, EmailID, WebID, and business UseID). Generally, due to the inconsistency of user primary keys, data cannot be linked for analysis. IDMapping resolves such issues, enabling true connectivity of data from various channels, creating more complete data files and profiles, and facilitating more precise insight analysis and marketing applications.

Additionally, the VeCDP\-ID graph construction feature also supports **multi\-subject ID graph construction**, allowing the construction of multiple subjects beyond "individuals," such as vehicles, merchants, etc. By configuring mapping relationships between multiple subjects, management and analysis of multi\-subject scenarios can be achieved.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d46b58ca771e4fd9be5ad256888205e9~tplv-goo7wpa0wc-image.image" width="1966px" /></div>


<span id="f6a9a052"></span>
# 2. Prerequisites

Only group administrators (admin accounts) can configure the ID graph.

<span id="3241b3c4"></span>
# 3. Application Scenarios

<span id="6fc3d6cd"></span>
### 3.1 Single\-Subject ID\-Mapping Application Scenarios

In single\-subject scenarios, most activities revolve around the "**user**" as the main subject for ID recognition and integration. Common scenarios include:


* Subject: **Cross\-Platform User Identification**: Users may use the same service on different devices (such as PCs, phones, tablets). ID\-Mapping helps companies identify the same user behind these devices to provide a seamless cross\-device experience.

* Subject: **Marketing Activity Optimization**: Through ID\-Mapping, companies can more accurately understand user profiles and significant features, combine attributes, orders, and behavioral data to comprehensively analyze user preferences, optimize marketing strategies, achieve precise ad placements, increase conversion rates, and user engagement.

* Subject: **Personalized Recommendations**: By combining user attributes, orders, and behavioral data to understand user profiles, companies can provide more personalized content recommendations to enhance user experience.


<span id="bd93a489"></span>
### 3.2 Multiple Subject ID\-Mapping Application Scenarios


* **Automotive Scenario:** 

   * Subject: **Marketing and Promotion Scenarios:**  For example, if a car manufacturer wants to promote a specific type or color of car, they can pull target users related by a multi\-subject relationship like [Person<\-\>Car=Follow Relationship] to send out marketing promotions. This enables scenarios where users immediately receive corresponding marketing information upon clicking to follow or algorithmically predicting interest.

   * Subject: **Car Owner Service Scenarios:**  For instance, focusing on "vehicles" as subjects, businesses can locate targeted vehicles in need of service based on usage data, identify the associated "car owner" group, and deliver messages to enhance car owner service experiences.

* Subject: **Mass Consumption Scenarios:**  In mass consumption scenarios, the multi\-subject capability enables more precise person\-to\-product matching, person\-to\-store matching, and product\-to\-store matching.


<span id="f0c67e47"></span>
# 4. Operation Instructions


|**Document Title** |**Document Details** |
|---|---|
|ID\-Mapping configuration logic explanation |[View operation instructions](https://www.volcengine.com/docs/7139/1282860) |
|Single Subject ID\-Mapping configuration operation instructions |[View operation instructions](https://www.volcengine.com/docs/7139/1222701) |
|Multiple Subject ID\-Mapping configuration operation instructions |[View operation instructions](https://www.volcengine.com/docs/7139/1222702) |
|ID\-Mapping operation and management |[View operation instructions](https://www.volcengine.com/docs/7139/1222703) |


<span id="51d76af3"></span>
# 5.**FAQs**

Q1: **Which data in the data file supports OneID correction and where is it set?** 


1. The data file does not automatically generate task production data, it only tags the datasets, so in most cases, there is no need for a backfill.

2. Historical customers in the data file will automatically be included in the list of tasks for OneID correction due to the existence of validation data format rules for building system transformation visualization modeling tasks, which will be executed regularly for correction backfill.

3. Only **detailed data and behavioral data** in the data file need OneID correction backfill. Attribute data and dimensional data files obtain the latest partition data daily without the need for correction backfill.


Q2: **When is the correction of OneID data executed?** 


1. The correction of OneID data is an auxiliary task that triggers the OneID data correction task after the latest tasks of the day are executed. For example, visual modeling tasks will prioritize the execution of the most recent daily instance tasks. Upon successful execution, the task will initiate a correction backfill for OneID data.


Q3: **When DataFinder is deployed independently, does it support OneID correction capability?** 


1. It is not supported at the moment.
