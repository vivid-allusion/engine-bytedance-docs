---
title: "[Case] Automotive User Intention Label Prediction"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Case_Automotive_User_Intention_Label_Prediction"
---

<span id="62b3d9b1"></span>
## I. Overview

Automotive marketing has a wealth of intention recommendation scenarios, such as the common optional package intention recommendation, led car purchase intention anticipation, replacement/maintenance intention, combined with the management of the user's whole life cycle, to take different marketing strategies for different life cycles:

For users without perception: car brand/model introduction, learning to drive knowledge push


* Learn to drive users: car brand/model introduction, car purchase needs understanding, car learning knowledge, car purchase knowledge

* Users who plan to buy a car: car brand/model introduction, car buying time, car buying budget, intention model push, car purchase knowledge, car discount promotion

* Buying users: car brand/model introduction, car buying time, car buying budget, intention model push, car purchase knowledge, car discount promotion, capital retention

* Users who just bought a car: car brand/model introduction, car buying time, brand model, car promotions, capital retention, car purchase knowledge

* Old car owners: car brand/model introduction, repurchase and exchange needs, car purchase budget, intended car brand, exchange and retention, car knowledge, preferential activities


This case is aimed at the scenario of planned car purchase/upcoming car purchase/old car owner, using machine learning to calculate the user's car purchase intention, using the user data of successful marketing car purchase/exchange retained in history to train, and to predict the purchase intention of users who meet the three life cycles, and adopt appropriate marketing methods

<span id="74ad3329"></span>
## II. Modeling process

<span id="ea419443"></span>
### 1. Data description


|field name |field type |Field meaning |Field description |
|---|---|---|---|
|uid |bigint |user id |*  |
|gender |string |Gender |Gender: male, female |
|age |string |age group |Age group: 18\-23, 24\-30, 31\-40, 41\-50, 51\- |
|area |string |resident |Resident \- District |
|lifestage |string |Life stage |Life stages: marriage, preparation, pregnancy, childbearing |
|education |string |Education |Education: high school or below, college, bachelor's degree, master's degree or above |
|job |string |occupation |Occupation: international students, doctors, lawyers, teachers, blue\-collar workers, white\-collar workers, and others |
|birthday |string |birthday |birthday |
|lifecycle |string |Life Cycle |Lifecycle: fans, leads, owners, attrition |
|own_store |string |Affiliated store |Store: Central Guanghui, Pudong Yongda, Others |
|own_sales |string |Responsible for sales |Responsible for sales: Dawson, Wang Ning, Robert |
|wanted_store |string |Intended distributor: |Intentional distributors: Pudong Yongda, Zhonghuan Guanghui |
|wanted_carmodel |string |Intended model |Intended model: RX5 Plus, ER6, RX3, i5, i6, iMAX8, unknown |
|rank |string |Intent rating |Intent rating: high, medium, low, closed |
|lasttime_pudongyongda_testdrive |string |Last store test drive time |Last store test drive time: within 1 week, within 2 weeks, within 1 month, within 2 months, within 3 months, within half a year, within one year |
|newcar_tasting |string |New car tasting |New Car Tasting Session: Yes, No |
|storetimes_lastthreemonth |string |Number of visits to dealers in the past three months |Number of visits to dealers in the past 3 months: 0, 1, 2, 3, 4, \> 4 |
|storenumbers_lastthreemonth |string |Number of dealers visited in the past three months |Number of dealers visited in the past 3 months: 0, 1, 2, 3, 4, \> 4 |
|warranty_times |int |Number of visits during the quality assurance period |Number of visits during the quality assurance period: 0, 1, 2, 3, 4, 5 |
|warranty_values |string |Total service value during the quality assurance period |Total service value during the quality assurance period: 0~ 3000, 3000~ 5000, 5000~ 10000, \> 10000 |
|pudongyongda_noentry_time |string |Duration of not entering our store |Duration of not entering our store (Pudong Yongda): 1 month, 2 months, 3 months, 4 months, 5 months, 6 months, 7 months, 8 months, 9 months, 10 months, 11 months, 12 months |
|forwardtimes_lastthreemonth |string |Cumulative forwarding in the past 3 months |Cumulative forwarding in the past 3 months: < 3, 3~ 5, 6~ 10, \> 10 |
|publishtimes_lastmonth |string |Number of posts in the past month |Number of posts in the past month: 0, 1, 2, 3, 4, \> 4 |
|applets_opentimes_lastmonth |int |Number of Mini Programs opened in the past month |Number of Mini Programs opened in the past month |
|optionalpackpage_opentimes_lastmonth |int |The number of times the optional package page has been opened in the past month |The number of times the optional package page has been opened in the past month |
|optionalpackpage_time_lastmonth |int |The browsing time of the optional package page in the past month |The browsing time of the optional package page in the past month. Unit: min |
|last_eta |int |Current eta |Current eta. Unit: day |
|eta_modifytimes |string |eta modification times |ETA modification times: 0, 1, 2, 3, 4, \> 4 |
|pointuse_lastmonth |string |Have you used your points in the past month? |Have you used your points in the past month? Yes, No |
|point_count |string |integral amount |Integral amount: 0\-500, 500\-10000, 100000\-30000, 30000 or more |
|active_lasttime |string |Last active time |Last active time |
|contact_preference |string |Touchpoint preference |Touchpoint preference |
|gift_preference |string |Boutique category preference |Boutique category preference |
|carowner |string |Owner of this product |Owner of this product |
|salescarmodel |string |This product transaction model |This product transaction model |
|salestime |string |Transaction date of this product |Transaction date of this product |
|carownerappvisit |string |Owner app access frequency |Owner app access frequency |
|othercarmodel |string |The remaining models are held |The remaining models are held |
|interest_car_price |string |Car price |Car price |
|interest_car_brand_country |string |Auto country |Auto country |
|interest_car_brand |string |Car brand |Car brand |
|interest_car_other_series_type |string |Car model |Car model |
|interest_car_newenergy_type |string |New energy type |New energy type |
|client_stage |string |customer phase |customer phase |
|channel |string |retention channel |retention channel |
|community_pv_lastweek |int |Community PV of the past week |Community PV of the past week |
|community_creation_lastweek |int |Community content creation over the past week |Community content creation over the past week |
|community_forward_lastweek |int |Community retweets from the past week |Community retweets from the past week |
|community_recruit_lastweek |int |Community updates from the past week |Community updates from the past week |
|car_optical_pack_eagerness |string |Option Pack Preference |Option Pack Preference |
|car_pick_up_eagerness |string |Pickup urgency |Pickup urgency |
|returned_customer |string |return customer |return customer |
|car_price_comparison |string |cross\-store price comparison |cross\-store price comparison |
|stored_many_points |string |Hoarding of points |Hoarding of points |
|club_freshman |string |Club newbie |Club newbie |
|recall_values |string |churn recall value |churn recall value |


The data contains most of the key indicators that have been processed by data, including the user's life cycle/active level/channel information/personal attributes, etc. Using such structured data, through simple modeling, the intention rating can be predicted, so as to carry out accurate marketing.

<span id="12462a1f"></span>
### 2. Data preparation

Hive data access, data preparation supports direct connection to hive data sources, simple data search + drag to access data, this case is divided into two pieces of data, historical manual labeled data + newly generated data, historical labeled data for intention rating classification training, new data for intention prediction.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/695f77fdc6fe4821a11efede6b1b2b39~tplv-goo7wpa0wc-image.image) </span>

<span id="fa6d0c3f"></span>
### 3. Problem modeling

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad79b58e605b4d1999df398b4d72ee1f~tplv-goo7wpa0wc-image.image) </span>

We choose the core indicators for intention training. Since we have processed the data beforehand, we can understand that all the indicators affect the choice of intention. Therefore, there is no need for feature screening/feature processing here. After simple logistic regression, the goal can be achieved

<span id="a2f447fb"></span>
### 4. Model evaluation

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/b39d0df75ea044319a0c0e3e96fdf2bc) </span>

The data preparation module supports the function of training model evaluation and assists users in manually adjusting parameters. Referring to the confusion matrix in the figure above, the recall and accuracy of the final effect of the model are displayed, and the performance of the test set is displayed under different classification conditions. At the same time, the calculation of weighted recall, weighted precision and accuracy is supported

<span id="26cd0541"></span>
### 5. Data production applications

After obtaining a better model, the predicted results can be output to hive/clickhosue, which can be combined with ABI for analysis and processing later. At the same time, it can also be connected to the CDP platform, and the indicator can be put into production for label insight/marketing application/user grouping

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/881b3de829264257b4d7a46fb61a866a~tplv-goo7wpa0wc-image.image) </span>
