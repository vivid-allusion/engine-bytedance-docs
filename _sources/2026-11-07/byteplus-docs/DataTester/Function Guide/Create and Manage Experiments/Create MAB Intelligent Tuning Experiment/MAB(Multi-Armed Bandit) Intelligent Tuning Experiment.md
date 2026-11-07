---
title: "MAB(Multi-Armed Bandit) Intelligent Tuning Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/MAB-Multi-Armed-Bandit-Intelligent-Tuning-Experiment"
---

An intelligent tuning experiment is a type of experiment that sequentially evaluates the performance of experimental data and adaptively directs traffic to a better version of the experiment. Among them, the adaptive evaluation and tuning algorithm is mainly MAB (Multi\-Armed Bandit). This article introduces DataTester's MAB intelligent tuning experimental application scenarios and key points for creation.

<span id="二-应用场景"></span>
# Application scenario

<span id="_1-传统ab的弊端"></span>
## The disadvantages of traditional AB

Traditional A/B experiments rely on statistically significant classical hypothesis tests to allocate corresponding traffic to the control and experimental versions, but it is generally not allowed to change the traffic for each subversion during the experiment. Therefore, this type of experiment has several drawbacks. Firstly, it is necessary to reserve a certain period of time (at least 7 days) for regular experiments. For some urgent needs, it is difficult to meet such harsh conditions. Secondly, it is necessary to have enough samples to enter the experiment in order to obtain significant results.

<span id="_2-智能调优实验的应用场景和优势"></span>
## Application scenarios and advantages of intelligent tuning experiments

> Purpose of the experiment: The index has the highest benefit and the experimental cost is the smallest



|Scenario |Intelligent tuning experiment |A/B experiment |
|---|---|---|
|High\-value traffic: The opportunity cost of lost conversions is high, such as online sales of large\-value goods (cars, diamonds, etc.), and each lost conversion will result in a loss of thousands/tens of thousands of dollars. |Dynamically adjust the flow, find the current version with better effect in time according to the experimental results, and reduce the flow and loss of the version with poor conversion effect |The goal is to get a statistically significant solution: AB testing can get a robust, statistically significant winning solution faster when time and opportunity cost allow, although losing some conversions in the process. |
|Short activity cycle: For example, the entire cycle of many e\-commerce activities is only one or two days. If the traditional AB method generally takes more than 7 days, the activity cannot provide enough time for A/B experiments |The core goal of MAB is to optimize the whole activity, not to help customers find the optimal group, and there is no requirement for the experimental time limit |Sufficient time is required, generally at least 7 days, excluding time variables |
|Optimization goals are highly effective: for example, the optimization tests of headlines, thumbnails, video content, etc., need to obtain the maximum number of clicks within a short window period. |MAB can periodically query the conversion effect of each version, and the tuning frequency can be customized. At present, the shortest can reach half an hour |Weak real\-time: you need to wait until the end of the experiment time or after the traffic is exhausted to produce statistical results |
|Continuous optimization: Multiple elements can be added or subtracted from variants at any time during the MAB optimization process, such as adjusting the elements being tested on the interface when the interface MAB is turned on |MAB has no strict requirements for flow/experimental variants, and can switch between experimental flow and elements of experimental variants during tuning |When deep data analytics is needed, AB testing the data collected is more suitable for multi\-dimensional analysis of the data at the time of the experiment or after the experiment to see how different segments of the population react to the variables tested. For MAB, the underperforming group may not have enough data to perform these tasks. |
|Small traffic: For startups or cold starts, there may not be enough traffic to experiment |MAB will perform dynamic allocation based on the current metric, so in principle, the MAB process can maximize the traffic revenue when the total traffic is not much (Note: the essence is a compromise solution to optimize the revenue in the case of less traffic, which does not mean that the same effect can be achieved by using less traffic than AB testing). |If you want to learn some lessons from all variants (especially the worse variants):the AB testing to some extent to ensure that each variant has enough traffic to count and calculate the confidence level, if you want to measure how bad the worse variant is, so as to guide business decisions, choose AB testing. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If it is necessary to take the overall traffic revenue and decide the merits of the solution, Tester will provide a comprehensive solution that mixes MAB and AB experiments in subsequent versions.</div>


<span id="d5de1ec1"></span>
# Notes and Prerequisites


|Breakdown |Precautions in detail |
|---|---|
|Version requirement |Currently, only A/B Testing **Ultimate Edition** supports MAB Intelligent Tuning Experiment. If you want to use MAB Intelligent Tuning Experiment for experimental analysis, please make sure you have purchased A/B Testing Ultimate Edition. |
|MAB tuning effect limit |After creating the MAB tuning experiment, if the **number of users entering the group** and the **metrics** need to meet the following conditions at the same time to perform the experimental tuning normally, otherwise the experimental tuning cannot be started:<br><br><br>* Privatization 4.9.2 and later versions<br><br>   * The first round \- cold start: the number of people in each experimental group is greater than 500, and the index value of each group is greater than 0.<br><br>   * Conditions for subsequent tuning (modifying configuration values in operation) for each round: the **average new group users** between each experimental group round are greater than 50, and the index value of each group is greater than 0.<br><br>* Before privatization 4.9.2<br><br>   * The number of users in the group is required: the number of participants in each experimental group exceeds 500.<br><br>   * Metric requirements:<br><br>      * The index value is greater than 0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The privatized version 4.9.0 started to support per capita metrics, for example, pv/au, sum/au.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">5.0.0 start of the privatization version, you can check whether the relevant data meets the restrictions in the experimental report:</div><br><br><br>   <div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d72bf6ef089420781587cc103e3542f~tplv-goo7wpa0wc-image.image" />   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip">The number of people entering the group and the metric value can be directly displayed in the report.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">For conversion metrics, conversion rate \* the number of people entering the group is the number of users with metric behavior.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Privatized version 500 will now support status alerts for untuned states and interrupts during tuning</div><br><br><br>   <div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/612b7eeb5d144d7ea264afde16e3c747~tplv-goo7wpa0wc-image.image" />   </div><br>    |
|Preparation |Before creating the MAB intelligent tuning experiment, you need to ensure that the administrator and R & D have completed the corresponding preparations, including group configuration and application addition. After completing the preparation work, the operator can follow the following steps to create an experiment. |


<span id="三-操作演示"></span>
# Operation demonstration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1837938aeaf645ac92d59e57f2b00741~tplv-goo7wpa0wc-image.image) </span>

<span id="四-操作说明"></span>
# **Create an intelligent tuning experiment**

After logging in and entering the A/B testing application page, select **Intelligent Optimization \> Intelligent Dynamic Tuning** in the left navigation bar of the page, enter the **tuning list** and click the **Intelligent Tuning** button in the upper right corner to enter the Create Intelligent Tuning Experiment page.

<span id="_4-1-1-输入基本信息"></span>
## **Step1 Enter basic information**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37b7c4f42cf240b9bd7c1c935e0b0fad~tplv-goo7wpa0wc-image.image) </span>


|Configuration item |Configuration instructions |
|---|---|
|**Tuning name** |Tuning name It is recommended to take the name related to the tuning content. If there is an experimental version iteration, you can add the version number suffix, so that your partner can quickly understand what the experiment is doing and which iteration version it is in. |
|**Tuning description** |The brief description of the tuning content allows project stakeholders to more clearly understand how the tuning is done and what problems to solve, and also makes it easier to view and manage the historical tuning at a glance later. |
|**Tuning scenario** |There are [Landing Page Optimization] and [APP Mini Program Optimization]. The choice of tuning scenarios will directly affect the configuration items of the experimental version in the subsequent steps of the third step of tuning \- configuring the experimental version.<br><br><br>* Select [Landing Page Optimization], there will be two tuning methods, namely "Visual Tuning" and "Multi\-Link Tuning";<br><br>* Select [APP Mini Program Optimization], and two methods of "client side tuning" and "server level tuning" will be called. |
|**Tuning direction and metrics** |Here, only one core metric can be selected. Intelligent tuning only focuses on the improvement ratio of the metric that the experimenter cares about the most. The final experimental report is also designed around this metric.<br><br>Attention:<br><br><br>* Tuning metrics cannot carry constant items, and metrics with faster feedback need to be selected, such as whether to click, whether to convert within the hourly granularity, etc.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The identification rules for constant items are as follows:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Suppose C is a constant and X is a variable item.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Then the following are all metrics with constant terms: C + X, C\-X, C \* X.   </div><br>   <br><br>* For conversion rate metrics that are only converted the next day, the current version of the algorithm will basically fail. For metrics that require a long time (e.g. more than two or more tuning cycles) to receive feedback, it is not possible to obtain timely effect data to adjust the flow, so it is not recommended to use them as tuning metrics.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Starting from the privatization 4.9.0 version, the core metrics are newly added to support the per capita category. The operator is: according to xxx, the average value of the group and the number of times the per capita group is entered.</div><br> |
|**Tuning time** |The default is 7 days, and the upper limit is 60 days. |
|**Experiment leader** |Default is the experiment creator. |


<span id="_4-1-2-设置生效策略"></span>
## **Step2 Set the effective policy**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1cc5a0b628f24ccc955b76d844e951de~tplv-goo7wpa0wc-image.image) </span>


|Configuration item |Configuration instructions |
|---|---|
|**Traffic settings** |Control the total flow involved in tuning, the system defaults to 100%.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In each tuning frequency, the average traffic per group should not be less than 500, otherwise the system will wait until it has accumulated enough samples to start tuning.</div><br> |
|**User audience rules** |Objects involved in tuning can be controlled by filtering user properties and importing clusters |
|**Experience consistency** |Entering the group but not leaving the group guarantees that users participating in the tuning will enter the same experimental version every time. |
|**Tuning frequency settings** |Support users to set the tuning frequency, the current range can be set is [0.5h, 24h]. |


<span id="_4-1-3-配置实验版本"></span>
## **Step3 Configuration experimental version**

The configuration of the experimental version here depends on the settings of the tuning scene and tuning method in [Enter Basic Information] in the first step of the experiment:


* Key differences from normal experimental configurations

   
   |Experimental version configuration reference | |
   |---|---|
   |Experimental version |The MAB experimental version no longer distinguishes between the experimental version and the control version, and identifies different experimental versions through version 1 and version 2. |
   |Traffic allocation |MAB Experiment supports custom setup of traffic allocation buttons.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c390d812fc7e4666b7a65a3db384a890~tplv-goo7wpa0wc-image.image) </span><br><br><br>* **Custom settings** not turned on: Traffic allocation only shows the proportion of **assessed traffic** and **intelligently tuned traffic** overall.<br><br>   * The evaluation traffic is given 3% of the traffic by default for each version, and this part of the traffic is used for algorithm tuning and revenue calculation.<br><br>   * The remaining traffic is given to intelligent tuning and distributed evenly according to the number of versions. If the remainder exceeds one decimal place, it is processed according to the back\-end logic.<br><br>* **Custom Settings** When turned on: You can manually set the comment traffic intelligent traffic initial settings. |
   

* For other configuration parameters similar to the general experimental configuration, please refer to the configuration documentation of the general experimental configuration.

   
   |Tuning scenario |Tuning method |Experimental version configuration reference |
   |---|---|---|
   |Landing page optimization |Visual tuning |[Visual Experiment](https://docs.byteplus.com/docs/DataTester/120779) |
   |Landing page optimization |Multi\-link tuning |[Multi-Link Experiment](https://docs.byteplus.com/docs/DataTester/120803) |
   |APP Mini Program Optimization |Client side tuning/server level tuning |[Programming Experiment](https://docs.byteplus.com/docs/DataTester/120774) |
   


<span id="_4-2-开启实验"></span>
# Start the experiment


|Product example diagram |Operation item description |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2915b648b7c4ba89decece859005170~tplv-goo7wpa0wc-image.image) </span> |Click on the experiment details page to start the experiment. |
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ef4f02ab44d476f8fc19e99521228b7~tplv-goo7wpa0wc-image.image) </span> |Click "Start" to tune the list page. |


<span id="a67fddcd"></span>
# Support adjusting the experimental version during the experiment

MAB experiment \- **APP Mini Program optimization experiment \- experience consistency off, that is,**  support for adding and reducing versions during the experiment process, and also support adjusting the release parameters of the experimental version. This function is suitable for scenarios where the experiment is online for a long time, and it is hoped that the parameters of the released version can be adjusted during the experiment.

> For example, I hope to make a long\-term selection of app banners. At the beginning of the experiment, there are only three versions to compare. During the process, poor banners will be eliminated or new banners will be added to participate in traffic tuning according to data performance.


<span id="51728db0"></span>
## Precautions


* This feature is only suitable for scenarios where the experience is inconsistent. Currently supports client side/server level tuning in the APP Mini Program, available when experience consistency is turned off.

* The privatized 4.9.2 version starts to support modifying the experimental version of the MAB experiment and configuring parameters such as the number of custom cold start rounds. Privatized 5.0.1 version has improved this function, and it is recommended to enable this function in 5.0.1 and later versions.


<span id="2bf43049"></span>
## Operation steps

<span id="b3495682"></span>
### Enable function

To enable this function, in addition to configuring the experiment, you also need to add mab_arm attribute to the event public attribute, and correctly report the parameter information in the event related to the metric calculation. You need to manually report the event attribute in the event related to the exposure event and the tuning metric, and the attribute value is the corresponding configuration value issued by the shunt, otherwise the incoming group and metrics will not be counted.

> Example: The experiment is a poster horse racing experiment, and each version takes the poster's identification parameters (such as: postid) as the goal of traffic tuning. Then you need to report postid to the mab_arm.


<span id="5da9c31b"></span>
### **New experiment**


|**Operation** |**Schematic diagram** |
|---|---|
|Enter basic information<br><br>**Experiment Scenario Selection: APP/Mini Program Optimization** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a40cbd2fb840475f9e297f17736fd28d~tplv-goo7wpa0wc-image.image) </span> |
|Set effective policy<br><br>Experience Consistency: **Close**<br><br>> Remarks: Since the adjustment of the parameters issued by the experiment is allowed during the experimental process, the consistency of the experiment cannot be guaranteed (that is, the user always experiences the same set of issued parameters), so the adjustment of parameters can be supported when experiencing the consistency level |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/398307ca14434d57801b581a0a1f8121~tplv-goo7wpa0wc-image.image) </span> |
|Configure the experimental version<br><br>During the experiment, the number of configured versions cannot be increased or decreased, so you need to reserve enough experimental versions in advance (that is, the number of versions online at the same time), and the versions that do not need to be used can be reserved and not released.<br><br>Reserved version configuration:<br><br>When there are more than 3 initial releases, you can set a version as a reserved version and adjust it during the experiment.<br><br>The number of versions distributed at the same time shall not be less than 2<br><br>Tuning parameter configuration:<br><br>In the case of experience inconsistency, the tuning modeling is changed from the original version modeling to the delivery parameter modeling, and the tuning parameters need to be specified when multi\-parameter delivery.<br><br>Tuning parameters do not support JSON types.<br><br>Note: If there is only one parameter, there is no need to configure the tuning parameters (hiding is unrealistic) |Reserved version configuration<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65c5977311d2489688e9470758769737~tplv-goo7wpa0wc-image.image) </span><br><br>Tuning parameters and traffic configuration<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6751a75c943943bdb7d6887397f35a3d~tplv-goo7wpa0wc-image.image) </span><br><br>Note: If there is only one parameter, there is no need to configure tuning parameters |


<span id="b550a00d"></span>
### **Editing experiment**


|**Operation** |**Schematic diagram** |
|---|---|
|For the ongoing experiment, click Edit to edit the released version of the experiment. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/755bb62a67dc48b88ad76e2081d47b4d~tplv-goo7wpa0wc-image.image) </span> |
|**Edit the released version**<br><br>The previously reserved version can be closed, and the version parameters can be issued after going online.<br><br>This version will enter the cold start process (cold start traffic is the average traffic of the online version)<br><br>**Edit delivery parameters**<br><br>Allow the released version to adjust the released parameters<br><br>After the initial parameter is adjusted, the corresponding version will enter the cold start process (re\-accumulate data for tuning, and the cold start traffic is the average traffic of the online version) |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8b66637439c4b218bda16c0ade3a3e0~tplv-goo7wpa0wc-image.image) </span> |
|**Traffic configuration**<br><br>The traffic allocation changes when the following operations are performed:<br><br><br>1. **Reserved version, open \-\- \> close**<br><br><br>Traffic: Enter the cold start, and the cold start traffic ratio is the average traffic of the online version<br><br><br>2. **Reserved version, close \-\- \> clock in**<br><br><br>Flow: Adjust to 0, and the original flow will be recycled.<br><br><br>3. **Send parameter changes**<br><br><br>Traffic: The version with changed parameters re\-enters cold start, and the cold start traffic ratio is the average traffic of the online version.<br><br>**The remaining versions:** <br><br>During the traffic adjustment process, the traffic allocation ratio before adjustment is maintained between versions that have not entered the cold start. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0447f2cc13c04c06975325440d652339~tplv-goo7wpa0wc-image.image) </span> |
|**Save reminder**<br><br>When saving, a pop\-up window confirmation reminder will be made, prompting the adjustment of the released version, parameter adjustment and the configuration of the cold start traffic after adjustment after this editing. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cae2e95882e43cfa4e23b09f9f389f7~tplv-goo7wpa0wc-image.image) </span> |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The function upgrade of the privatized 4.9.2 version is not compatible with the MAB experiment of conversion rate metrics. Therefore, before upgrading the version to the 4.9.2 version, the experiment of conversion rate metrics is recommended to stop first, and then restart the experiment after upgrading to the 4.9.2 version. If it doesn't stop, it will enter the cold start logic of the new model, which will have some impact on the experimental effect. No effect on off\-line MAB experiments.</div>


* <div data-tips="true" data-tips-type="warning">Modify the value of the experimental parameters configured by the experimental version of the running MAB experiment, the metric data and data improvement ratio in the experimental report will no longer be trusted, and the traffic allocation part in the report will still be trusted.</div>



<span id="五-实验报告"></span>
# View the experimental report

After the experiment is opened, you can also click to enter the experimental report page through the experimental operation entrance in the experimental list to view the experimental report, and the MAB experimental report can be viewed: [Overview of Intelligent Traffic Tuning (MAB) Reports](https://docs.byteplus.com/docs/DataTester/120828).

Report reading for non\-experience consistency scenarios can be viewed [Interpretation of MAB Experiment Report: Non-Experiential Consistency Scenarios](https://docs.byteplus.com/docs/DataTester/120821).
