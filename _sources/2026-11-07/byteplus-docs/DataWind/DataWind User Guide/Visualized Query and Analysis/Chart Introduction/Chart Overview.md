---
title: "Chart Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Chart_Overview"
---

<span id="_1-图表选择"></span>
# 1. Chart selection

The presentation of data analysis dashboards is always based on charts. Selecting the right chart allows you to convey information to readers more quickly and accurately. However, BI products offer a wide variety of chart types, each suited to different scenarios. How should we choose the appropriate chart to display our data?

Typically, based on the structure of the data to be displayed, charts can be divided into four main types: comparison, relationship, composition, and distribution/geography. On this basis, by considering the data variables, you can further determine which chart type is more suitable.

<span id="_2-图表类型与常见场景"></span>
# 2. Chart types and common scenarios


|**Chart name** |**Application scenario** |**Common application examples** |
|---|---|---|
|[Table](https://docs.byteplus.com/docs/DataWind/Table)/[Pivot Table](https://docs.byteplus.com/docs/DataWind/Pivot_Table)/[Raw-Data Table](https://docs.byteplus.com/docs/DataWind/Raw-Data_Table)/[Trend Analysis Table](https://docs.byteplus.com/docs/DataWind/Trend_Analysis_Table) |Tables display statistical or detailed data, or changes in data. |View the sales amount, cost, and profit of products under each region, channel, and primary category when clear and detailed data display or observation of data changes is required. |
|[Column Chart](https://docs.byteplus.com/docs/DataWind/Column_Chart)/[Bar Chart](https://docs.byteplus.com/docs/DataWind/Bar_Chart) |Display metric values under different categories. |View the sales amount of products under each category, sorted from high to low.<br><br>View the sales amount of products under each category for different channels. |
|[Line Chart](https://docs.byteplus.com/docs/DataWind/Line_Chart) |Display metric trends over time. |View monthly revenue trends, sorted in chronological order. |
|[Area Chart](https://docs.byteplus.com/docs/DataWind/Area_Chart) |Display changes in metric values under different categories over time. |View the sales amount of each channel for each month.<br><br>Use a percentage area chart to view changes in the proportion of sales amount for each channel by month. |
|[Dual-Axis Chart](https://docs.byteplus.com/docs/DataWind/Dual-Axis_Chart) |Use different axis chart types and Y\-axis ranges to display two groups of metrics with large differences in value ranges. |View daily revenue, and display the month\-over\-month comparison on the secondary axis.<br><br>View revenue (in millions) and sales volume (in ten thousands) by category |
|[Pie Chart](https://docs.byteplus.com/docs/DataWind/Pie_Chart) |Display the proportion of different categories |View the proportion of total sales revenue by channel |
|[Map](https://docs.byteplus.com/docs/DataWind/Map) |Display geographic information data for provinces/countries |View the distribution of sales revenue across provinces using color |
|[Bi-Directional Bar Chart](https://docs.byteplus.com/docs/DataWind/Bi-Directional_Bar_Chart) |Compare two metrics under the same dimension |View sales revenue and sales volume by channel |
|[Combo Chart](https://docs.byteplus.com/docs/DataWind/Combo_Chart) |Display charts of the same dimension together |View sales revenue, cost, and profit together by channel |
|[Scatter Plot](https://docs.byteplus.com/docs/DataWind/Scatter_Plot) |Display the relationship between two continuous data points, usually the impact of one metric on another |View the relationship between sales revenue and price<br><br>View the relationship between total profit and price |
|[Word Cloud](https://docs.byteplus.com/docs/DataWind/Word_Cloud) |Display large amounts of text data, typically used to describe keywords or tags |View the video tag word cloud, measure weight by the number of videos, and highlight tags with more videos in the center |
|[Histogram](https://docs.byteplus.com/docs/DataWind/Histogram) |Display data distribution and frequency across different intervals |View the price distribution of manufacturer A's products over the past year |
|[Measure Card](https://docs.byteplus.com/docs/DataWind/Measure_Card)/[Measure Trend Chart](https://docs.byteplus.com/docs/DataWind/Measure_Trend_Chart) |Visually display metric values, usually core metrics |View total DAU |
|[Funnel Map](https://docs.byteplus.com/docs/DataWind/Funnel_Map) |Display data funnel |View the conversion funnel for homepage visitors, video viewers, and likes, including the number of users and conversion rates |
|[Radar Chart](https://docs.byteplus.com/docs/DataWind/Radar_Chart) |Display multidimensional evaluation scores |View the category interest distribution of users who purchased product A<br><br>View the scores for profitability, productivity, liquidity, safety, and growth of a department |
|[Sankey Diagram](https://docs.byteplus.com/docs/DataWind/Sankey_Diagram) |Display traffic distribution or data flow across different dimensions |View the distribution of new users by channel, campaign, and region<br><br>View the redirection from an app to other products<br><br>View the user acquisition sources for an app's direct, indirect, and tertiary referrals |
|[Progress Chart and Progress Bar](https://docs.byteplus.com/docs/DataWind/Progress_Chart_and_Progress_Bar) |Display the completion rate of metrics |Monitor the progress of KPI completion |
|[Waterfall Chart](https://docs.byteplus.com/docs/DataWind/Waterfall_Chart) |Express the quantitative relationship among several specific values |Display the structure or sequence changes of the total score |
|[Sparkline](https://docs.byteplus.com/docs/DataWind/Sparkline) |Sparklines in individual table cells |View changes in profit in the raw\-data table |
|[OKR Table](https://docs.byteplus.com/docs/DataWind/OKR_Table) |Display the completion status of objectives |View the completion rates of the monthly, quarterly, and annual targets for business metrics, progress within the current cycle, and the year\-on\-year and month\-on\-month comparisons for each metric |


<span id="_3-注意事项"></span>
# 3. Notes

(1) When there are too many legend items to render the chart, it will automatically switch to a table.

(2) The following five chart types support custom fields: table, column chart, bar chart, line chart, and area chart. At the bottom of the chart configuration area, you can enable "Custom Fields". Note: Only metric fields are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bdc656cb60f4363975341e740f86c7b~tplv-goo7wpa0wc-image.image) </span>
