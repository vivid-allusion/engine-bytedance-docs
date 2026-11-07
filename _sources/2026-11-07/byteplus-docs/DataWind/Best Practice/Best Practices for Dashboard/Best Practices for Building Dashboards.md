---
title: "Best Practices for Building Dashboards"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Best_Practices_for_Building_Dashboards"
---

[Dashboard Overview](https://docs.byteplus.com/docs/DataWind/Dashboard_Overview) is the presentation of data analysis results. It conveys effective data information and business insights to readers, making the business landscape clearer and more intuitive, helping readers identify key metrics, and accelerating decision\-making.

Given the inherent value of dashboards, building a clear and usable data dashboard is crucial. A dashboard overloaded with information and poor design not only fails to convey useful information, but may also make the data even harder to understand than before.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e8d4ecbe91a4016afc488b2523ec41d~tplv-goo7wpa0wc-image.image) </span>


---



<span id="_1-概述"></span>
# 1. Overview

This article will guide you step by step in building a "good\-looking" data dashboard.

**However, before that, it is necessary to explore one question: What does "good\-looking" mean ❓ ❓ ❓** 

> "Good\-looking" can be understood from two perspectives. The first is easy to understand, which means presenting the full picture of metrics clearly and accurately, so that readers can understand the data at first glance without spending time and effort to interpret it. The second is aesthetically pleasing and elegant (good\-looking), that is, using a well\-structured and harmonious page to attract the reader's attention and keep them engaged with the dashboard for as long as possible.


Therefore, the key to creating a successful dashboard mainly lies in the following three aspects:

<span id="_1-1-讲好故事（tell-a-good-story）"></span>
## 1.1 Tell a good story

A good data dashboard can connect data to business and answer the viewer's questions. The viewer can accurately and quickly receive and understand the business meaning of the data, gaining insights into the current business situation.

Therefore, the first key to a successful dashboard is whether it has a good storyline.

<span id="_1-2-摆好数据（present-convincing-data）"></span>
## 1.2 Present convincing data

A data dashboard usually contains ten or more charts, and each chart contains a large amount of data. Deciding in what format each chart should be presented and in what units each data point should be displayed are all issues that need to be considered when presenting convincing data.

Using a line chart to visualize fluctuations in sales revenue over time makes the data more vivid, and displaying large sales revenue figures with unit suffixes is more intuitive than showing raw numbers. Therefore, arranging data properly is crucial for improving the readability of a data dashboard and enhancing the efficiency of information delivery.

<span id="_1-3-做好设计（deliver-a-nice-design）"></span>
## 1.3 Deliver a good design

Just as people rely on clothes and horses rely on saddles, appearance matters. To make a dashboard stand out, great design is of utmost importance!

In data visualization projects, design principles are highly valued. With strong design, a data dashboard can skillfully use layout and typography to highlight the core narrative, quickly convey effective business information to readers, and bring data and business to life.

<span id="_2-内容与结构篇"></span>
# 2. Content and structure section

Suppose you are an analyst for an education product. The customer success manager contacts you today, hoping you can create a dashboard to help them understand the key metrics of all online courses, in order to assess current user satisfaction and identify potential issues with the online courses.

After receiving this task, how should you design this dashboard?

The reader's role + The information the reader wants to see = The story the dashboard needs to tell

Specifically, this can be divided into the following two steps.

<span id="_2-1-明确看板阅读者角色（who-to-present）"></span>
## 2.1 Identify the dashboard reader's role (who to present)

Users in different roles have different requirements for data dashboards. For example, enterprise executives focus more on key metrics, the gap between targets and current status, and major business risks; while business leaders focus more on profit growth, the sales funnel, abnormal business performance, and hope to monitor the core KPIs of their department staff.

Different roles have different data needs within the dashboard. Only by identifying the target audience can the content of the dashboard be further determined.

<span id="_2-2-确定呈现的数据内容（what-to-present）"></span>
## 2.2 Determine the data to present (what to present)

After clarifying the roles of readers, we can confirm data requirements through research or even interviews (for example: which metrics are needed for which dimensions?). This work is not only reflected in the initial stage of dashboard setup, but is also crucial during dashboard maintenance. Understanding what data everyone wants to see, and continuously updating based on the evolving needs of dashboard readers, is very important.

<span id="_2-3-精雕深层的数据细节（reader-stratification）"></span>
## 2.3 Deep data details (reader stratification)

Each dashboard may have multiple readers, and different users have varying requirements for data granularity. To support readers in more flexible data exploration, present information at different levels, and enable users to independently extract deeper insights, dashboard creators should appropriately embed interactions such as drill up and drill down, multi\-table linkage, chart navigation, and intelligent attribution to enhance the reader experience.

> To learn more about interactive features, click here to view

> [Drill Up and Drill Down](https://docs.byteplus.com/docs/DataWind/Drill_Up_and_Drill_Down)

> [Chart Linkage](https://docs.byteplus.com/docs/DataWind/Chart_Linkage)

> [Chart Redirect](https://docs.byteplus.com/docs/DataWind/Chart_Redirect)

> [Intelligent Attribution](https://docs.byteplus.com/docs/DataWind/Intelligent_Attribution)


<span id="_3-图表与数据篇"></span>
# 3. Charts and data

Now you have determined the charts within the dashboard, but the dashboard still appears unremarkable, and the data within the charts remains difficult to interpret.

You may find that the issue lies in the choice of charts and the presentation of data. But how can you make the business significance represented by the data vivid and three\-dimensional, truly stand out?

<span id="_3-1-选对图表类型"></span>
## 3.1 Select the right chart type

As the saying goes, "**One** picture is worth a thousand words." The presentation of a data analysis dashboard is always based on charts, and choosing the right chart allows you to convey accurate information to readers more quickly. However, BI products offer a wide variety of chart types, each suited to different application scenarios. How should we choose charts to display our data?

Usually, based on the structure of the data to be displayed, charts can be divided into four main types: comparison, relationship, composition, and distribution/geography. On this basis, combine the data variables to determine which chart type is more appropriate.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e99cb34a4024b5fbbfa69dc243226ae~tplv-goo7wpa0wc-image.image) </span>

Here we have prepared examples of chart types supported by the product and their common application scenarios for your reference.


|**Chart name** |**Application scenarios** |**Common application examples** |
|---|---|---|
|[Table](https://docs.byteplus.com/docs/DataWind/Table)/[Pivot Table](https://docs.byteplus.com/docs/DataWind/Pivot_Table)/[Raw-Data Table](https://docs.byteplus.com/docs/DataWind/Raw-Data_Table) |Display statistical or detailed data in a table |View product sales revenue, cost, and profit for each region, channel, and primary category, with clear and detailed data presentation required |
|[Column Chart](https://docs.byteplus.com/docs/DataWind/Column_Chart)/[Bar Chart](https://docs.byteplus.com/docs/DataWind/Bar_Chart) |Display metric values for different categories |View product sales revenue under each category, sorted from high to low<br><br>View product sales revenue under each category for different channels |
|[Line Chart](https://docs.byteplus.com/docs/DataWind/Line_Chart) |Display metric trends over time |View the monthly income trend, sorted in chronological order |
|[Area Chart](https://docs.byteplus.com/docs/DataWind/Area_Chart) |Display changes in metric values over time for different categories |View monthly sales revenue for each channel<br><br>Use a percentage area chart to view changes in the proportion of monthly sales revenue for each channel |
|[Dual-Axis Chart](https://docs.byteplus.com/docs/DataWind/Dual-Axis_Chart) |Use different chart types and Y\-axis ranges to display two sets of metrics with large differences in value ranges |View daily income, and display the day\-over\-day change on the secondary axis<br><br>View income (in millions) and sales volume (in units of ten thousand) for each category |
|[Pie Chart](https://docs.byteplus.com/docs/DataWind/Pie_Chart) |Display the proportion of different categories |View each channel's share of total sales revenue |
|[Map](https://docs.byteplus.com/docs/DataWind/Map) |Display geographic information data for provinces or countries |Use color to view the distribution of sales revenue across provinces |
|[Bi-Directional Bar Chart](https://docs.byteplus.com/docs/DataWind/Bi-Directional_Bar_Chart) |Compare two metrics under the same dimension |View sales revenue and sales volume for each channel |
|[Combo Chart](https://docs.byteplus.com/docs/DataWind/Combo_Chart) |Display charts of the same dimension together |View combined sales revenue, cost, and profit for each channel |
|[Scatter Plot](https://docs.byteplus.com/docs/DataWind/Scatter_Plot) |Display the relationship between two continuous data sets, typically showing how one metric affects another |View the relationship between sales revenue and selling price<br><br>View the relationship between total profit and selling price |
|[Word Cloud](https://docs.byteplus.com/docs/DataWind/Word_Cloud) |Display large amounts of text data, typically used to describe keywords or tags |View the video tag word cloud, weighting tags by the number of videos and centering and highlighting those with more videos |
|[Histogram](https://docs.byteplus.com/docs/DataWind/Histogram) |Display data distribution and frequency of data in different intervals |View the price distribution of manufacturer A's product over the past year |
|[Measure Card](https://docs.byteplus.com/docs/DataWind/Measure_Card) |Directly display metric values, usually core metrics |View total DAU |
|[Funnel Map](https://docs.byteplus.com/docs/DataWind/Funnel_Map) |Display data funnel |View the conversion funnel for homepage visits, video views, and likes, including the number of users and conversion rates |
|[Radar Chart](https://docs.byteplus.com/docs/DataWind/Radar_Chart) |Display multidimensional evaluation scores |View the category interest scores of the user group who purchased product A<br><br>View the scores for profitability, productivity, liquidity, safety, and growth of a certain department |
|[Sankey Diagram](https://docs.byteplus.com/docs/DataWind/Sankey_Diagram) |Display traffic distribution or data flow under different dimensions |View the distribution of new users across different channels, campaigns, and regions<br><br>View the redirection situation from a certain app to other products<br><br>View the sources of customer acquisition for a certain app's superior, superior's superior, and superior's superior's superior |


<span id="_3-2-巧用数据配置"></span>
## 3.2 Making effective use of data configuration

Selecting the chart type does not mean the main task is accomplished. Chart titles, units, legends, and labels all greatly assist users in interpreting data, and the data format in the plotting area especially contains hidden nuances. The product provides several data configuration options. Flexibly using these features is very helpful for accurately displaying data characteristics and highlighting data hierarchy.

**Data format**

Data configuration within charts is a core factor affecting how readers understand chart information. Dashboard configurators should consider the following aspects to make data more intuitive and prominent.


* **Field name**: For field names that are easily confused, may be unclear, or are system\-generated derivative fields, it is recommended to set aliases or field information to improve readability and reduce dashboard maintenance costs.

   For example, change 'date' to 'outbound date' to clarify the action associated with the date; change the system\-generated field display name 'sales amount difference percentage\-1M' to 'sales amount month\-over\-month', making the name more consistent with readers' habits.

   For the detailed user manual on alias management, see: [Set Field Value Aliases](https://docs.byteplus.com/docs/DataWind/Set_Field_Value_Aliases).

* **Field value**: Setting the field format is equally crucial. For instance, '500 million' is much easier to understand and less prone to misinterpretation than '5,000,123,345'. In chart design, units, formats, and prefixes or suffixes should be set based on the business meaning of the data itself. For example, for sales amount data, add units such as yuan or US dollars as suffixes; for growth rates, proportions, and similar data, set the data format to percentage.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21c5af9ac8e742e898eed190bd3c2b0c~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Conditional formatting**

Icon sets, color scales, and data bars are common types of conditional formatting that can enhance visual effects in data. Using conditional formatting makes it easier to compare metric values within a specified range simultaneously.


* Icon sets: Icon sets provide a more intuitive way to categorize and display data. Icons are displayed based on threshold ranges, allowing readers to quickly group data by size.

* Color scales: Color scales help readers better understand the distribution of data. After setting color scales, values will display gradient colors from high to low. For scenarios with outliers or custom color scales, you can configure the maximum and minimum values as needed.

* Data bars: Data bars help readers compare metric values and identify larger or smaller values. The longer the data bar, the greater the value; the shorter the data bar, the smaller the value.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6caf862dbb8641788b42b6c2453322ba~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5ebe845d731445397d19373f34c2eba~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a81843c5f7b4a288d5c28bb9865a5bf~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b694dc8f1174a9db00b1fbf60df2688~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65a9d0b272e74982ac34f36d3a3ca30e~tplv-goo7wpa0wc-image.image) </span>

**Analysis features:** 


* Sorting and TopN settings: Set the default sorting for specific data items. Use the sorting component to highlight data that readers are most interested in. The sorting feature component provided by the product supports sorting the horizontal axis, vertical axis, and dimension fields within charts.

* Statistic item settings (total, percentage, and so on): Specify which data to perform secondary statistics on. Display statistical items to compare detailed data with statistical data, helping readers understand data characteristics and gain business insights.

* Reference line settings: To make data charts clearer and easier to understand, it is common to add reference lines such as target lines, control lines, and average lines to assist with analysis.


**Table styles**

Tables are popular among report creators because they clearly present a large number of dimensions and metric summaries. However, due to the large amount of data in tables, optimizing table configuration to highlight key information while displaying large datasets is crucial. Here are a few simple tips for designing table styles.


* The background color of a cell and its content must have sufficient contrast: it is recommended to use text colors that stand out clearly against the dashboard background. To assist users in reading, zebra striping can be used to improve browsing speed.

* Avoid using dark or thick borders to prevent borders from drawing too much attention.

* Highlight key data points, which can be combined with conditional formatting features.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be93efe82869417ba8709f24bff32cae~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-3-更多交互配置"></span>
## 3.3 More interactive configurations

How can the dashboard be made "dynamic" to meet the needs of different users for viewing data at various levels of granularity? Make effective use of both filters and dynamic dimension indicators to enhance the analytical flexibility for dashboard viewers.

**Filters**

The filtering feature helps readers quickly filter charts and view the required data. For example, in a retail sales data dashboard, store managers in different cities may want to quickly focus on their own region or even their specific store to view the performance data for that part of the business.

When configuring filters for a dashboard, pay special attention to the following points:


* Filter item settings: that is, which dimensions need to be added as filters and from which perspectives readers typically want to query the data. Setting filter items requires a high level of business understanding. If you are unsure, consider consulting several business stakeholders, as they may have the answers.

* Default query time: set the default query time for the dashboard so that viewers see the latest data as soon as they enter.

* Other edge cases to consider: removing extreme data values, limiting the time range, handling cases where no data is returned, and more. These types of data need to be excluded or transformed based on the business scenario.

* Learn more about filters[Dimension Filtering](https://docs.byteplus.com/docs/DataWind/Dimension_Filtering), [Metric Filtering](https://docs.byteplus.com/docs/DataWind/Metric_Filtering), and [Filtering](https://docs.byteplus.com/docs/DataWind/Filtering).


**Dynamic dimension indicators**

Want to analyze the same indicator from multiple dimensions freely? Want to see the performance of multiple indicators under a single dimension? Different users may care about different indicators, and creating a separate chart for each is inefficient and takes up space.

At this point, you can try the dynamic dimension/dynamic metric feature, using filters to switch analysis dimensions and metrics to meet the needs of different viewers for analyzing different dimensions and metrics.

For more information about dynamic dimensions and metrics[Best Practices for Building Dashboards](https://docs.byteplus.com/docs/DataWind/Best_Practices_for_Building_Dashboards) and [Filtering](https://docs.byteplus.com/docs/DataWind/Filtering).

<span id="_4-设计与排版"></span>
# 4. Design and layout

In the field of design, there is a concept called **cognitive load**, which refers to the cost required to effectively convey information in a work to the reader. An excellent visualization can quickly eliminate redundant chart information and deliver sufficient information to the reader's brain through visual channels in a short time, completing data transmission.

This section will focus on common data analysis optimization approaches such as design, layout, and chart color schemes.

<span id="_4-1-基础设计原则"></span>
## 4.1 Basic design principles

(1) **Contrast:** 

Highlight differences through contrast.

Common types of contrast include contrast in shape, size, and color.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20745e88f6af4cf98e65274ecc337312~tplv-goo7wpa0wc-image.image) </span>

(2) **Repetition:** 

Achieve consistency among dashboard components through repetition, enhancing visual effect.

Common forms of repetition include repeating icons within a page, repeating charts within a page, and repeating structures across pages.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d56b4ebdf5504a2eabf80e3d0369db8c~tplv-goo7wpa0wc-image.image) </span>

(3) **Alignment:** 

Use alignment to make elements consistent, connected, and clarify their relationships.

Common alignment methods include left alignment, center alignment, and right alignment. It is generally not recommended to mix multiple alignment methods on the same page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a20ea79e0c24177a32a2c745d276240~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">On the dashboard editing page, when dragging components, the system automatically displays alignment lines</div>


(4) **Proximity:** 

By grouping chart components, placing similar elements close together, and separating different elements, users are visually guided to perceive differences in proximity between elements.

By applying the principle of proximity, simply grouping elements of the same hierarchy and separating them using color, background, or configuration will result in automatic visual grouping.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e33b6bc5540f4ad99a10d10fd96a7b13~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-常见排版设计"></span>
## 4.2 Common layout designs

As a specific technique in graphic design, layout essentially deals with the relationships among elements on the canvas.

> Elements on the canvas include composition, color, font, and more.

> The relationship refers to the distance between elements, their size and area, color combinations, and so on.


A successful layout design can fully leverage design principles, balance the relationships between elements, reduce the reader's cognitive load, and enhance the readability of the work. The following two types of layout are commonly used in data analysis dashboards.

(1)**Container\-based layout method**

Group content\-related elements together, wrap the elements in a container, and adjust the formatting.

The container\-based layout method first requires clarifying the correlation between elements, then, following the principle of proximity and separation, placing related elements together and keeping unrelated elements apart. By segmenting and separating the layout, the page becomes more intuitive and clear. When the page is organized into sections with a clear structure, the entire layout appears flexible and elegant.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f6a17aafc2640fd9d7c7876f20a9a65~tplv-goo7wpa0wc-image.image) </span>

In dashboard editing, lowering the background color opacity of a text component can achieve the mask effect shown above.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3829c0f3d8744534834c09656cd5e41d~tplv-goo7wpa0wc-image.image) </span>

(2)**Split\-screen layout method**

Use color blocks to divide the background into N sub\-screens, with each screen serving as a container that can carry a type of information.

The split\-screen layout serves two purposes:

> (1) To modularize the presentation of information, reducing the audience's cognitive load.

> (2) To significantly increase the visual richness of the page and enhance its visual effect.


The split\-screen layout can usually be combined with the container\-based layout, using background color blocks to achieve the split\-screen effect. Additionally, users can achieve split screens through dividers, color contrast, and product features such as tab pages or sheet pages.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c676600b54a4f16903c827f92a90aef~tplv-goo7wpa0wc-image.image) </span>

Tab pages allow for more organized data folding and preview. For details, click [Operations in the Multi-Page Editing Area at the Bottom of the Dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Multi-Page_Editing_Area_at_the_Bottom_of_the_Dashboard).

<span id="_4-3-图标与颜色"></span>
## 4.3 Icons and colors

Whether a dashboard looks attractive and professional often depends on this!

Exquisite icons make the dashboard more refined, and outstanding color schemes make the dashboard more vivid and rich.

**Icons**

A dashboard typically contains various types of charts, a large amount of numbers, and text, and the sheer volume of information can easily cause customers to lose focus. Bright\-colored icons serve as the finishing touch that draws customers' attention. Proper use of icons can significantly reduce users' cognitive load and improve reading efficiency.

For analysts who pursue perfection, some icons are also essential to showcase the dashboard's excellence in the details. Try adding your company's logo and your department's slogan to the template to create a unique and impressive dashboard!

For more resources, you can click [this address](https://www.iconfont.cn/?lang=en-us).

**Color**

The colors of the charts should be closely related to the overall color scheme. When the dashboard uses a dark background, highly saturated charts will stand out even more. In addition, many charts can use gradients in the details to make the visuals richer, and text shadow details can also enhance the overall visual quality.

A harmonious and well\-coordinated color scheme can help the dashboard tell its story more effectively. For example, when analyzing changes in sales volume year\-over\-year and month\-over\-month, you can use a consistent red\-green color scheme to represent increases and decreases in sales volume, respectively.

**Basic knowledge of color schemes:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54d2720659d44fe1a20b14dda02bac85~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71ffa85b9b804de181c6adedcf607471~tplv-goo7wpa0wc-image.image) </span>

**General color scheme:** 

**Primary color + secondary color + accent color Primary color (usually accounts for 75%)** 


* Primary color (usually accounts for 50%)

   * The main color of the entire work, which affects the overall visual impression of the dashboard;

* Secondary color (usually accounts for 20%)

   * Helps the primary color establish a more complete image, making the dashboard harmonious or lively;

* Accent color (usually accounts for 5%)

   * Guides and highlights specific content, emphasizing key points.


**Steps for color matching:** 

**Determine the color scheme based on the content; determine the primary, secondary, and accent colors based on the theme; try not to use more than four colors.** 


* Ways to present the primary color:

   * Large area and high purity; or slightly smaller area but the most prominent color in the visual; dual primary colors are also possible.

* Use of secondary colors:

   * You can use analogous colors of the primary color to make the visuals unified and harmonious. You can also use a contrasting color to the primary color to make the visual more lively and stable.

* Characteristics of accent colors:

   * Frequent appearance; vibrant colors; strong contrast with other colors, which can highlight key elements.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/512740a9984b4a27a0b8a636c221e13c~tplv-goo7wpa0wc-image.image" width="618px" />   </div>
   


For an [excellent article](https://colorhunt.co/) on color matching, click to reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Dashboard editing supports users entering RGBA values for precise color adjustment</div>


<span id="_5-写在最后"></span>
# 5. Final remarks

Attractive appearances are common, but interesting souls are rare. The creation of dashboards for data analysis is similar; telling a good story is the core priority. Therefore, after creating a dashboard, remember to collect feedback from frontline readers and iterate continuously.

To quickly learn how to build a clear and visually appealing dashboard, join our learning course and make progress together.

**60\-minute introduction to intelligent data insight products**


* 30\-day free trial opportunity, click to activate, [Free Trial](https://docs.byteplus.com/docs/DataWind/Free_Trial).

* Complete the course to receive a ByteDance exclusive certificate and a premium gift package

* Systematic organization of key concepts, learn to get started with BI tools from scratch

* Detailed instructional guidance, step\-by\-step teaching to help you complete the following business sales analysis report


**Registration address:**  [Volcano Engine Digital Intelligence Platform Learning Center](https://docs.byteplus.com/docs/DataWind/Volcano_Engine_Digital_Intelligence_Platform_Learning_Center).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/267b81472f284a6a8598d2a03ad5a273~tplv-goo7wpa0wc-image.image) </span>
