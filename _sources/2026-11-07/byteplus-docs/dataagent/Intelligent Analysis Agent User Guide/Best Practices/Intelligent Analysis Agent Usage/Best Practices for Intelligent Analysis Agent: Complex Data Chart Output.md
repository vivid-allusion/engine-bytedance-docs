---
title: "Best Practices for Intelligent Analysis Agent: Complex Data Chart Output"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Best_Practices_for_Intelligent_Analysis_Agent_Complex_Data_Chart_Output"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This article aims to bridge the entire process of data charts from "theoretical understanding" to "practical application," helping you master two core capabilities in one place:</div>



1. <div data-tips="true" data-tips-type="tip"><strong>Learn essential knowledge</strong>: Easily understand the principles for selecting mainstream data charts and methods for interpreting them;</div>


2. <div data-tips="true" data-tips-type="tip"><strong>Master hands\-on operations with agents</strong>: Learn how to use intelligent analysis agents to efficiently and reliably generate the required charts through precise prompt input (the previous section focuses on—quadrant charts, scatter plots, heat maps, stacked charts, and waterfall charts).</div>



<span id="c6899158"></span>
# 1. Fundamental understanding | How to choose the right chart for your data?

On the journey of data analysis, choosing the right chart is like finding the most suitable "interpreter" for complex data, enabling vast amounts of information to be transformed into a clear visual story. When faced with a dizzying array of chart types, we do not need to worry; simply return to the **core purpose** of the analysis to quickly make a choice.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>For beginners selecting charts, remember one core principle: prioritize requirements; clarity comes first</strong></div>


<div data-tips="true" data-tips-type="tip">Rather than pursuing "flashy" visual effects, first ask yourself: What issue do I want to illustrate with this chart? Is it to compare performance or clarify trends? Or is it to analyze proportions or identify correlations? Starting from this point, you will find that chart selection is actually quite simple.</div>


<span id="96979e72"></span>
#### 🔍 1. Compare sizes and differences: Use "bar chart / column chart"


* **Core function:**  Use the height of columns or the length of bars to intuitively display the numerical differences between different categories (such as different cities or departments) for the same metric.

* **Suitable scenarios**:

   * Compare sales revenue across product lines in the same quarter;

   * Show the number of new users acquired through different channels;

   * Review the annual budget completion rate for each team.

* **Practical tip:**  When category names are long (for example, "East China region \- offline self\-operated \- sports apparel category"), it is recommended to use a bar chart to ensure that label text is fully displayed and avoid overlap.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a29ec9036fd4ade8712d86a11705cd5~tplv-goo7wpa0wc-image.image) </span>

<span id="ed1df1d1"></span>
#### 📈 2. Observe changes and track trends: Use "line chart"


* **Core function**: By connecting each data point, accurately depict the fluctuations and trends of a metric over continuous time (or other continuous variables).

* **Typical scenarios**:

   * Track the annual trend of daily active users (DAU) for an app;

   * Observe the monthly changes in key business metrics (such as order volume or GMV);

   * Analyze the fluctuations in product performance metrics (such as CPU usage) after different versions are released.

* **Practical tip**: To keep the chart clear, a single line chart should not contain too many series. It is generally recommended **not to exceed 4 lines**; otherwise, overlapping lines can severely affect readability.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c9fd2b2892343d183ca05e5771c9521~tplv-goo7wpa0wc-image.image) </span>

<span id="8a0de13e"></span>
#### 🥧 3. Calculate proportions and examine composition: Use "pie chart / donut chart"


* **Core function**: Breaks down a whole into different parts and clearly displays the percentage each part contributes to the total.

* **Typical scenarios**:

   * Analyze the proportion of revenue from different business lines within a company's total revenue;

   * Count the distribution of age groups within a user base;

   * View the conversion contribution of each traffic channel in a marketing campaign.

* **Practical tip**: Pie charts are better suited for scenarios with **fewer than 6 categories**. If there are too many categories or items with very small percentages, the chart becomes crowded and hard to distinguish. In such cases, it is recommended to merge these small items into an "Other" category.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8b4f3f106f84530b1488f7ec599f991~tplv-goo7wpa0wc-image.image) </span>

<span id="989dfc6e"></span>
#### 🎯 4. Identify relationships and patterns: Use "scatter plot"


* **Core function**: Uses two numerical variables as the X and Y axes, and observes their potential correlation (such as positive, negative, or no correlation) through the distribution pattern of data points.

* **Typical scenarios**:

   * Analyze whether there is a linear relationship between advertising spend and resulting sales revenue;

   * Study the correlation between the time users spend within a product and their final conversion rate;

   * Explore the relationship between product pricing and sales volume.

* **Practical tip**: You can **add a trend line** to a scatter plot, which visually reveals the general direction of the relationship between the two variables. If the clusters of points generally follow the trend line from the lower left to the upper right, it usually indicates a "positive correlation".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db895ce5e10545b58adcbd3c9cec5674~tplv-goo7wpa0wc-image.image) </span>

<span id="c969d856"></span>
#### 📊 5. Analyze distribution and find intervals: Use "histogram"


* **Core function**: Divides continuous numerical values into several equal\-width intervals ("bins"), counts the frequency of data in each interval, and uses bar height to represent it, helping to understand the concentration, dispersion, and distribution pattern of the data.

* **Typical scenarios**:

   * Count the distribution of user ages to determine the main age group of the user base;

   * Analyze the distribution of e\-commerce order amounts to observe the proportion of high\- and low\-value orders;

   * Assess whether product quality inspection data is concentrated near the qualification standard.

* **Practical tip**: Never confuse histograms with bar charts. **The X\-axis of a histogram represents continuous numerical intervals** (such as 18\-24, 25\-30), with no gaps between the bars; whereas **the X\-axis of a bar chart represents independent, discrete categories** (such as "Beijing", "Shanghai"), with gaps between the bars.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cacdf8acb21343b48ada95b458d0f2ac~tplv-goo7wpa0wc-image.image) </span>

<span id="9f2caa01"></span>
# 2. Best practices | How to use the intelligent analysis Agent to output complex charts?

Mastering general chart selection principles is like having the "theoretical knowledge" of data visualization. The value of the intelligent analysis Agent lies in **automating, scaling, and stabilizing** this knowledge, seamlessly integrating the ability to select and interpret charts into your AI workflow. Especially in scenarios such as **report automation, operational review, risk monitoring, and product comparison**, the Agent can turn the tedious task of chart generation into **a simple intelligent conversation**.

<span id="01856af1"></span>
### 1. Practical product introduction

**Intelligent Analysis Agent** is a business\-savvy data insight partner that combines the deep reasoning of AI and big data capabilities. Based on "intelligent data querying", it helps you clarify problems, build an analysis outline, and execute a complete analysis. It excels at cross analysis and attribution analysis, turning complex data into understandable stories, and presents conclusions, causes, and action recommendations through clear and intuitive **charts and visualizations**, making every data analysis visible, understandable, and actionable.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/259dc2ad297f42f0a498c84778a7b402~tplv-goo7wpa0wc-image.image" width="594px" /></div>


<span id="66555239"></span>
### 2. Core pain points


* **Inconsistent chart selection and statistical standards:**  The same metric may lead to vastly different conclusions due to varying chart types and statistical standards.

* **Incorrect configuration of continuous/discrete axes:**  Treating discrete data as a continuous axis (or vice versa) can distort charts or even prevent them from being generated.

* **Unstable multidimensional charts:**  With multiple dimensions and series, improper legend, color, or value range settings can make charts chaotic and difficult to interpret.


<span id="d4fac56e"></span>
### 3. Advanced data chart output practice solutions

<span id="37111421"></span>
#### 3.1 Four\-quadrant chart

<span id="77c65344"></span>
##### (1) Scenario requirements:

Using the Boston matrix model, analyze the relationship between the gross margin and material loss of each store to identify the reasons affecting profitability. We use the average gross margin and average comprehensive loss rate as dividing lines to split the matrix chart into four quadrants, and plot scatter diagrams for each store within the matrix chart to help regional managers implement differentiated management strategies.

<span id="789fb7e1"></span>
##### (2) prompt template:

Report output chart requirements (use a four\-quadrant scatter plot, do not use other chart types, cannot be omitted):

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Use Python's Matplotlib library to plot a four\-quadrant scatter plot, and specify the following in the prompt</strong>:</div>



* <div data-tips="true" data-tips-type="tip">X\-axis: Comprehensive loss rate. Under {"Regional Manager"}, use AVG[Comprehensive Loss Rate] to calculate the reference point (coordinate origin).</div>


* <div data-tips="true" data-tips-type="tip">Y\-axis: Gross profit margin. Under {"Regional Manager"}, use AVG[Gross Profit Margin] to calculate the reference point (coordinate origin).</div>


* <div data-tips="true" data-tips-type="tip">Define quadrant labels for the four quadrants (labels placed inside the quadrants): high gross profit and low loss as star stores (upper left), high gross profit and high loss as abnormal stores (upper right), low gross profit and low loss as efficient stores (lower left), and low gross profit and high loss as problem stores (lower right).</div>


* <div data-tips="true" data-tips-type="tip">Set the axis ranges so that the reference lines are centered and the four quadrants are of equal size.</div>


* <div data-tips="true" data-tips-type="tip">Draw two reference lines: X = AVG[Comprehensive Loss Rate] and Y = AVG[Gross Profit Margin].</div>


* <div data-tips="true" data-tips-type="tip">Use different colored dots for each quadrant: green, orange, blue, and red.</div>


* <div data-tips="true" data-tips-type="tip">Hide data point labels (do not display the name at the top).</div>



<span id="eddaf02d"></span>
##### (3) **Agent** tuning experience summary:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Best practice 1: Clearly define the <strong>axes</strong> of the overall chart and specify the definitions of the X\-axis and Y\-axis.</div>


* <div data-tips="true" data-tips-type="tip">Best practice 2: Specify the requirements for <strong>distinguishing the four quadrants</strong> and the requirements for the reference lines.</div>


* <div data-tips="true" data-tips-type="tip">Best practice 3: Clearly state the overall chart display requirements (such as <strong>do not use other chart styles, do not omit</strong>, and similar prompts).</div>


* <div data-tips="true" data-tips-type="tip">Best practice 4: Using ECharts provides better\-looking and interactive charts compared to plotting with Python; however, in terms of stability, plotting with Python is more stable than with ECharts.</div>



<span id="b7b4755e"></span>
##### (4) Implementation results:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afa7eb7e76244989931ebe93509dd644~tplv-goo7wpa0wc-image.image" width="400px" /></div>


<span id="13a4ef1d"></span>
#### 3.2 Scatter plot and bubble chart

<span id="4a0b91f0"></span>
##### (1) Scenario requirements:

Use scatter plots to help customers handle complex analysis scenarios involving multiple dimensions and indicators. From the customer's perspective, clarify the distribution of contract duration, contract price, and sales volume among different customers. Represent different indicators simultaneously with the position, height, and size of a scatter point, enhancing the visualization of information elements.

<span id="7e0daa46"></span>
##### (2) prompt template:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Generate a scatter plot and specify the following details in the prompt:</strong></div>



* <div data-tips="true" data-tips-type="tip">X\-axis: <code>Contract signing time</code> (by date), as a continuous variable</div>


* <div data-tips="true" data-tips-type="tip">Y\-axis: <code>Contract signing price</code>, as a continuous variable</div>


* <div data-tips="true" data-tips-type="tip">Data series: Use different colors for the scatter points to distinguish <code>customer names</code>, and use the size of the scatter points to represent the <code>sales shipment volume</code> aggregated by <code>contract signing time</code>.</div>


* <div data-tips="true" data-tips-type="tip">Scale lines: Set the lower limit of the Y\-axis scale to 90% of the minimum <code>contract signing price</code>, and the upper limit to 110% of the maximum <code>contract signing price</code>. Keep two decimal places for the scale line labels.</div>



<span id="5fdf296f"></span>
##### (3) **Agent** tuning experience summary:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Best practice 1: For variables such as time and amount, always emphasize in the instructions "<strong>as a continuous variable</strong>" or "<strong>arranged in chronological order</strong>". This is key to generating an effective scatter plot. If the Agent misinterprets the date as discrete categories such as "first quarter" or "second quarter", all data points will be stacked at a few fixed positions, losing analytical value.</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Positive example</strong>: X\-axis (contract signing time): Set as a continuous timeline by "date (continuous variable)", ranging from "April → July → October → April 2025", with smoothly progressing scale marks;</div>


   * <div data-tips="true" data-tips-type="tip">Negative example: The X\-axis scale becomes three independent categories "Q1, Q2, Q3"; all April data are crowded at the "Q1" position, July at "Q2", October at "Q3"; if multiple contract prices fall within the same quarter, the points overlap into a "cluster", making it impossible to identify the price and time relationship for individual customers</div>


* <div data-tips="true" data-tips-type="tip">Best practice 2: Set the upper and lower limits of the Y\-axis range based on the extreme values of the metric to avoid scatter points being too densely packed</div>



<span id="a152ad87"></span>
##### (4) Implementation results:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0abb6cbd994b4b07b2ced6efb32ee85f~tplv-goo7wpa0wc-image.image" width="597px" /></div>


<span id="957c56dc"></span>
#### 3.3 Heat map

<span id="d51cf416"></span>
##### (1) Scenario requirements:

Use heat maps to help customers compare the contribution of multiple products to price fluctuations. From the product perspective, clarify the price difference for each product under different contract cycles. Use different color blocks and variations in shade to represent positive and negative impacts and highlight discrete extreme values.

<span id="b80908aa"></span>
##### (2) prompt template:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Generate a heatmap and specify the following details in the prompt:</strong></div>



* <div data-tips="true" data-tips-type="tip">Heatmap value: The heatmap value represents the <code>impact amount of price difference</code> for different <code>product models</code> during each contract period</div>


* <div data-tips="true" data-tips-type="tip">X\-axis: <code>Product model</code>, displayed in the order "G12", "G12R", "M10"</div>


* <div data-tips="true" data-tips-type="tip">Y\-axis: <code>Contract signing time</code>, arranged in ascending order from top to bottom by "year and month".</div>


* <div data-tips="true" data-tips-type="tip">Color scheme: Use a two\-color gradient to distinguish <code>impact amount of price difference</code>. When <code>impact amount of price difference</code> < \-0.001, use light yellow (#F6DA6D); between \-0.001 and 0.001, use light gray (#F2F2F2); when <code>impact amount of price difference</code> \> 0.001, use light blue (#88BDF5). The color intensity varies according to the value.</div>


* <div data-tips="true" data-tips-type="tip">Data labels: Display value labels centered in each cell.</div>


* <div data-tips="true" data-tips-type="tip">Cell: Maintain a white background plus cell color block style, and use the "loose" table layout format.</div>



<span id="0161de51"></span>
##### (3) **Agent** tuning experience summary:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Best practice 1: Specify the cell <strong>color block style</strong></div>


* <div data-tips="true" data-tips-type="tip">Best practice 2: Indicate whether the heat value <strong>uses a single color or two colors</strong>. Setting different color schemes for different value ranges can stabilize the display effect of the heat value.</div>



<span id="1a90bf7b"></span>
##### (4) Implementation results:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/344e5791e47e40f583ec0e99885fc1f2~tplv-goo7wpa0wc-image.image" width="691px" /></div>


<span id="92bd57e3"></span>
#### 3.4 Stacked chart

<span id="9fb49d73"></span>
##### (1) Scenario requirements:

Use stacked charts (also called accumulation charts), mainly to facilitate customers in observing the trend of a single indicator across multiple dimensions. From the product perspective, clarify the composition of sales volume under different contract cycles, making it easy to understand each product's impact on sales fluctuations.

<span id="c2c679b2"></span>
##### (2) prompt template:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Generate a stacked chart, and specify the following in the prompt:</strong></div>



* <div data-tips="true" data-tips-type="tip">X\-axis: <code>Contract signing time</code>, arranged in ascending order from left to right by month</div>


* <div data-tips="true" data-tips-type="tip">Y\-axis: <code>Sales shipment volume</code></div>


* <div data-tips="true" data-tips-type="tip">Split dimension: <code>Product model</code>, distinguished by different colors (you may specify the exact colors and product order).</div>



<span id="56ba2a8b"></span>
##### (3) Tuning experience summary:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Best practice 1: Specify <strong>the color differentiation for the split and nested dimensions</strong>, and if necessary, indicate the order of values for the split dimension</div>



<span id="5d085392"></span>
##### (4) Implementation results:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0306553ae13541bcb4c5f04c366780cb~tplv-goo7wpa0wc-image.image" width="738px" /></div>


<span id="3bce718a"></span>
#### 3.5 Waterfall chart (step chart)

<span id="c5d81cc9"></span>
##### (1) Scenario requirements:

Use waterfall charts (step charts) mainly to help customers break down the process of indicator changes in a time series. From the contract period perspective, analyze the impact of previous contracts on the current contract price, as well as the final price resulting from mutual influences, thereby identifying the main causes of price differences.

<span id="9373e387"></span>
##### (2) prompt template:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Generate a waterfall chart, and specify the following in the prompt:</strong></div>



* <div data-tips="true" data-tips-type="tip">Data preprocessing: With <code>sales shipment time</code> limited to the current month, aggregate <code>contract signing price</code>, <code>sales ex-factory price</code>, and <code>price difference impact amount</code> by <code>contract signing time</code> (by month), and simultaneously calculate the <code>sales ex-factory price</code> summarized by <code>contract signing time</code>.</div>


* <div data-tips="true" data-tips-type="tip">Starting bar: The <code>contract signing price</code> of the current contract, with the bar starting at zero;</div>


* <div data-tips="true" data-tips-type="tip">Adjustment items: For previous contracts, display the <code>price difference impact amount</code> by month according to <code>contract signing time</code>. When the <code>price difference impact amount</code> is positive, it represents a positive adjustment; when negative, a negative adjustment; when zero, no adjustment.</div>


* <div data-tips="true" data-tips-type="tip">Display requirements for adjustment items: The starting position of each adjustment bar must align with the ending position of the previous bar, and adjustment bars must connect end\-to\-end, forming a "staircase" pattern (pay special attention to this).</div>


* <div data-tips="true" data-tips-type="tip">Ending bar: The overall <code>sales ex-factory price</code> for the current month. The length of the ending bar must match the height of the starting bar plus all adjustment items.</div>


* <div data-tips="true" data-tips-type="tip">Style requirements: Fill the starting and ending bars with dark blue, positive adjustment bars with green, and negative adjustment bars with red.</div>


* <div data-tips="true" data-tips-type="tip">Labels: Add data labels outside the top end of each bar, displaying values with four decimal places.</div>


* <div data-tips="true" data-tips-type="tip">Other requirements: Strictly present in the form of a "waterfall chart"; do not omit anything and do not elaborate.</div>



<span id="5290d221"></span>
##### (3) **Agent** tuning experience summary:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Experience one: Label the X\-axis <strong>starting item, increase/decrease items, and final item</strong>.</div>


* <div data-tips="true" data-tips-type="tip">Experience two: Label the <strong>stacking relationship and the starting position of the bars for intermediate items</strong> to help AI better understand the "stacking" relationship.</div>



<span id="d841a3dc"></span>
##### (4) Implementation results:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a91c7dd8faf48bca006b00efa1d91d7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa848130ecc74420b4a72e1241ddb1bc~tplv-goo7wpa0wc-image.image) </span>
