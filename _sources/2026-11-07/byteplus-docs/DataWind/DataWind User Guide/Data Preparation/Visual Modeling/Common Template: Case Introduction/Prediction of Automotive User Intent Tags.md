---
title: "Prediction of Automotive User Intent Tags"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Prediction_of_Automotive_User_Intent_Tags"
---

<span id="_1-场景概述"></span>
# 1. Scenario overview

Car marketing includes a variety of intent recommendation scenarios, such as common optional package intent recommendations, potential customer car purchase intent prediction, and replacement or maintenance intent prediction. Business personnel can combine user lifecycle management to adopt different marketing strategies for user groups at different lifecycle stages, such as:


* Unaware users: car brand and model introductions, driving knowledge recommendations

* Users learning to drive: car brand and model introductions, understanding car purchase needs, driving knowledge, car purchase knowledge

* Users planning to buy a car: car brand and model introductions, car purchase timing, car purchase budget, recommendation of intended car models, car purchase knowledge, car promotion offers

* Users about to purchase a car: car brand and model introductions, car purchase timing, car purchase budget, recommendation of intended car models, car purchase knowledge, car promotion offers, lead collection

* Users who have just purchased a car: car brand and model introductions, car purchase timing, brand and model, car promotional activities, lead collection, car purchase knowledge

* Existing car owners: car brand and model introductions, repeat purchase or replacement needs, car purchase budget, intended car brands, replacement lead collection, car knowledge, promotional activities


This case focuses on the scenarios of users planning to purchase a car, users about to purchase a car, and existing car owners. It uses machine learning to infer users' car purchase intent, trains on historical data of car purchase and replacement users, predicts car purchase intent for users in these three lifecycle stages, and adopts appropriate marketing measures.

<span id="_2-建模过程"></span>
# 2. Modeling process

<span id="_2-1-数据描述"></span>
## **2.1 Data description**


|Field name |Field type |Field definition |Field description |
|---|---|---|---|
|uid |bigint |User ID |*  |
|gender |string |Gender |Gender: Male, female |
|age |string |Age group |Age group: 18\-23, 24\-30, 31\-40, 41\-50, 51 and above |
|area |string |Permanent residence |Permanent residence \- district |
|lifestage |string |Life stage |Life stage: Seeking marriage, preparing for marriage, pregnancy, have children |
|education |string |Education |Education: High school or below, associate degree, bachelor's degree, master's degree or above |
|job |string |Job |Job: International student, doctor, lawyer, teacher, blue\-collar worker, white\-collar worker, others |
|birthday |string |Birthday |Birthday |
|lifecycle |string |Lifecycle |Lifecycle: Fan, Potential customer, Car owner, Lost |
|own_store |string |Affiliated store |Affiliated store: Zhonghuan Guanghui, Pudong Yongda, Others |
|own_sales |string |Responsible Sales representative |Responsible Sales representative: Dawson, Wang Ning, Robert |
|wanted_store |string |Intended dealer: |Intended dealer: Pudong Yongda, Zhonghuan Guanghui |
|wanted_carmodel |string |Intended car model |Intended car model: RX5 Plus, ER6, RX3, i5, i6, iMAX8, Unknown |
|rank |string |Intention rating |Intention rating: High, Medium, Low, Completed |
|lasttime_pudongyongda_testdrive |string |Last store test drive time |Last store test drive time: within 1 week, within 2 weeks, within 1 month, within 2 months, within 3 months, within half a year, within one year |
|newcar_tasting |string |New car tasting event |New car tasting event: Yes, No |
|storetimes_lastthreemonth |string |Number of dealer visits in the past 3 months |Number of dealer visits in the past 3 months: 0, 1, 2, 3, 4, \>4 |
|storenumbers_lastthreemonth |string |Number of dealers visited in the past 3 months |Number of dealers visited in the past 3 months: 0, 1, 2, 3, 4, \>4 |
|warranty_times |int |Number of store visits within warranty period |Number of store visits within warranty period: 0, 1, 2, 3, 4, 5 |
|warranty_values |string |Total service value within warranty period |Total service value within warranty period: 0\-3000, 3000\-5000, 5000~10000, \>10000 |
|pudongyongda_noentry_time |string |Time not entering this store |Time not entering this store (Pudong Yongda): 1 month, 2 months, 3 months, 4 months, 5 months, 6 months, 7 months, 8 months, 9 months, 10 months, 11 months, 12 months |
|forwardtimes_lastthreemonth |string |Total forwards in the past 3 months |Total forwards in the past 3 months: <3, 3\-5, 6\-10, \>10 |
|publishtimes_lastmonth |string |Number of posts in the past month |Number of posts in the past month: 0, 1, 2, 3, 4, \>4 |
|applets_opentimes_lastmonth |int |Mini program open times in the past month |Mini program open times in the past month |
|optionalpackpage_opentimes_lastmonth |int |Optional package page open times in the past month |Optional package page open times in the past month |
|optionalpackpage_time_lastmonth |int |Optional package page browsing duration in the past month |Optional package page browsing duration in the past month. Unit: min |
|last_eta |int |Current ETA |Current ETA. Unit: days |
|eta_modifytimes |string |ETA modification times |ETA modification times: 0, 1, 2, 3, 4, \>4 |
|pointuse_lastmonth |string |Used points in the past month |Used points in the past month: Yes, No |
|point_count |string |Points amount |Points amount: 0\-500, 500\-10000, 10000\-30000, above 30000 |
|active_lasttime |string |Last active time |Last active time |
|contact_preference |string |Contact preference |Contact preference |
|gift_preference |string |Preferred premium categories |Preferred premium categories |
|carowner |string |Owner of this vehicle |Owner of this vehicle |
|salescarmodel |string |Car model sold in this transaction |Car model sold in this transaction |
|salestime |string |Transaction date of this vehicle |Transaction date of this vehicle |
|carownerappvisit |string |Car owner app visit frequency |Car owner app visit frequency |
|othercarmodel |string |Other car models owned |Other car models owned |
|interest_car_price |string |Car price |Car price |
|interest_car_brand_country |string |Car brand country of origin |Car brand country of origin |
|interest_car_brand |string |Car brand |Car brand |
|interest_car_other_series_type |string |Car model |Car model |
|interest_car_newenergy_type |string |New energy type |New energy type |
|client_stage |string |Customer stage |Customer stage |
|channel |string |Lead source channel |Lead source channel |
|community_pv_lastweek |int |Community PV in the past week |Community PV in the past week |
|community_creation_lastweek |int |Community content creation in the past week |Community content creation in the past week |
|community_forward_lastweek |int |Community shares in the past week |Community shares in the past week |
|community_recruit_lastweek |int |Community new user acquisition in the past week |Community new user acquisition in the past week |
|car_optical_pack_eagerness |string |Optional package preference |Optional package preference |
|car_pick_up_eagerness |string |Car pick\-up urgency |Car pick\-up urgency |
|returned_customer |string |Returning customer |Returning customer |
|car_price_comparison |string |Cross\-store price comparison |Cross\-store price comparison |
|stored_many_points |string |Large accumulation of points |Large accumulation of points |
|club_freshman |string |New club member |New club member |
|recall_values |string |Churn recall value |Churn recall value |


The data contains most of the key processed indicators, including user lifecycle, activity level, channel information, personal attributes, and more. By leveraging such structured data and applying straightforward modeling, it is possible to predict intent ratings and thus enable precise marketing.

<span id="_2-2-数据准备"></span>
## **2.2 Data preparation**

Data access is achieved through a direct connection to Hive data. This case involves two datasets: historical manually labeled data and newly generated data. Classification training is performed on the historical labeled data for intention rating, and intention prediction is carried out on the new data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0063692f6aa340a091a30ad333431d22~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-问题建模"></span>
## **2.3 Problem modeling**

Core indicators are selected for intention training. Since data processing has already been completed in advance, all indicators can be considered as core factors influencing the selection of intention. Therefore, there is no need for feature selection or feature processing here. The target requirements can be met through simple logistic regression.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c94fb41681442a5bf9b08bfb244aa9a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-模型评估"></span>
## **2.4 Model evaluation**

Supports model evaluation during training, assisting users with manual parameter tuning. Refer to the confusion matrix below, which shows the final recall and precision of the model, as well as the performance on the test set under different classification scenarios. It also supports the calculation of weighted recall, weighted precision, and accuracy.

<span id="_2-5-数据生产应用"></span>
## **2.5 Data production application**

After obtaining a model with satisfactory performance, the prediction results can be exported to Hive/ClickHouse. Subsequent visualization queries and dashboard creation can be performed on the DataWind platform. It can also be integrated with CDP products for tag insights, marketing applications, user segmentation, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0471a88388d044daa6cac7ff157f028d~tplv-goo7wpa0wc-image.image) </span>
