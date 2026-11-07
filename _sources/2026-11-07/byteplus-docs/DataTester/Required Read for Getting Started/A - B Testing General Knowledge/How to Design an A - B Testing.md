---
title: "How to Design an A/B Testing"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/How-to-Design-an-A-B-Testing"
---

Before you learn how to design an experiment, read:[How to Start an A/B Testing](https://docs.byteplus.com/docs/DataTester/How-to-Start-an-A-B-Testing)

<span id="一、a-b实验流程"></span>
# 1. A/B testing process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0decea92cce44f3e8eb456e15ce4c9fa~tplv-goo7wpa0wc-image.image) </span>

<span id="二、a-b实验设计举例"></span>
# 2. Example of A/B testing Design

The following is a scenario example to show **how to analyze and breakdown a business problem, set the optimization direction, evaluate the metrics and design an A/B experiment to verify the effect.** 

<span id="【业务背景】"></span>
##  **[Business background]** 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The source of the experiment: by analyzing current business problems and proposing potential solutions, an "experimental idea" is formed.</div>


**Background:**  This product is an automotive App product, and the App login rate is found to be low. The problem is located through the conversion funnel to trigger the login rate to be too low, which affects the opportunity of personalized service.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62f31f00a9fc491b9131bb014533511f~tplv-goo7wpa0wc-image.image) </span>

According to the above analysis, an instant idea is to increase the trigger login rate, that is, to add more login entries for unlogged users. Then there are two problems:


* Where to add the entrance?

* In what form is the entrance added?


In response to the first problem, it is necessary to locate the main traffic destinations of currently unlogged users, and it is best to add login entries to these main traffic fields. Existing functions that can be used without logging in include but are not limited to: follow, like, enter the live stream, save and release draft, view the browsing history, etc. By analyzing the behavioral path of unlogged users through the user path, it is found that there is a lot of web\-traffic in scenarios such as following, liking, and viewing history. It is suggested to add login guidance to these sections.

<span id="【实验目标】"></span>
## [Experiment Objectives]

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Objective:</strong> Clarify the business goals that the "experimental idea" ultimately achieves, and develop measurement metrics according to the goals.</div>


<div data-tips="true" data-tips-type="tip"><strong>Metrics:</strong> Success criteria used to evaluate the achievement of goals. And it needs to be demonstrated that it was achieved because of the application of an experimental strategy, so the metrics and strategies must have clear business causality</div>


<div data-tips="true" data-tips-type="tip">At this point, a complete <strong>"experimental hypothesis"</strong> is formed: it is expected that through xxx improvement, metric A can be increased by n%, thus bringing xxxx value to the product/users.</div>


**Goal:**  Improve login rate and better serve users without affecting the user experience of unlogged\-in users.

**Metrics:**  login rate

**Experimental hypothesis:**  By trying different guidance methods at each entrance, the metric "login rate" can be improved by n%, so as to serve users well.

<span id="【实验设计】"></span>
## [Experiment design]

The current mainstream login guidance from weak to strong: non\-blocking pop\-up/overlay guidance, half\-screen/full\-screen panel guidance, full\-screen panel forced login. For different entries, you can experiment with different login guidance methods.


|Experimental mode |Client side programming experiment |
|---|---|
|Experimental audience |All users, without any filtering |
|Web\-traffic size |According to the calculation of the sample size calculator, there are huge differences in different products and business forms. To be on the safe side, the order of magnitude exceeds 10,000 in a single group. |
|Experiment duration |14 days or more |
|Experimental version |Control group: Online style<br><br>Full screen panel forced login<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8d8180eed404d2380d860fcb734f771~tplv-goo7wpa0wc-image.image) </span> |
||Experimental Group: New Style<br><br>Half\-screen panel boot, add boot instructions<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4987e00aa97341b18d96d3af14ab6bc9~tplv-goo7wpa0wc-image.image) </span> |
|Monitor metrics |Core metrics: login rate |
||Follow metrics: conversion rate of login triggering, login submission, and login success |
|Evaluation ideas |* The login rate is the success metric<br><br>   * A significant increase indicates that the plan is effective and can be directly launched.<br><br>   * A significant decrease indicates that the program has a negative impact, and further disaggregation of the data is required to analyze the reasons.<br><br>   * No significant change means that there is no obvious effect. You can analyze the cause by disassembling the data of user segmentation and product categories. If sensitive groups or sensitive categories with significant changes are found, you can further apply strategies for experiments. |
