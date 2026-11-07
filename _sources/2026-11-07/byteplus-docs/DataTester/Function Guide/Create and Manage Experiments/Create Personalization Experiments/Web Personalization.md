---
title: "Web Personalization"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Web-Personalization"
---

Personalization refers to the user's behavior, interests, geographic location and other information, **to provide users with personalized content and experience**, in order to improve user satisfaction and conversion rate. DataTester supports the creation of personalized experiments. This article introduces the application scenarios, advantages, and operation steps for creating personalized experiments on the Web.

<span id="cc0a2365"></span>
# Application scenario

Traditional A/B experiments have long test cycles, high costs, can not be optimized in real time, difficult to meet the individual needs of restrictions, DataTester in the privatization 4.9.0 version began to support personalized experiments, in a number of typical application scenarios, can further meet the flexible, efficient and low cost to carry out A/B experiments, the comparison is as follows.


|Application scenario |Traditional AB test pain points |Application value of personalized experiment |Advantages of personalized experimentation |
|---|---|---|---|
|**Product recommendations** for e\-commerce websites |Traditional AB test can only be tested on the entire client base, cannot meet individual needs, and cannot be tested according to different characteristics of users |Test according to the different characteristics of users. |AB personalized test can recommend different products to different users based on their historical purchase records, browsing records, search records, etc., to improve user purchase rate and satisfaction. |
|**Targeted delivery** of marketing activities |Traditional AB test require a significant investment of manpower, material resources and time costs, and for small businesses or start\-up companies, the cost of testing may exceed budget. |Reduce AB test costs. |AB personalized testing can target different users according to their geographical location, age, gender, interests and other information, and improve the click through rate and conversion rate of advertisements. |
|Social media **content recommendations** |The traditional AB testing cycle is long and cannot respond quickly to market changes. |Quickly respond to market changes. |AB personalization testing can recommend different content to different users based on their social relationships, interests, historical behaviors, etc., to improve customer engagement and retention. |
|Mobile application **function optimization** |Traditional AB testing cannot be optimized in real time and strategies cannot be adjusted in a timely manner based on test results. |Real\-time optimization and timely adjustment of strategies based on test results. |AB personalized testing can optimize the function of different users according to the user's device type, operating system version, network environment and other information, and improve the user experience and retention rate. |
|Website page **layout optimization** |The traditional AB test cannot meet individual needs and cannot be tested according to the different characteristics of users. |Test according to the different characteristics of users. |AB personalized testing can optimize the page layout for different users according to the user's device resolution, browser type, operating system and other information, and improve the user experience and conversion rate. |


<span id="e926c98e"></span>
# Usage restrictions


* Privatized version: 4.9.0 and above

* Experiment type: Only client side experiments are supported


<span id="9d06d939"></span>
# Create personalized experiments

<span id="9fd39db8"></span>
## Preparation

Similar to a normal A/B experiment, before creating a personalized experiment, complete the following preparations:


* Complete the data access operation according to the experimental requirements.

* According to the experimental plan, the experimental metrics are clear, and it is recommended to create the experimental metrics in advance.


<span id="73daef6c"></span>
## Step1: Go to the Web Personalization experiment page

After logging in and entering the A/B test console, select **Personalization** \> **Web Personalization** in the left navigation bar of the page, enter the **Web Personalization List** and click the **Create Personalization** button in the upper right corner to enter the Create page.

<span id="82de62c3"></span>
## Step2: Configure Web Personalization experimental parameters


1. Configure basic information for personalized experiments.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba1c5bee42e04fc69743c4d0b8f49eb7~tplv-goo7wpa0wc-image.image) </span>

   
   |Configuration item |Configuration instructions |
   |---|---|
   |**Personalized name** |Suggest a name associated with personalized content, such as version number + content. It is convenient for other relevant personnel to quickly understand what this personalized experiment is doing and in which iteration. |
   |**Destination URL** |* Supported matching types: URL simple matching, URL precise matching.<br><br>* URL address: The URL of a personalized web page. Including H5 page, Web page, H5 page in APP, H5 page in Mini Program.<br><br>   Note that the URL address configured here must be accessible directly through the browser, and can support pages that require login to access, or pages that require permissions to access. |
   |**Reserved traffic** |Reserved traffic refers to the percentage of users who should see your original page, at least 5%. |
   

2. Add metrics.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0f26d30e98945f4951f454a7ffc3948~tplv-goo7wpa0wc-image.image) </span>

   * Support for adding core metrics and common metrics.

      * Core metrics: Only one core metric can be selected, and the improvement ratio of the metric is the most concerned. The final experimental report is also designed primarily around this metric.

      * Ordinary metrics: multiple metrics can be configured to serve as a reference for index data other than core metrics to form experimental report metric data.

   * If there is no metric required for experimentation in the drop\-down box selected by the metric, you can click New metric at the top right to jump to the Create metric page to create it; for the selected metric, you can also click the link button after the metric to jump to the metric group details page to view the details.

3. Click **OK** to go to the Experiment Builder page to continue with the steps for creating a child experiment.


<span id="fd9fbf59"></span>
## Step3: Create sub\-experiments

Support to create multiple sub\-experiments for Web personalized experiments, with similar operation steps. The following example is to create a sub\-experiment to introduce the detailed operation steps for you.


1. Click the  **+**  sign to the right of the personalized card to add a sub\-experiment.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebbc37a7a3704c5eaba4133f90644851~tplv-goo7wpa0wc-image.image) </span>

2. Configure the basic information parameters of the sub\-experiment.

   
   |Configuration item |Configuration instructions |
   |---|---|
   |**Name** & **Description** |Suggest a name related to the experimental content, such as version number + content. |
   |**Duration** |The default is 7 days, and the maximum setting is 365 days. |
   

3. Configure the target user.

   Only users who meet this rule can see the experience. If no conditions are provided, this experience will be showcased to all users who visit your website.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51c6c13b3f5b473fbe782f47fe339f1e~tplv-goo7wpa0wc-image.image) </span>

   * Add and condition, or condition: You can control users participating in personalized experiments by filtering **user attributes**.

   * Add clustering: You can control users participating in personalized experiments by filtering **user clustering**.

4. Configure experimental version information for personalized experiments.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10bb1023760545a995328d197211d57d~tplv-goo7wpa0wc-image.image) </span>

   1. According to the interface detection result prompt, if the visual editor plug\-in is not followed, the corresponding plug\-in can be installed according to the interface prompt.

      * For personalized experiments on Web pages, you can directly edit the page to be subjected to A/B experiments through the visual editor, and save the modified page directly as the experimental version of the page, and conduct A/B comparisons with the original page to carry out experiments.

      * After installing the plug\-in for the first time, you need to refresh the operation page before continuing the subsequent operation.

   2. Click **to enter the visual editor**, enter the visual editor page, you can edit and modify the Web page through the visual editor, and click **Save** when you are done, you can save the modified page as an **experimental version** page.

   3. Configure the version parameters of the control version and the experimental version.

      The control version is the page of the original page URL of the Web personalization experiment; the experimental version is the page modified and saved by the visual editor.

      
      |Configuration item |Configuration instructions |
      |---|---|
      |**Version Name** & **Description** |Set the version name and description used to quickly identify experimental and control versions, such as version number + content. |
      |**Whitelist** |Add test whitelist users for subsequent experimental debugging, support:<br><br><br>* Manually enter the ssid of the whitelisted user, supporting multiple entries, separated by commas.<br><br>* You can also select a whitelist group that has been created to support multiple selections. |
      |**Experimental version operation record** |You can view the operation record of the current experimental version in the experimental version. In the above steps, the operation in the visual editor will be recorded and displayed here. |
      |**Traffic allocation** |Configure the user flow distribution of the control group and the experimental group to support uniform distribution, or manually adjust the flow distribution ratio after closing the uniform distribution switch. |
      

5. Click **Save and enter Debugging**, and the created sub\-experiment enters **the debugging** state.

   The added whitelist users can check the page status of the corresponding version to confirm whether the configuration of the sub\-experiment meets expectations. If it meets expectations, you can officially start a personalized experiment according to the plan.


<span id="aeae5b5b"></span>
# Start/end personalized experiments

The personalized experiment that meets the expectations has been debugged. You can start the experiment on demand, and you can also stop the corresponding personalized experiment according to the experimental situation after starting.


* You can start/stop the corresponding personalized experiment on the Web Personalized Experiment List page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07fe5b1b6f004c6c9c9d8e1f08292a6d~tplv-goo7wpa0wc-image.image) </span>

* You can also enter the experiment builder for personalized experiments, where you can turn on/off the entire personality experiment, or just one of its subexperiments.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff33ad8d073742a38a37cdbede596c81~tplv-goo7wpa0wc-image.image) </span>


<span id="e3f75ed4"></span>
# View personalized lab reports

After the experiment starts, you can enter the report page of the personalized experiment, view the metric results of the personalized experiment and other information, and make business adjustments in combination with the personalized experiment report.

<span id="2cdb8849"></span>
## Overview of the report

Personalization is more concerned with the global optimal solution, that is, the overall personalized overall optimal solution. Personalization overview is the most important among the core metrics. The card to the right of the personalization overview is the payoff of the experiment in the core metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17d9180cc76c453f89410b9d09c88164~tplv-goo7wpa0wc-image.image) </span>

Switch to experiment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd6bafd72a6245119c61da6fa123b305~tplv-goo7wpa0wc-image.image) </span>

<span id="d73c1795"></span>
## Date filter

Support day level, range: personalized start date, to T\-1. For example, personalization is turned on in 20240613. If we query in 20240621, the optional range is: 20240613 \- 20240620.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7454c5d20d97411ba5d7c430a871afdb~tplv-goo7wpa0wc-image.image" width="500px" /></div>


<span id="768d175b"></span>
## Incoming user trends

According to the date filter to see the number of users in the personalization reserved traffic and personalized traffic. If you switch to the experimental version, show the number of users in the control version and the experimental version. This graph allows you to view the trends of incoming users.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01bbf7b0510347b7b50b6b05cc14db19~tplv-goo7wpa0wc-image.image) </span>

Switch to experiment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/092fcb88fb564bf89833c663717ef1c7~tplv-goo7wpa0wc-image.image) </span>

<span id="3b7c6cad"></span>
## Metric value change

Filter and select metrics by date to see how metrics perform in personalization. By default, the core metric is selected, and you can switch to the normal metric. Select the daily change of the metric in the date range to get the daily change trend of the metric.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/890366f24b974a209f798df0b74f210f~tplv-goo7wpa0wc-image.image) </span>

Switch to experiment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fe751e1f52f4c919fcf950ee07c2674~tplv-goo7wpa0wc-image.image) </span>

<span id="9b7a208e"></span>
## P value change

Filter and select metrics by date to see the performance of metrics in personalization. The p\-value is used to indicate the size of the difference between the experimental results and the control group, that is, to determine whether the experimental results are statistically significant. The smaller the p\-value, the greater the difference, and the more significant the difference between the experimental results and the control group.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c10db7c8a6b24cf798b2748d3003f183~tplv-goo7wpa0wc-image.image) </span>

Switch to experiment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8de6b2b959b4508a041deba424ee3d6~tplv-goo7wpa0wc-image.image) </span>

<span id="80f8523e"></span>
# Common problems

<span id="9cc90f51"></span>
## Q1: What is the difference between personalization and recommendation?

Personalization and recommendations are essentially the best\-matched information delivery to the most appropriate people, but in large optimization scenarios, **recommendations are only a subset of personalization**.

Recommendation is mainly concerned with content (products, articles, etc.), while **Personalization is concerned with the entire user experience under different scenarios and needs from a macro perspective\-\-** from content, to the impact of a word on different groups of people. Recommendation, in the context of personalization, will only be used as a component, or a scene to choose. Therefore, simply **understanding recommendation as personalization is inaccurate and not comprehensive**.

<span id="78f39e61"></span>
## Q2: Differences between personalization and father\-son experiments


* **Personalization layers users, and parent\-child experiments layer experiments**.

   * Personalization experiments usually involve layering users into different groups, and then designing different experiments for different groups.

   * Parent\-child experiments typically involve stratifying the experiment into different groups, and then designing different experiments for different groups.

* Personalized hits allow for adjustment of experimental priorities.

* Run neutron experiments dynamically adjusted for the population.

* Personalized reports that demonstrate personalized overall benefits and global benefits.


<span id="2379ba5f"></span>
## Q3: What is the processing logic of the experimental layer in personalization?

Personalization corresponds to a separate layer, and each experiment added to the experiment is on top of a different layer, each layer is orthogonal.

<span id="20fa2abf"></span>
## Q4: When there are multiple sub\-experiments, how to modify the setting of the sub\-experiment hit priority?

If a user hits the audience conditions of Experiment 1 and Experiment 2 at the same time, they can prioritize the previous sub\-experiments by setting the order of the experiments, and ultimately only one version of one sub\-experiment will be hit.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d06329029c804bba8036753e9186982b~tplv-goo7wpa0wc-image.image) </span>

<span id="3282d7bb"></span>
## Q5: What is the user offloading logic in personalization?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d96fbe94c6c473a9e66b79440eb3764~tplv-goo7wpa0wc-image.image) </span>
