---
title: "Dashboard Openness"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Dashboard_Openness"
---

<span id="ac7d7a7a"></span>
# Attention and limitations

<span id="1e1187ae"></span>
## Embedded out precautions


* Dashboard embedded in this way requires the current account to be logged in. When not logged in, you need to log in to BytePlus first, and then open the Dashboard embedded page.

* When using custom permissions, no account is required to be logged in. If the embedded environment requires custom permissions, please check < [DataFinder Dashboard Analysis Integration Solution ](https://bytedance.feishu.cn/docx/S2j3dCy6KoA2VXx19WrcZm9Nn5e)\> first.


<span id="568bbc7e"></span>
## Supported embedded chart types


* SaaS domestic version: supports embedding charts under the BytePlus domain name, such as growth analysis under other applications and the URL address of each product page;

* SaaS overseas version: support embedding charts under byteplus domain name;


That is, when embedding an external Dashboard, it supports embedding the Dashboard of the current environment portal environment domain name. If it is another domain name, you need to configure a whitelist for that domain name before embedding it.

<span id="_1-看板和图表嵌出"></span>
# 1. Dashboards and diagrams are embedded out

<span id="_1-1-看板和图表嵌出说明"></span>
## 1.1 Dashboards and diagrams embedding instructions

Dashboard and chart embedding refers to embedding DataFinder's Dashboard boards/charts into external platforms, such as reporting platforms, Lark documents, or your company's own business systems. Through this ability, you will get a link belonging to the Dashboard/chart. For users with a Dashboard/chart permission account, they can view the embedded Dashboard/chart directly on the external platform through this link.

<span id="_1-2-看板和图表嵌出操作"></span>
## 1.2 Dashboard and chart embedding operations

<span id="_1-2-1-看板嵌出"></span>
### 1.2.1 Dashboard embedding


* Enter the Dashboard board that needs to be subscribed. After clicking "..." in the upper right corner and pulling down, you can see "Embedded";

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0039827f2bdc404e967784bcf280ed6b~tplv-goo7wpa0wc-image.image) </span>

* After the pop\-up Dashboard interface is embedded, you can make the settings you need:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dafe83992c424f16afe591e30a70dcc0~tplv-goo7wpa0wc-image.image) </span>

   Support selecting to configure [Dashboard title, Dashboard operation area, Dashboard layout], as follows:

   1. Hide Dashboard Title: When checked, the Dashboard name is not displayed.

   2. Hide Dashboard operation area: Hide the [Filter Configuration, Refresh, Edit Dashboard] function after checking.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Contains resident filters.      </div>
      

* Schematic diagram of embedded Dashboard effect

   Note that the embedded Dashboard/chart still needs to verify whether the current user has Dashboard permissions, and users without permissions cannot view it.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f233edf3656544f995ab02dc06f872a4~tplv-goo7wpa0wc-image.image" width="539px" /></div>


<span id="_1-2-2-图表嵌出"></span>
### 1.2.2 Chart embedded


* Select the chart you want to embed. After clicking "..." in the upper right corner, you can see "Embed Chart".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/760ea15291684ecda8dc2d87bcf26e74~tplv-goo7wpa0wc-image.image) </span>

* After the pop\-up Dashboard interface is embedded, you can make the settings you need: you can choose whether to "hide the chart title and operation area".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adaeb03ea5914f60a352a7be7b460cc7~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-图表嵌入"></span>
# **2. Chart embedding**


1. Click the **Edit** button in the upper right corner to enter the Dashboard editing page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f40a89ee75cb4e77b10c68978999967e~tplv-goo7wpa0wc-image.image) </span>

2. Click **Embed Chart** at the top of the Dashboard Edit page to add the chart/Dashboard under the Volcano domain name to the "Current Dashboard".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3397259134324582a6ee9f26b0fc96a0~tplv-goo7wpa0wc-image.image) </span>

3. Enter the chart name and URL, save the chart and embed it in the Dashboard board. Exists as a chart after embedding, supports editing url & name and chart deletion.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/655df1d5f9074ad4a6ee9c40926a7226~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d2bcec36d5a4572b4750cc78443ad0f~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-创建a-b实验指标与优化计划"></span>
# **3.**  Create A/B experimental indicators and optimization plans

Core metrics of business concern, such as login rate and conversion rate, are also experimental metrics used frequently. When we find that core metrics are low, business personnel typically perform functional optimization to increase user conversion rates. Therefore, in order to more conveniently support the creation of experiments, DataFinder allows customers to select the indicators (charts) of interest in the Dashboard module, and create A/B experimental indicators or A/B optimization plans with the same indicator logic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This feature is only available to users who are also purchasing Growth Analytics & A/B Testing.</div>


* <div data-tips="true" data-tips-type="tip">Privatized version v4.1.0 (inclusive) is now supported.</div>



<span id="_3-1-操作说明"></span>
## Operation entrance


* Click **More** \> **Create Experimental Metrics** / **Create Optimization Plan** in the upper right corner of the Dashboard board.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/709c36a0ad624572a1a7a7b230b0404e~tplv-goo7wpa0wc-image.image) </span>

* After selecting the chart, click **Confirm**.

   Only charts created by event analysis, retention analysis, and conversion analysis are supported (up to 6 charts).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/057011ea6bbc4223b743676acf474f86~tplv-goo7wpa0wc-image.image) </span>


<span id="df96f8b7"></span>
## Create experimental metrics


1. Select the desired metrics Click **OK** to save the metrics as [A/B Test Metrics].

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b54b17edfa94be089ad15c30f9baeff~tplv-goo7wpa0wc-image.image) </span>

2. Create a successful jump to A/B test and support adding filter conditions and configurations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/529d8c28add440e2960b5995cf3676b1~tplv-goo7wpa0wc-image.image) </span>


<span id="0ae466d1"></span>
## Create an optimization plan


1. Select Metrics Create as "A/B Test Metrics"

2. Select the chart and configure **Success Metrics** , **Guardrail Metrics** , click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f426ac506244d47be330120486eb5a7~tplv-goo7wpa0wc-image.image) </span>

3. Create a successful jump to the A/B optimization plan and fill in the optimization plan content.
