---
title: "Sensitive Population Insights"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Sensitive-Population-Insights"
---

<span id="d81ff145"></span>
## 1. Function overview

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93dc80a7054b40148270859c4f52ef70~tplv-goo7wpa0wc-image.image) </span>

The sensitive population insight function is a set of intelligent insights into sensitive populations based on the Uplift Model model. It is a data analytics tool that plays a unique role in marketing, advertising, and many other fields. Unlike traditional predictive models, which focus on predicting whether events occur (e.g., whether a user purchases a product or whether a patient's condition improves), they focus on estimating the "extra boost" of an intervention on outcomes.

For example, in one experiment, the overall order conversion rate increased by 8.04%, but I hope to increase the conversion ROI and find users who are more sensitive to activities. Through the sensitive population insight analysis, the age and active level have the greatest impact on conversion, and the analysis shows that users aged 21\-30 years old with medium and high active levels have a significant increase of 15.23% in conversion rate indicators. This sub\-population is a sensitive sub\-population and can be used as the main object of activities to improve ROI.

<div style="text-align: right">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7200401a686342f08a504f4d565bf5f8~tplv-goo7wpa0wc-image.image" width="1080px" /></div>


Taking the marketing coupon scenario as an example, we plan to issue users a 10 yuan coupon to increase the purchase rate of the product. Which customers do we want to issue coupons to? We can divide our customers into four categories:


* Persuadables: Do not buy if you do not send the coupon, buy if you send the coupon;

* Sure things: It will be purchased regardless of whether the coupon is sent or not;

* Lost causes: will not be purchased regardless of whether the coupon is sent or not;

* Sleeping Dogs: If you don't send a coupon, you will buy it, but if you send a coupon, you won't buy it.


We hope to carry out strategic intervention only for those customers who do not convert without distributing coupons, but convert without distributing coupons (corresponding to: Persuadables customers). Sensitive population analysis ability is to accurately find the more **sensitive groups of people** for such interventions through the method of Uplift modeling and prediction, so that we can accurately put energy and resources on the blade to maximize benefits.

<span id="61f81ae6"></span>
## 2. Typical application scenarios


|**Scenario** |**Case** |
|---|---|
|**Marketing Promotion** |**E\-commerce retail**:<br><br>Large supermarket chains want to increase the sales of their own brand goods. In the past, they issued discount coupons, which were expensive and partially distributed to customers who would have bought them anyway. After the Uplift Model debuted, it integrated online and offline consumption data (purchase category span, purchase frequency, customer unit price, online search records, etc.), targeted those "swing customers" who wandered between competing products and private brands, browsed frequently but did not place an order, and issued targeted coupons, which not only increased sales significantly, but also saved more than x% of the marketing budget due to accurate delivery, achieving a leap in input\-output ratio |
||**Online travel platform**<br><br>Before the peak tourist season, the platform plans to promote popular destination travel packages. With the help of Uplift Model, users' past travel data (travel time preferences, accommodation grade selection, interest in play items), in\-app search collection behavior, identify users who have potential interest in a specific destination and have recently followed but not booked, push exclusive offers and personalized itinerary recommendations, the conversion rate is nearly twice that of random promotion, hotel and air ticket bookings have risen sharply, revitalizing tourism resources |
|**Financial services** |**Bank credit business**:<br><br>In expanding new credit card users and improving the active level, banks use the Uplift Model to comprehensively consider multi\-dimensional information such as user income stability, consumption habits, and existing financial product holdings. After accurately finding out the card opening gift and consumption cashback discount, they will switch from low\-frequency savings accounts to high\-frequency card consumption and high\-quality potential customers who repay on time. At the same time, the number of new user card openings increased by x% quarter\-on\-quarter, and the transaction volume of card swiping rose simultaneously. |
|**Internet Technology** |**Content Platform User Retention**:<br><br>In order to enhance user stickiness and reduce churn, the video streaming platform uses the Uplift Model to analyze user viewing history (subject matter preference, viewing time distribution), interactive behavior (likes, comments, collection frequency), login time and other data, targeting users who have signs of churn (viewing frequency decreases sharply, not logging in for a long time) but are expected to return and extend the viewing time after pushing personalized content recommendations and exclusive membership rights. Timely intervention, MAU user retention rate has increased by more than x%, and the depth and breadth of content dissemination have been expanded. |


<span id="17083aa0"></span>
## 3. Function entrance

**Path: AB test List Select an Experiment \- Data Metrics TAB \- Sensitive Population Insights**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c4fdcef2afb48dca704f2dbe9f5a5a4~tplv-goo7wpa0wc-image.image) </span>

Analysis tasks require a certain amount of incoming data and indicator transformation before they can be analyzed. Analysis task creation is not supported on the day the experiment was created.

<span id="6570a01e"></span>
## 4. Introduction to each module

<span id="eebae02c"></span>
### 4.1 Create a task

The task is to analyze "one indicator, one experimental group, one control group" in an experiment

Determine the metrics and mining direction to be analyzed, and select user attributes that may affect the metrics based on business experience, then submit the analysis task.


|**Field name** |**Description** |
|---|---|
|**Task name** |Meet the name field input specification, support Chinese and English, special symbols and length limits need to be confirmed. Empty, enter from the experimental report, and fill in the experimental name by default |
|**Experiment** |Enter from the experimental report, and bring experimental information by default |
|**Control group** |Analysis task control group |
|**Experimental group** |The experimental group on the analysis task applied a strategy of hope analysis |
|**Analytical metrics** |An analysis is only for one metric<br><br>Indicator support type: per capita indicators. |
|**Excavation direction** |**Mining direction** Positive mining refers to finding those who are more effective in improving the indicator, such as finding customers who are more likely to buy (purchase conversion rate increases); negative mining refers to finding people who are more effective in reducing the indicator, such as finding customers who are less likely to churn (attrition rate decreases) |
|**Time frame** |The time frame refers to the period of time during which users entering the experiment are used as samples for training and modeling. |
|**User attributes** |Analyze which dimensions are significant for identifying sensitive populations, and explore sensitive populations under the intersection of these dimensions |
|**Advanced Settings \- Resource Configuration** |Model training depends on resources, and the platform provides the function of resource allocation, which can be selected according to the size of the dataset.<br><br>Adaptive: The platform automatically determines which of the following configurations is selected by selecting the dataset size.<br><br>Low configuration: 8Core, 24GB<br><br>Middle configuration: resource 12Core, 40GB<br><br>High configuration: resource 16Core, 50GB |


Notes Note 1: Models require some data accumulation in order to be better modeled and analyzed. It is recommended that the number of people entering the analysis task be greater than 20,000, and the analysis dimension be greater than 4 dimensions

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d006caa5553e4d87bb7c0cd761be81ad~tplv-goo7wpa0wc-image.image) </span>

Note 2: Resource allocation reference, and estimated time


|**Number of participants (experimental and control groups)/number of user attributes** |**100,000** |**1 million** |**2.50 million +**  |**5 million** |
|---|---|---|---|---|
|**10** |**Low configuration**<br><br>About 10min |**Middle configuration**<br><br>About 15min |**Middle configuration**<br><br>About 30min |**Middle configuration**<br><br>About 1h |
|**20** |**Low configuration**<br><br>About 10min |**Middle configuration**<br><br>About 30min |**Middle configuration**<br><br>About 1h30min |**Middle configuration**<br><br>About 1h30min |
|**40** |**Low configuration**<br><br>About 10min |**Middle configuration**<br><br>About 30min |**High configuration**<br><br>About 1h30min |**High configuration**<br><br>About 2h |


<span id="69cf5682"></span>
### 4.2 Task Status

Task header tab to view task status. Divided into running, completed, error and other states.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b100ace08e5e464d83454c297e6d495d~tplv-goo7wpa0wc-image.image) </span>

For the running status, you can view the running status of the task through the task panel.

During the operation of the task, it will be divided into four stages: data preparation, model training, model prediction and result output

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5339fd7eca3478fb1378658c60eefd3~tplv-goo7wpa0wc-image.image) </span>

<span id="83481a1d"></span>
## 5. Analysis report

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a169c84f5614af8a768fe9a6b3a2c1f~tplv-goo7wpa0wc-image.image) </span>

<span id="8c305cb7"></span>
### 5.1 Overview of the report

**TOP\-sensitive population refers to the collection of significant sub\-populations that improve in line with the mining direction in the important feature cross sub\-population** .

> Note: The relative difference contribution may be negative, mainly when the experimental neatness is negative, but the excavation direction is positive, and there are positive sensitive subpopulations (and vice versa). For example, the overall click through rate of the experiment group was negative compared with the control group, but it was possible to find subgroups with better click through rate than the control group.



|**Description** |**Screenshot** |
|---|---|
|Can the sensitive population be obtained in this task, and analyze the improvement effect of the sensitive sub\-population.<br><br>At the same time, it outputs the importance of features to help businesses mine the core difference dimensions of the crowd and provide interpretability.<br><br>Overall refers to the analysis version selected by the analysis task and all users participating in the experiment during the time period.<br><br>**Sensitive population** refers to the overall population, the important characteristics of the two\-dimensional cross sub\-population is always consistent with the excavation direction, and there are significant indicators to show the collection of sub\-populations. Example: Cross subpopulation 1, cross subpopulation 2 is significant, sensitive population = cross subpopulation 1 and cross subpopulation 2 population set, add the number of people, recalculate the relative difference, absolute difference and relative difference contribution. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7610eb14ea84392b6b8a41d39e6ff36~tplv-goo7wpa0wc-image.image) </span> |


<span id="bba1fcea"></span>
### 5.2 Key characteristics of cross\-subpopulations

The important feature cross sub\-population refers to the feature based on the model analysis, taking the TOP 3 importance of the feature, and doing a 2D cross drill\-down analysis.


|**Description** |**Screenshot** |
|---|---|
|Display information:<br><br><br>1. Population ratio: the proportion of the sub\-population (including the experimental group and the control group) in the overall number of experimental participants<br><br>2. Absolute difference: the difference between the mean of the indicators in the experimental group and the mean of the indicators in the control group in this subpopulation<br><br>3. Relative difference: the difference between the mean index value of the experimental group and the mean index value of the control group in this sub\-population/the mean index value of the control group<br><br>4. Relative difference contribution: the difference between the mean value of the indicators of the experimental group and the mean value of the indicators of the control group in this sub\-population/the difference between the indicators of the overall experimental group and the mean value of the indicators of the control group<br><br>5. P\-value: The p\-value, the statistical data obtained when the null hypothesis is true (such as the difference between the mean of the two sets of sample data) will be greater than or equal to the probability of the actual observed result |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/576b9a74af8345b8a9de9403fb206709~tplv-goo7wpa0wc-image.image) </span> |


<span id="5a39e753"></span>
### 5.3 Sub\-population downloads

Through the crowd download button at the top right, the customer obtains detailed data about the user, including the following information:


|**Field** |Meaning |
|---|---|
|treatment |1 represents the experimental group selected in the task, 0 represents the control group selected in the task |
|uid |User IDs defined in the DataTester platform |
|app_id |BytePlus platform defined app_id |
|activation_channel, activation_type, p_version |Attributes selected in task analysis |
|ite |It is an \*\*\*\* abbreviation for Individual Treatment Effect, which refers to the difference in the outcome of a particular individual with some kind of intervention (Treatment) and without intervention. This value is the model predicted value. |
|bins |Based on ITE value sorting, the ITE value is divided into 10 intervals, each interval corresponds to a bins value |
|uc2 |The user id defined in the customer system (the customer can use this id to identify) |


Example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/faa6d1566d51457ea88fb4f39a0764f4~tplv-goo7wpa0wc-image.image) </span>

<span id="4dd4d95b"></span>
## 6. Description

**Recommended configuration:** 


* This function will train and infer forest models, requiring certain computing resources. For more accurate analysis results, it is recommended to configure the single instance memory to 128GB +.

   **Suggestions for use in low\-end environments:** 

* For low\-configuration environments, such as 64GB of memory, analysis may fail due to insufficient memory when processing large amounts of data, such as more than 1 million records. It is recommended to reduce the selected properties and consider increasing memory.
