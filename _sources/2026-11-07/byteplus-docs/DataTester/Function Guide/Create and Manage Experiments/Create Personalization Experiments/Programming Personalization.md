---
title: "Programming Personalization"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Programming-Personalization"
---

Personalization refers to the user's behavior, interests, geographic location and other information, **to provide users with personalized content and experience**, in order to improve user satisfaction and conversion rate. DataTester supports the creation of personalized experiments. This article shows you the steps to create a programmed personalized experiment.

<span id="955091b6"></span>
# Usage restrictions


* Function activation: If you want to use programming personalized experiments, you can contact the A/B testing technical support staff to apply for a whitelist trial.

* Experiment type: server side/client side


<span id="2c96cc50"></span>
# Create personalized experiments

<span id="504bd871"></span>
## Preparation

Similar to a normal A/B experiment, before creating a personalized experiment, complete the following preparations:


* Complete the data access operation according to the experimental requirements.

* According to the experimental plan, the experimental metrics are clear, and it is recommended to create the experimental metrics in advance.


<span id="c7c41fb0"></span>
## Step1: Go to the personalized experiment page

After logging in and entering the A/B test console, select **Personalization** \> **Programming Personalization** in the left navigation bar of the page, enter the **Programming Personalization List** and click the  **+ Programming Personalization** button in the upper right corner to enter the creation page.

<span id="2887a81c"></span>
## Step2: Configure personalized experimental parameters


1. Configure basic information for personalized experiments.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64e39966410343ac9c5e6621aa82f313~tplv-goo7wpa0wc-image.image) </span>

   
   |Configuration item |Configuration instructions |
   |---|---|
   |**Personalized name** |Suggest a name associated with personalized content, such as version number + content. It is convenient for other relevant personnel to quickly understand what this personalized experiment is doing and in which iteration. |
   |**Type** |Support for selecting **server side**or **client side** experiment types. |
   |**Person in charge** |The default is the personalized experiment creator. |
   

2. Configure personalized policies.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed3d842077494f978a3ec14ea7d839c6~tplv-goo7wpa0wc-image.image) </span>

   
   |Configuration item |Configuration instructions |
   |---|---|
   |Traffic layer |* Select the traffic layer for the programmed personalization experiment, and a new traffic layer is automatically created by default.<br><br>* You can also choose to **manually select** one of the traffic tiers you have created. |
   |Traffic layer traffic |Configuration programming personalization experiments require a reserved traffic layer for the traffic share. Reserved traffic refers to the percentage of users who should see your original page, at least 5%. |
   |Control flow ratio |Control traffic used to do personalized global control groups, global control metrics can be presented.<br><br>Actual control flow = flow layer flow \* comparison flow ratio |
   

3. Add personalized observation metrics.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a782745bbcae4887a6e3720e4e7c5434~tplv-goo7wpa0wc-image.image) </span>

   * Support check Add observation metric in the metric list.

   * If there is no metric required for experimentation in the drop\-down box selected by the metric, you can click New metric at the top right to jump to the Create metric page to create it; for the selected metric, you can also click the link button after the metric to jump to the metric group details page to view the details.

4. Click **Save** to go to the Experiment Builder page to continue with the steps for creating a personalized experiment.


<span id="97993c55"></span>
## Step3: Create an experimental strategy

Support to create multiple experimental strategies for programming personalized experiments. The operation steps are similar. The following is an example of creating an experimental strategy to introduce the detailed operation steps for you.


1. In the Personalization Canvas tab, click Add Experiment Policy in the Canvas.


Create the first experiment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e28ae6eb9e824f0eac1fe3d48bec3a3c~tplv-goo7wpa0wc-image.image) </span>

Create multiple experiments

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1614c4b16cdd41c8a68dd565d35c8a7e~tplv-goo7wpa0wc-image.image) </span>


2. Configure the basic information parameters of the experiment.

   
   |Configuration item |Configuration instructions |
   |---|---|
   |**Name** & **Description** |Suggest a name related to the experimental content, such as version number + content. |
   |**Duration** |The default is 7 days, and the custom valid period is set to a maximum of 365 days. You can also choose whether to set it to be valid for a long time as needed. |
   

3. Configure the experiment take effect policy.

   Only users who meet this audience rule can see the experiment. If no conditions are provided, this experiment will be shown to all users who visit your website.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/300a8615e9d84ec68f489585d69fe594~tplv-goo7wpa0wc-image.image) </span>

   * Add and conditions, or conditions: You can control who participates in personalization experiments by filtering **user attributes** (client side) or **server side filtering parameters (server side)** .

   * Add cluster (client side support): You can control users participating in personalized experiments by filtering **user clusters**.

4. Configure experimental version information for personalized experiments.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bf06368d846427a944fb866ece250b2~tplv-goo7wpa0wc-image.image) </span>

   1. You can choose whether the version of the personalized experiment is a multi\-experimental version or a single version according to the actual experimental needs.

      * Multi\-experimental version: The default is multi\-experimental version, you can add multiple experimental versions by clicking the  **+ Add Experimental Version** button below.

      * Single version: Only one experimental version.

   2. Configure the corresponding version type and version parameters of the experimental version on each experimental version page.

      
      |Configuration item |Configuration instructions |
      |---|---|
      |**Version Name** & **Description** |Set the version name and description used to quickly identify experimental and control versions, such as version number + content. |
      |**Test user** |Add test whitelist users for subsequent experimental debugging, support:<br><br><br>* Manually enter the ssid of the whitelisted user, supporting multiple entries, separated by commas.<br><br>* You can also select a whitelist group that has been created to support multiple selections. |
      |**Parameter configuration** |Add experimental parameters for each experimental version. |
      |**Traffic allocation** |Configure the user flow distribution of the control group and the experimental group to support uniform distribution, or manually adjust the flow distribution ratio after closing the uniform distribution switch. |
      

5. Click **Create and go to Debugging** to return to the Programming Personalization Experiment Canvas page.

   The added whitelist users can check the page status of the corresponding version to confirm whether the configuration of the sub\-experiment meets expectations. If it meets expectations, you can officially start a personalized experiment according to the plan.


<span id="a6582b4f"></span>
# Start/end personalized experiments

The personalized experiment that meets the expectations has been debugged. You can start the experiment on demand, and you can also stop the corresponding personalized experiment according to the experimental situation after starting.


* You can start/stop the corresponding personalized experiment on the experiment list page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9eb9c970245406da857e2f71e4ae9bb~tplv-goo7wpa0wc-image.image) </span>

* You can also enter the experiment builder for personalized experiments, where you can turn on/off the entire personality experiment, or just one of its sub\-experiments.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/854c8c0292c843d99ed8f66e811d57b5~tplv-goo7wpa0wc-image.image) </span>


<span id="db1668f6"></span>
# View personalized experiment reports

After the experiment starts, you can enter the report page of the personalized experiment, view the metric results of the personalized experiment and other information, and make business adjustments in combination with the personalized experiment report.

<span id="fa6a212c"></span>
## Overview of the report

Personalization is more concerned with the absolute optimal solution, that is, the overall personalized overall optimal solution. Personalization overview is the most important among the core metrics.


* When Personalization is selected, the report displays:

   (1) Overall overview

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d04b613f492b42018637e9d5c08e8fb3~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f91de4ac994745fa899b6010d25cf6fc~tplv-goo7wpa0wc-image.image) </span>

   (2) Experimental trends

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8b330a4ad414932a3c7ef0c7d6357d0~tplv-goo7wpa0wc-image.image) </span>

* Show when switching to an experiment:

   (1) Overview of personalized experimental data

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65bd91b57adb45b48ddd734da8bdf71b~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/802f6e28fbc74f3a93a9a9436743f850~tplv-goo7wpa0wc-image.image) </span>

   (2) Experimental trends

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a30b712cde3425db2977a4c8beefdf2~tplv-goo7wpa0wc-image.image) </span>


<span id="2ed67b8f"></span>
## Date filter

Support day level, range: personalized start date, to T\-1. For example, personalization is turned on in 20250615. If we query in 20250714, the optional range is: 20250615 \- 20250713.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7454c5d20d97411ba5d7c430a871afdb~tplv-goo7wpa0wc-image.image" width="500px" /></div>


<span id="138069c9"></span>
# Reference: Integration Considerations

Since the implementation logic of the personalized programming experiment is similar to that of the parent\-child experiment, after the personalized experiment configuration is completed:


* In the General Overview of the Use of Personalized Experiments page, the actual query is for incoming data similar to the "parent experiment".

* In the configuration page of the Get Canvas Experiment, the configuration information of the "child experiment" is actually obtained, not the configuration information of the "parent experiment".


Therefore, for personalized experiments, you need to manually obtain the configuration information of the "parent experiment" when integrating the SDK, which can be configured and used during SDK integration.


1. Get the variantKey for the "parent experiment" on the following page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/672c3657742442468b0500729aa22ede~tplv-goo7wpa0wc-image.image) </span>

2. When experimenting with SDK integration, before obtaining the configuration of the "sub\-experiment" (that is, the experiment in the canvas), obtain the configuration information found above once to expose the parent experiment.

   Taking Java SDK as an example, the `activate`method is called only once, and the `variantKey`of the parameter is the `key`obtained above, and the result does not need to be processed. For details, please refer to: [Java SDK](https://docs.byteplus.com/docs/DataTester/Java-SDK).
