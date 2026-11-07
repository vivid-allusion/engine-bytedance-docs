---
title: "Prediction of Automotive User Intent Tags"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Prediction_of_Automotive_User_Intent_Tags_"
---

<span id="_1-场景概述"></span>
# 1. Scenario overview

Automotive marketing features a wide range of intent recommendation scenarios, such as common optional package intent recommendations, potential customer car purchase intent prediction, and replacement or maintenance intent prediction. Business personnel can leverage user lifecycle management to implement different marketing strategies for user groups at various lifecycle stages, for example:


* For unaware users: automotive brand/model introduction, driving knowledge push

* For users learning to drive: automotive brand/model introduction, car purchase needs understanding, driving knowledge, car purchase knowledge

* For users planning to buy a car: automotive brand/model introduction, purchase timing, purchase budget, recommended model push, car purchase knowledge, automotive discount promotion

* For users about to purchase a car: automotive brand/model introduction, purchase timing, purchase budget, recommended model push, car purchase knowledge, automotive discount promotion, lead collection

* For users who have just purchased a car: automotive brand/model introduction, purchase timing, brand/model, automotive offer promotion, lead collection, car purchase knowledge

* For existing car owners: automotive brand/model introduction, repurchase or replacement needs, purchase budget, intended car brand, replacement lead collection, automotive knowledge, offer promotion


This case focuses on scenarios involving users planning to purchase a car, users about to purchase a car, and existing car owners. It uses machine learning to infer users' car purchase intent, training on historical data from car purchase and replacement users, to predict purchase intent for users in these three lifecycle stages and implement appropriate marketing strategies.

<span id="_2-建模过程"></span>
# 2. Modeling process

<span id="_2-1-数据描述"></span>
## **2.1 Data description**


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|uid |bigint |User ID |*  |
|gender |string |Gender |Gender: male, female |
|age |string |Age group |Age group: 18\-23, 24\-30, 31\-40, 41\-50, 51\- |
|area |string |Permanent residence |Permanent residence \- area |
|lifestage |string |Life stage |Life stage: Seeking marriage, preparing for marriage, pregnancy, already have children |
|education |string |Education |Education: High school or below, associate degree, bachelor's degree, master's degree or above |
|job |string |Occupation |Occupation: International student, doctor, lawyer, teacher, blue\-collar, white\-collar, others |
|birthday |string |Birthday |Birthday |
|lifecycle |string |Lifecycle |Lifecycle: Fan, Potential customer, Car owner, Lost |
|own_store |string |Affiliated store |Affiliated store: Zhonghuan Guanghui, Pudong Yongda, Others |
|own_sales |string |Responsible sales representative |Responsible sales representative: Dawson, Wang Ning, Robert |
|wanted_store |string |Intended dealer: |Intended dealer: Pudong Yongda, Zhonghuan Guanghui |
|wanted_carmodel |string |Intended car model |Intended car model: RX5 Plus, ER6, RX3, i5, i6, iMAX8, Unknown |
|rank |string |Intention rating |Intention rating: High, Medium, Low, Completed transaction |
|lasttime_pudongyongda_testdrive |string |Last store test drive time |Last store test drive time: within 1 week, within 2 weeks, within 1 month, within 2 months, within 3 months, within half a year, within 1 year |
|newcar_tasting |string |New car appreciation event |New car appreciation event: Yes, No |
|storetimes_lastthreemonth |string |Dealer visit count in the past three months |Dealer visit count in the past three months: 0, 1, 2, 3, 4, \>4 |
|storenumbers_lastthreemonth |string |Number of dealers visited in the past three months |Number of dealers visited in the past three months: 0, 1, 2, 3, 4, \>4 |
|warranty_times |int |Store visits during warranty period |Store visits during warranty period: 0, 1, 2, 3, 4, 5 |
|warranty_values |string |Total service value during warranty period |Total service value during warranty period: 0\-3000, 3000\-5000, 5000~10000, above 10000 |
|pudongyongda_noentry_time |string |Duration not entering this store |Duration not entering this store (Pudong Yongda): 1 month, 2 months, 3 months, 4 months, 5 months, 6 months, 7 months, 8 months, 9 months, 10 months, 11 months, 12 months |
|forwardtimes_lastthreemonth |string |Total forwards in the past three months |Total forwards in the past three months: <3, 3\-5, 6\-10, \>10 |
|publishtimes_lastmonth |string |Post count in the past month |Post count in the past month: 0, 1, 2, 3, 4, \>4 |
|applets_opentimes_lastmonth |int |Mini program open count in the past month |Mini program open count in the past month |
|optionalpackpage_opentimes_lastmonth |int |Optional package page open count in the past month |Optional package page open count in the past month |
|optionalpackpage_time_lastmonth |int |Optional package page browsing duration in the past month |Optional package page browsing duration in the past month. Unit: minutes |
|last_eta |int |Current ETA |Current ETA. Unit: days |
|eta_modifytimes |string |ETA modification count |ETA modification count: 0, 1, 2, 3, 4, \>4 |
|pointuse_lastmonth |string |Whether points were used in the past month |Whether points were used in the past month: Yes, No |
|point_count |string |Points amount |Points amount: 0\-500, 500\-10000, 10000\-30000, above 30000 |
|active_lasttime |string |Last active time |Last active time |
|contact_preference |string |Contact preference |Contact preference |
|gift_preference |string |Premium category preference |Premium category preference |
|carowner |string |Car owner for this product |Car owner for this product |
|salescarmodel |string |Transaction car model for this product |Transaction car model for this product |
|salestime |string |Transaction date for this product |Transaction date for this product |
|carownerappvisit |string |Car owner app visit frequency |Car owner app visit frequency |
|othercarmodel |string |Other owned car models |Other owned car models |
|interest_car_price |string |Car price |Car price |
|interest_car_brand_country |string |Country of car brand |Country of car brand |
|interest_car_brand |string |Car brand |Car brand |
|interest_car_other_series_type |string |Car model |Car model |
|interest_car_newenergy_type |string |Type of new energy vehicle |Type of new energy vehicle |
|client_stage |string |Customer stage |Customer stage |
|channel |string |Information collection channel |Information collection channel |
|community_pv_lastweek |int |Page views in the community in the past week |Page views in the community in the past week |
|community_creation_lastweek |int |Community content generated in the past week |Community content generated in the past week |
|community_forward_lastweek |int |Community shares in the past week |Community shares in the past week |
|community_recruit_lastweek |int |Community new user acquisition in the past week |Community new user acquisition in the past week |
|car_optical_pack_eagerness |string |Optional package preference |Optional package preference |
|car_pick_up_eagerness |string |Car pick\-up urgency |Car pick\-up urgency |
|returned_customer |string |Returning customer |Returning customer |
|car_price_comparison |string |Price comparison across stores |Price comparison across stores |
|stored_many_points |string |Large point accumulation |Large point accumulation |
|club_freshman |string |Club newcomer |Club newcomer |
|recall_values |string |Churn recovery value |Churn recovery value |


The data includes most of the key processed indicators, including user lifecycle, activity level, channel information, and personal attributes. By using such structured data and applying straightforward modeling, it is possible to predict intent ratings and thus enable precise marketing.

<span id="_2-2-数据准备"></span>
## **2.2 Data preparation**

Data integration is achieved by directly connecting to Hive data. This case involves two datasets: historical manually labeled data and newly generated data. Classification training is performed on historical labeled data based on intention rating, and intention prediction is carried out on new data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3708c0410504b07a502a2265e9dc246~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-问题建模"></span>
## **2.3 Problem modeling**

Core metrics are selected for intention training. Since data processing has already been completed in advance, it can be understood that all metrics fundamentally influence the selection of intention. Therefore, there is no need for feature selection or feature processing. The target requirements can be met through simple logistic regression.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9116c94932d47b7ac0716c4b0c9ef4a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-模型评估"></span>
## **2.4 Model evaluation**

Supports model evaluation functionality for training, assisting users in manual parameter tuning. Refer to the confusion matrix below, which shows the recall and precision of the final model performance. It displays the performance on the test set under different classification scenarios, and also supports the calculation of weighted recall, weighted precision, and accuracy.

<span id="_2-5-数据生产应用"></span>
## **2.5 Data production application**

After obtaining a model with satisfactory performance, the predicted results can be exported to Hive/Clickhouse. Subsequent visualization queries and dashboard creation can be performed on the DataWind platform. It can also be integrated with CDP products for label insights, marketing applications, user segmentation, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b14d1e28bb4463898e051e51c2e84f3~tplv-goo7wpa0wc-image.image) </span>
