---
title: "Predict Intent Tags for Automotive Users"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Predict_Intent_Tags_for_Automotive_Users"
---

<span id="_1-场景概述"></span>
# 1. Scenario overview

Automotive marketing offers a wide range of intent recommendation scenarios, such as common optional package intent recommendations, potential customer car purchase intent prediction, and replacement or maintenance intent prediction. Business personnel can leverage user lifecycle management to adopt different marketing strategies for user groups at different lifecycle stages, for example:


* For unaware users: introduce automotive brands and models, provide driving knowledge

* Users learning to drive: introduce automotive brands and models, identify car purchase needs, provide driving knowledge and car purchase knowledge

* Users planning to buy a car: introduce automotive brands and models, car purchase timing, car purchase budget, recommend intended car models, provide car purchase knowledge, and promote automotive discounts

* Users about to purchase a car: introduce automotive brands and models, car purchase timing, car purchase budget, recommend intended car models, provide car purchase knowledge, promote automotive discounts, and collect leads

* Users who have just purchased a car: introduce automotive brands and models, car purchase timing, brand and model, automotive promotional activities, collect leads, and provide car purchase knowledge

* Existing car owners: introduce automotive brands and models, assess repurchase or replacement needs, car purchase budget, intended car brands, collect replacement leads, provide automotive knowledge, and promotional activities


This case focuses on the scenarios of users planning to purchase a car, users about to purchase a car, and existing car owners. It uses machine learning to infer users' car purchase intentions, training on historical data of users who have purchased or replaced cars, predicting purchase intent for users in these three lifecycle stages, and adopting appropriate marketing strategies.

<span id="_2-建模过程"></span>
# 2. Modeling process

<span id="_2-1-数据描述"></span>
## **2.1 Data description**


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|uid |bigint |User ID |*  |
|gender |string |Gender |Gender: Male, female |
|age |string |Age group |Age group: 18\-23, 24\-30, 31\-40, 41\-50, 51 and above |
|area |string |Permanent residence |Permanent residence \- district |
|lifestage |string |Life stage |Life stage: Seeking marriage, preparing for marriage, pregnancy, already has children |
|education |string |Education |Education: High school or below, associate degree, bachelor's degree, master's degree or above |
|job |string |Job |Job: International student, doctor, lawyer, teacher, blue\-collar, white\-collar, other |
|birthday |string |Birthday |Birthday |
|lifecycle |string |Lifecycle |Lifecycle: Fan, Potential customer, Car owner, Churned |
|own_store |string |Affiliated store |Affiliated store: Zhonghuan Guanghui, Pudong Yongda, Others |
|own_sales |string |Responsible Sales representative |Responsible Sales representative: Dawson, Wang Ning, Robert |
|wanted_store |string |Intended dealer: |Intended dealer: Pudong Yongda, Zhonghuan Guanghui |
|wanted_carmodel |string |Intended car model |Intended car model: RX5 Plus, ER6, RX3, i5, i6, iMAX8, Unknown |
|rank |string |Intention rating |Intention rating: High, Medium, Low, Completed transaction |
|lasttime_pudongyongda_testdrive |string |Last store test drive time |Last store test drive time: within 1 week, within 2 weeks, within 1 month, within 2 months, within 3 months, within half a year, within 1 year |
|newcar_tasting |string |New car tasting event |New car tasting event: Yes, No |
|storetimes_lastthreemonth |string |Dealer visits in the past three months |Dealer visits in the past three months: 0, 1, 2, 3, 4, \>4 |
|storenumbers_lastthreemonth |string |Dealers visited in the past three months |Dealers visited in the past three months: 0, 1, 2, 3, 4, \>4 |
|warranty_times |int |Store visits during warranty period |Store visits during warranty period: 0, 1, 2, 3, 4, 5 |
|warranty_values |string |Total service value during warranty period |Total service value during warranty period: 0\-3000, 3000\-5000, 5000~10000, above 10000 |
|pudongyongda_noentry_time |string |Duration since last visit to this store |Duration since last visit to this store (Pudong Yongda): 1 month, 2 months, 3 months, 4 months, 5 months, 6 months, 7 months, 8 months, 9 months, 10 months, 11 months, 12 months |
|forwardtimes_lastthreemonth |string |Total forwards in the past three months |Total forwards in the past three months: <3, 3\-5, 6\-10, \>10 |
|publishtimes_lastmonth |string |Posts published in the past month |Posts published in the past month: 0, 1, 2, 3, 4, \>4 |
|applets_opentimes_lastmonth |int |Applet open count in the past month |Applet open count in the past month |
|optionalpackpage_opentimes_lastmonth |int |Optional package page open count in the past month |Optional package page open count in the past month |
|optionalpackpage_time_lastmonth |int |Optional package page browsing duration in the past month |Optional package page browsing duration in the past month Unit: min |
|last_eta |int |Current ETA |Current ETA Unit: days |
|eta_modifytimes |string |ETA modification count |ETA modification count: 0, 1, 2, 3, 4, \>4 |
|pointuse_lastmonth |string |Used points in the past month |Used points in the past month: Yes, No |
|point_count |string |Points amount |Points amount: 0\-500, 500\-10000, 10000\-30000, above 30000 |
|active_lasttime |string |Last active time |Last active time |
|contact_preference |string |Contact preference |Contact preference |
|gift_preference |string |Gift category preference |Gift category preference |
|carowner |string |Car owner of this product |Car owner of this product |
|salescarmodel |string |Transaction car model of this product |Transaction car model of this product |
|salestime |string |Transaction date of this product |Transaction date of this product |
|carownerappvisit |string |Car owner app visit frequency |Car owner app visit frequency |
|othercarmodel |string |Other owned car models |Other owned car models |
|interest_car_price |string |Car price |Car price |
|interest_car_brand_country |string |Car brand country |Car brand country |
|interest_car_brand |string |Car brand |Car brand |
|interest_car_other_series_type |string |Car model |Car model |
|interest_car_newenergy_type |string |New energy type |New energy type |
|client_stage |string |Client stage |Client stage |
|channel |string |Lead source channel |Lead source channel |
|community_pv_lastweek |int |Community PV in the past week |Community PV in the past week |
|community_creation_lastweek |int |Community content creation in the past week |Community content creation in the past week |
|community_forward_lastweek |int |Community forwarding in the past week |Community forwarding in the past week |
|community_recruit_lastweek |int |Community recruitment in the past week |Community recruitment in the past week |
|car_optical_pack_eagerness |string |Optional package preference |Optional package preference |
|car_pick_up_eagerness |string |Car pick\-up eagerness |Car pick\-up eagerness |
|returned_customer |string |Returning customer |Returning customer |
|car_price_comparison |string |Cross\-store price comparison |Cross\-store price comparison |
|stored_many_points |string |Large points accumulation |Large points accumulation |
|club_freshman |string |Club freshman |Club freshman |
|recall_values |string |Churn recall value |Churn recall value |


The data contains most of the key processed indicators, including user lifecycle, activity level, channel information, personal attributes, and more. By leveraging such structured data and simple modeling, it is possible to predict intent ratings and thus enable precise marketing.

<span id="_2-2-数据准备"></span>
## **2.2 Data preparation**

Data ingestion is accomplished by directly connecting to hive data. This case involves two datasets: historical manually labeled data and newly generated data. The historical labeled data is used for classification training based on intention ratings, while the new data is used for intention prediction.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3708c0410504b07a502a2265e9dc246~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-问题建模"></span>
## **2.3 Problem modeling**

Select core indicators for intention training. Since data processing has already been completed in advance, it can be understood that all indicators have a core impact on the selection of intention. Therefore, there is no need for feature selection or feature processing here. Simple logistic regression is sufficient to meet the target requirements.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9116c94932d47b7ac0716c4b0c9ef4a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-模型评估"></span>
## **2.4 Model evaluation**

Support for model evaluation functionality during training is provided to assist users in manual parameter tuning. Refer to the confusion matrix below, which shows the recall and precision of the model's final performance, as well as the performance on the test set under different classification scenarios. Weighted recall, weighted precision, and accuracy calculations are also supported.

<span id="_2-5-数据生产应用"></span>
## **2.5 Data production application**

After obtaining a model with satisfactory performance, the prediction results can be exported to hive/ClickHouse. Subsequent visual queries or dashboard creation can be performed on the DataWind platform. It can also be integrated with CDP products for label insights, marketing applications, user segmentation, and many other applications.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b14d1e28bb4463898e051e51c2e84f3~tplv-goo7wpa0wc-image.image) </span>
