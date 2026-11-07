---
title: "Intelligent Analysis and Operation Scenarios"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Intelligent_Analysis_and_Operation_Scenarios"
---

<span id="_1-概述"></span>
# 1. Overview

With the deepening development of the concept of "openness, sharing, and cooperation" on the Internet, more and more enterprises hope to integrate the data chain between various stages of the enterprise lifecycle, allowing data sharing between systems to achieve rapid, efficient, and convenient data querying and application. It also provides data support for subsequent big data applications, intelligent applications, etc.


* This article briefly describes the CDP+DataWind product linkage scenario

* Supplemented with product feature descriptions, how enterprises can achieve intelligent analysis and operations through the linkage of CDP and DataWind


<span id="_2-场景阐述"></span>
# 2. Scenario Description

In the operational scenarios of enterprises, employees need to be data\-driven, promptly identify abnormal data, uncover the reasons behind the "anomalies," and promptly follow up and handle them to help sustain business growth.

**For example:**  When you, as a store employee, find a significant drop in sales this month, how would you use intelligent analysis and operations to solve the problem?

<span id="_3-产品解决方案"></span>
# 3. Product Solutions

<span id="_3-1-整体解决方案概述"></span>
## 3.1 Overview of the overall solution

Deep data insights based on DataWind products reveal potential issues, identify key audiences through attribution analysis and other product capabilities, synchronize insights into CDP for refined operations targeting the group, and finally track and analyze key metric changes based on CDP+DataWind to validate effectiveness. Continuously iterate operational strategies, truly achieving intelligent insights leading to closed\-loop decisions and executions.

<span id="77306c0a"></span>
## <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_bdbafe1901a0a612835d8dea2db8487c) </span>

<span id="bd5bae43"></span>
## 3.2 Breakdown of Solutions Step by Step

<span id="第一步：从数据入手，通过结构化思维拆解相关数据指标"></span>
### Step One: Start with the data, break down relevant data indicators through structured thinking

Structured thinking means logical thinking, starting from the problem to explore the causes. In this scenario, when we notice a downward trend in store sales, we should not think divergently, rely on past experiences to enumerate a bunch of possible reasons (such as market environment, price wars with competitors, promotional discounts, etc.). This not only disrupts our thinking but also makes us lose direction when adjusting operational strategies.

Firstly, we should start with the problem. Since sales are declining, we should start by breaking down the relevant indicators of sales, then analyze the reasons for abnormal fluctuations in corresponding indicators, further clarifying the root of the problem. For example, if store sales = number of customers \* average spending, we can further break down the "number of purchases" index into "new customers" and "repeat customers"; while "average purchase amount" is closely related to "product prices," "discount rates," and more.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_30616d6734fa4bab630867ce7372830c) </span>

<span id="第二步：-bi工具深度洞察数据，发现潜在问题"></span>
### **Step Two: BI Tools Deep Dive into Data for Insights**

Once data indicators are structured clearly, further "attribution" is needed. We drag "payment date" into the dimension item, drag "sales amount" into the index item, select the aggregation method as sum; in the filter conditions, choose payment from 2021\-09\-01 to 2021\-10\-31, and filter for the stores to be analyzed. Configure the line chart showing the trend of sales amount changes in the BI tool.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_65991eb8f90ca0293b6281ecd1494a54) </span>(\*The above image is for reference only)

Through the line chart, we can identify the nodes with abnormally low sales, and utilize DataWind's intelligent attribution analysis capability to generate attribution analysis reports. The reports rank dimensions based on the degree of impact causing the decline, further clarifying which dimensions are causing the decrease in sales.

In this scenario, **we found that "customer type" and "membership level" have a significant impact on the decrease in sales:** 


* Among customer types, the sales of walk\-in customers dropped significantly compared to the same period last year.

* Among membership levels, the sales of regular members dropped significantly compared to the same period last year.


<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f3d396ad22371e9dce6f7f59eb943710) </span>(\*The above chart is for reference only)

<span id="第三步：抽丝剥茧，锁定关键人群"></span>
### **Step Three: Thoroughly Identify Key Customer Segments**

By using the attribution analysis report, we can pinpoint groups highly correlated with the decrease in sales. Subsequently, we can directly create a new group that caused this fluctuation through attribution analysis, or utilize CDP segmentation capabilities to select opportunity groups based on store information and member\-related tags, such as "This month's buyers at Store B," "Buyers at Store B within the past year," "Regular members who purchased a product within the past year but have/haven't repurchased this month."

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_26fbacf80a92c503c9c70a9a8e22765d) </span>

<span id="第四步：洞察关键人群画像特征，制定运营策略"></span>
### **Step Four: Understand Key Customer Segment Characteristics and Develop Operational Strategies**

Once groups are identified, how should stores tailor appropriate operational strategies for these groups?


* **Analyze walk\-in customer characteristics to drive purchase decisions** In CDP's "Audience Insight" module, insight into the characteristics of "walk\-in customer groups" can be obtained. Discovery: "Points Sensitivity \- Yes" is the most significant feature in the current group, allowing the exportation of this group for the distribution of discount vouchers to facilitate user purchase decisions.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_99a0a045ba5b91bf8d71ae5e8a8b7e85) </span>(\*The above data is for reference only)


* Perform comparative analysis to identify differences. Encircle "ordinary members who purchased products within one year and repurchased this month" and "ordinary members who purchased products within one year but did not repurchase this month." Conduct demographic comparative analysis: significant differences exist in the 18\-24 age group. Further analyze whether the new product of these two months does not match this age group's characteristics. It is necessary to push more new product combinations to this group.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6814eea7b8ea820e40ccde096b39134e) </span>(\*The above figure is for reference only)


* **Upload positive and negative sample populations to mine label features**. Upload positive sample populations (i.e., repurchase populations) and negative sample populations (i.e., non\-repurchase populations) through the CDP multidimensional feature analysis function, calculate and obtain multidimensional feature analysis reports, mine the label combinations that best fit the characteristics of the repurchase populations, further develop relevant coupon marketing activities, and promote the target audience.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5fa395e45ba2c7ec3aa7c7e6c35ff3a7) </span>(\*The above figure is for reference only)

<span id="第五步：策略执行，多渠道触达目标群体"></span>
### Step Five: Strategy Execution, Multi\-channel Targeting

After formulating the strategy, it is equally important to reach the target audience through multiple channels more quickly and intelligently.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5cebe8bf3e38eed2d27079d63c2f898e) </span>


* Select the audience: in the CDP grouping module, select the opportunity audience package that was circled just now, and efficiently reach them through GMP.

* Select channels: APP push/SMS/mini programs/site messages/pop\-ups/telemarketing/emails, etc.

* Select materials: script templates/H5/graphic materials, etc.

* Select Timing: Scheduled Touchpoints/Routine Touchpoints/Event Triggered/Event Combination Strategy, etc.


<span id="第六步：追踪并分析关键指标变化，验收效果"></span>
### Step Six: Track and analyze changes in key indicators, verify effectiveness


* **View trends in key indicators in DataWind** Focus on this group in DataWind's visual query to observe the purchase of 50 items per capita, with an average order value of 200 yuan. Analyze SMS costs and GMV returns.

* **View audience packages and label effects in CDP** Store members can analyze audience effects in the CDP audience analysis module, understanding the audience packages' conversion on different touchpoints, tasks, etc. Focus on metrics like sent UVs, reached UVs, clicked UVs, click\-through rates, etc., to assist in evaluating effectiveness.


<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b56ad5e71bc010e10645ceacf10d1d71) </span>(\*The above data is for illustration purposes only and serves as a reference)

The above scenarios fully leverage the important value of data linkage, bridging the data chains between various stages of the enterprise lifecycle, enabling data sharing between systems, facilitating rapid, efficient, and convenient data querying and application.

Users conduct in\-depth data insights based on DataWind products, identify potential issues, use attribution analysis and other product capabilities to identify key audiences. Synchronize this information to VeCDP for insights into this group, achieve refined operations through VeCDP+GMP, and finally track and analyze changes in key indicators based on VeCDP+DataWind to verify effectiveness. Continuously iterate operational strategies, truly achieve intelligent insights leading to decision\-making and execution loops, and drive business growth with data.

<span id="_3-3-相关功能介绍"></span>
## 3.3 Introduction to Related Functions


|**Product Capabilities** |**Function Introduction** |**Product related** |
|---|---|---|
|Intelligent Attribution Analysis |[BI tools deeply analyze data to discover potential issues](https://www.volcengine.com/docs/4726/65155) |DataWind |
|Segmentation |[抽丝剥茧，锁定关键人群](https://docs.byteplus.com/docs/undefined/672484e558c46e0316c899fe) |CDP |
|User Insights |[洞察关键人群画像特征，制定运营策略](https://docs.byteplus.com/docs/undefined/672484e558c46e0316c899d1) |CDP |
|Multidimensional Feature Analysis |[上传正负样本，挖掘标签显著特征](https://docs.byteplus.com/docs/undefined/672484e558c46e0316c899ec) |CDP、DataWind |
|User Reach |[策略执行，多渠道触达目标群体](https://docs.byteplus.com/docs/undefined/672484e558c46e0316c898e1) |GMP |
|Effect Analysis |[追踪并分析关键指标变化，验收效果](https://docs.byteplus.com/docs/undefined/672484e558c46e0316c8995b) |CDP、DataWind |
