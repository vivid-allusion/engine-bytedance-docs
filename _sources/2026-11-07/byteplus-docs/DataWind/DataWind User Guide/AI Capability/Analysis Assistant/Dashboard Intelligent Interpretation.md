---
title: "Dashboard Intelligent Interpretation"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dashboard_Intelligent_Interpretation"
---

The intelligent data insight analysis assistant helps users intelligently build dashboards, intelligently modify dashboards, and assists users in interpreting dashboards. This article introduces how to use the analysis assistant's intelligent dashboard feature for dashboard interpretation.

<span id="8063e7fe"></span>
# Feature overview

Dashboard intelligent interpretation leverages large language model (LLM) capabilities to automatically perform in\-depth analysis of global dashboard data, enabling users to accurately grasp data value and efficiently support decision\-making.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f4c91cc704b4e7f99f69b62b55e0279~tplv-goo7wpa0wc-image.image) </span>


* Quickly summarize data in charts and extract key information

* Enable instant attribution linkage and data source verification

* Support custom interpretation templates, providing both template\-based and free\-form interpretation configuration methods


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is a sub\-feature under the value\-added module "Analysis Assistant" and is disabled by default. To use this feature, contact Volcano Engine technical support for consultation. After purchasing and activating this feature, it will be available for use.</div>


<span id="7f9dcf10"></span>
# Quick start


1. Before using intelligent dashboard generation, the corresponding dataset must have the analysis assistant capability enabled. On the "Dataset" details page, click the "Enable DataWind Analysis Assistant" button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cc0d788497449cc83e72bbe8eb75566~tplv-goo7wpa0wc-image.image) </span>

2. Enable interpretation. After opening the dashboard, users can find the "Dashboard Interpretation" entry at the top right corner of the chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15af68a77bfd49cc874f90222a8f7d62~tplv-goo7wpa0wc-image.image) </span>

3. Interpretation configuration. Both template\-based and free\-form interpretation methods are supported. Click "Go to Configure" or the "Interpretation Configuration" icon in the upper right corner to open the interpretation configuration window below, where users can select any interpretation configuration method.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Users need to have edit permissions for the dashboard. For details on how to apply for permissions, refer to <a href="https://docs.byteplus.com/docs/DataWind/Detailed_Explanation_of_Permission_Features">Detailed Explanation of Permission Features</a>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8296bada807440b8fc1a53964760718~tplv-goo7wpa0wc-image.image) </span>

   
   |**Template interpretation** |**Free interpretation** |
   |---|---|
   |Users input template text, then select the intelligent paragraph sections in the template, and configure the prompt for each intelligent paragraph. The large model generates Python code for processing each paragraph based on the prompt, and executes the Python code to produce the interpretation results. |The large model generates interpretation results by obtaining dashboard chart data based on the interpretation idea prompt entered by the user. |
   |Compared to free interpretation, template interpretation has the following characteristics:<br><br><br>* **More focused debugging**: Debugging is performed for a single paragraph, making it more focused<br><br>* **More stable results**: The LLM is only called during debugging, and the generated Python code is fixed. Subsequently, only the code is executed each time, resulting in more stable outcomes<br><br>* **Faster computation**: Similarly, since only the code is executed each time and the LLM is not called, the response speed is faster ||
   

4. Refresh interpretation. To regenerate the interpretation result if dissatisfied, click "Refresh" to generate a new interpretation result.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/136f26da99a04e5c876acf4b08bac795~tplv-goo7wpa0wc-image.image) </span>


<span id="80d0831e"></span>
# Configure interpretation

Dashboard intelligent interpretation allows users to set interpretation templates according to business scenarios, providing both template\-based and free\-form interpretation configuration methods, which users can freely choose as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83130ce3abf945fdbcc834569161f411~tplv-goo7wpa0wc-image.image) </span>

<span id="e2c00d3f"></span>
## Template\-based interpretation

The template interpretation feature performs a 'cloze test'\-like effect on the template text entered by the user, helping the user configure and debug prompts for the parts of the interpretation template that need to be flexibly modified.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Writing suggestions for interpretation ideas and configuration examples for template interpretation are provided in <strong>Related references</strong>.</div>



1. Switch to the "Template Interpretation" page and enter the template content on the left side.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3a1c3fa56a94f70a3d4849e0bdfe9c2~tplv-goo7wpa0wc-image.image) </span>

2. Select the parts that require AI\-assisted generation and convert them into intelligent paragraphs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40ae720ba1134ab9ad5e37bc96c5ab65~tplv-goo7wpa0wc-image.image) </span>

3. Configure the prompt for each intelligent paragraph. Please use natural language to describe the data retrieval logic and style of the intelligent paragraph. You can use "@" to insert objects such as datasets or charts, and you can also specify rules such as "red for increase, green for decrease" or "add a special symbol at the end if greater than 10%", and more.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0f401b1828e42298bc411715c2b5ff0~tplv-goo7wpa0wc-image.image) </span>

   The "Prompt Optimization" feature is provided. Click the "Prompt Optimization" icon to view the optimization results. To use the optimized result, click "Confirm"; otherwise, click "Cancel" to exit the local prompt optimization page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71c355b3b8b4472eb8d4fce43be75884~tplv-goo7wpa0wc-image.image) </span>

4. **Local preview** of each intelligent paragraph result. Click "Preview" to view the interpretation result of this paragraph.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The preview effect of intelligent paragraphs is based on the interpretation results obtained from the initial dashboard data and is not affected by changes to filter options.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/598a18ef5c13472a8f05f5c71455a549~tplv-goo7wpa0wc-image.image) </span>

   The local preview effect is as follows. You can switch to view the result preview, generation logic, and thought process.

   
   |Result preview |Generation logic |Thinking process |
   |---|---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4003c1b79de463d924e63f475c5617f~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06f01eb5fbc049cbbde0a903080dd7c7~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d4ecf40c8654570b6f5896e094903f1~tplv-goo7wpa0wc-image.image) </span> |
   

   If you are not satisfied with the preview result of the intelligent paragraph interpretation, you can click "Edit" or "Adjust based on the generated Python code".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75016d8b8da7465a81e4e8c07d9108e1~tplv-goo7wpa0wc-image.image) </span>

   * Edit: Return to the intelligent paragraph prompt input step to adjust the prompt content.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/352f44eb2d8c4081a96d8b10adfed582~tplv-goo7wpa0wc-image.image) </span>

   * Adjust based on the generated Python code: Open the generated Python code content and directly adjust the code as needed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bcb633d0e0444cfbba8711fbad8b310~tplv-goo7wpa0wc-image.image) </span>

5. **Global preview** of the interpretation result. After configuring the prompts for all intelligent paragraphs, click "Preview" to view the overall interpretation effect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/834c1e7bae42424197d17c11120f8a5b~tplv-goo7wpa0wc-image.image) </span>

   The overall interpretation preview result is as follows. Click "Save" to activate the template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9f649b3f233455eb21516131f13d142~tplv-goo7wpa0wc-image.image) </span>

6. Click "Dashboard Interpretation" again or refresh the interpretation content to use the configured template for interpretation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f32101a19964393ac0590452ddcfa08~tplv-goo7wpa0wc-image.image) </span>

7. In addition, the "Template Interpretation" area also provides the following features:

   * Insert intelligent paragraph: After insertion, you can configure the generation logic on the right side. The AI will obtain data and generate paragraph content according to the instructions.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db3291ad39414feda9ac05dec078947c~tplv-goo7wpa0wc-image.image) </span>

   * Auto display toggle: When enabled, interpretation content is automatically displayed to viewers when they access the dashboard; when disabled, viewers must manually turn on the interpretation toggle to view the content.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f8a4fec566149cf974ab9d94edec863~tplv-goo7wpa0wc-image.image) </span>

   * Data limit settings: You can enable the data limit toggle for individual or multiple charts. If not enabled, the maximum number of chart data entries retrieved is 1,000; when enabled, the limit is 10,000 entries.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc60abc0e3894a9ea5a23dcc6a9fab3f~tplv-goo7wpa0wc-image.image) </span>

   * Supports redo, undo, setting smart paragraph text format, deleting individual smart paragraphs, clearing all smart paragraphs, and more.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3de6c345f9ce483d82159e8bb626e38f~tplv-goo7wpa0wc-image.image) </span>


<span id="39446551"></span>
## Free interpretation

The large model generates interpretation results by retrieving dashboard chart data based on the interpretation prompt entered by the user.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Writing suggestions for interpretation ideas and configuration examples for free interpretation are provided in <strong>Related references</strong>.</div>



1. Switch to the "Free Interpretation" page and enter the free interpretation template content below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/891936697c9644e0a9f32629cb9a5cdc~tplv-goo7wpa0wc-image.image) </span>

2. Click "Preview" to view the interpretation effect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4841744aa0646fda8b09758f9e55338~tplv-goo7wpa0wc-image.image) </span>

3. If you are not satisfied with the new interpretation effect, you can click "Return to Edit".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6050702bcc1646329dcdb4264c307bd4~tplv-goo7wpa0wc-image.image) </span>

4. You can adjust the free template content, or click "Restore Default" to revert to the default interpretation approach.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c4dd57250fb443cbf1b0aaa25eb73e3~tplv-goo7wpa0wc-image.image) </span>

5. After completing the settings, click "Save". Then, by enabling the "Dashboard Interpretation" feature again or refreshing the interpretation content, you can use the customized interpretation analysis approach.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47de82b899d645cba48e5f2d2b0b5d32~tplv-goo7wpa0wc-image.image) </span>

6. Dashboard free interpretation also provides a "Knowledge Base" feature, allowing you to configure free interpretation template content in conjunction with knowledge base content.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/815c0b72508a482aa254d6c4d0bc9799~tplv-goo7wpa0wc-image.image) </span>

7. In addition, free interpretation also supports undo, redo, and adjusting the data limit.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/150685b4ee424ae9a8d4344fd030d0d6~tplv-goo7wpa0wc-image.image) </span>


<span id="931c9239"></span>
# View interpretation

The intelligent dashboard supports interpretation of all chart data. Click to enable "AI Interpretation"; an "Interpreting" prompt will appear at the top of the dashboard. After interpretation is complete, users can view the interpretation content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e11aa646f6044d33ba565b0999a5932a~tplv-goo7wpa0wc-image.image) </span>


* Key chart points such as outliers, trends, rankings, and more can be automatically extracted and summarized.

* In addition to automatically extracting key chart information, two advanced features are also provided: **Instant Attribution Linkage** and **Data Source Verification**.


<span id="2b102bfe"></span>
## Instant attribution linkage

The instant attribution linkage feature is an important support for the intelligent dashboard interpretation function to achieve deep data insights. This feature is based on preset attribution analysis logic and will automatically select the metrics in charts for which changes need to be analyzed, intelligently break down metrics and dimensions, and quickly identify the contributing factors behind changes.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8512b3038bf44c8bc76d939919d1c9a~tplv-goo7wpa0wc-image.image" width="2008px" /></div>



* The system can perform attribution analysis from both the dimension and metric levels, accurately pinpointing the key factors driving data changes, and will highlight the top three positive contributing factors (which drive positive data changes) and negative contributing factors (which lead to negative data changes).

* In\-depth impact analysis can be conducted for each dimension and metric. Interactive visualizations display key data, such as contribution values and contribution rates for dimensions like merchant segmentation and industry classification. Users can click on related chart elements to drill down from macro data to micro details, quickly identifying the root cause of data changes and providing a reliable basis for business decision\-making.


<span id="5d936d1a"></span>
## Data source validation

The intelligent dashboard interpretation supports establishing data mapping validation, deeply linking the core conclusions generated by the interpretation with the data dashboard.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05d321e660c0402aab45a2e74978990a~tplv-goo7wpa0wc-image.image) </span>


* When users click on key data in the conclusion, the corresponding original data trend chart automatically pops up, allowing users to drill through from textual conclusions to visualized data. This enables users to quickly trace data details from the conclusion, assists in validating the logic of the conclusion, and facilitates the exploration of deeper data change correlations, thereby improving analysis and decision\-making efficiency.


<span id="abc8f5a9"></span>
# Other features

<span id="96c88489"></span>
## Copy interpretation content

You can copy all interpretation content.

<span id="59d2bf12"></span>
## Refresh interpretation content

If the interpretation result is unsatisfactory, you can regenerate the interpretation by adjusting the template and clicking the refresh button.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb2c3e4060a2432daff273616d47f718~tplv-goo7wpa0wc-image.image) </span>

<span id="2f5b5c9e"></span>
## Subscribe to interpretation results

After enabling the intelligent dashboard feature, click "Create subscription" to see the "Large model intelligent interpretation" switch in the subscription summary/interpretation settings. Once enabled, the content pushed by the subscription will include dashboard intelligent interpretation content. Please refer to [Data Subscription](https://docs.byteplus.com/docs/DataWind/Data_Subscription) for detailed subscription setup steps.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This feature currently only supports subscriptions with the push method set to "Lark"; other push methods are not supported at this time.</div>


* <div data-tips="true" data-tips-type="warning">Currently, the subscription must select either "Dashboard screenshot [tiled large image]" or "Dashboard PDF download link" for the interpretation content to take effect.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81c1749a588b4e1680befb5e9b438325~tplv-goo7wpa0wc-image.image) </span>

After enabling "Large Model Intelligent Interpretation", the effects of subscription push include:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1db4f9344744764b9e99da194a3ec9d~tplv-goo7wpa0wc-image.image) </span>

<span id="48b756f2"></span>
## Quickly locate charts


* When searching for charts, you can locate the chart's position on the canvas.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fc9d433b6ba483288308c10577a8489~tplv-goo7wpa0wc-image.image) </span>

* You can also quickly locate a chart by clicking an inserted chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a9660f9e78f4977b3ff12c6b9fbdbd7~tplv-goo7wpa0wc-image.image) </span>


<span id="c4c31435"></span>
## Knowledge base integration

The "Free Interpretation" module of dashboard intelligent interpretation provides integration with the knowledge base. By leveraging existing industry patterns, historical data conclusions, business metric definitions, and other content in the knowledge base, the "Free Interpretation" module can automatically associate information and generate evidence\-based interpretation reports, eliminating the need for repeatedly consulting materials and manually organizing analysis logic. For knowledge base\-related information, see [知识库概述](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62a4b).

**Specific applications**:


* Generate analysis dimensions based on the knowledge base

* Embed knowledge base explanations in interpretation reports


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9df3f174bca94be686276b6026b8fb46~tplv-goo7wpa0wc-image.image) </span>

<span id="60947e37"></span>
# Relevant references

<span id="2a485da6"></span>
## Interpretation writing recommendations

The key to achieving ideal output when using data interpretation is writing high\-quality prompts. A clear, specific, and well\-organized prompt can significantly improve the response quality and efficiency of data interpretation. The following sections provide basic approaches, writing suggestions, and reference examples to help users better use data interpretation.


|**Steps** |**Example** |
|---|---|
|1. Clarify the analysis objective<br><br>   Clearly state the required interpretation direction to avoid ambiguous expressions |* Analyze the sales revenue trends of each product line and identify categories with significant increases or decreases<br><br>* Compare user retention rate data across different regions, identify the region with the largest difference, and hypothesize possible reasons<br><br>* Based on order data from the past six months, forecast the possible fluctuation range of sales volume for the next quarter and the key influencing factors |
|2. Consider the business scenario<br><br>   Provide the necessary business knowledge background and metric definitions to help the large model understand |* Redemption rate = Redemption GMV / Paid GMV. The redemption rate is a key metric we focus on. When the redemption rate exceeds 80%, it is considered satisfactory; otherwise, it is not considered satisfactory. |
|3. Guide step by step, breaking down the problem<br><br>   The problem can be broken down so that the large model interprets it according to your expected steps |* Please analyze the redemption rate situation according to the following steps<br><br>   * Step 1: Analyze the redemption rate trend, focusing on cases where the redemption rate is not considered satisfactory (<80%) or shows an abnormal decline (a drop of more than 3 percentage points)<br><br>   * Step 2: When the redemption rate is not considered satisfactory or shows an abnormal decline, drill down by industry, merchant segmentation, region, and other dimensions to analyze the main influencing factors |
|4. Output format requirements<br><br>   You can specify the required output format for ease of use |* Interpret the issue of rising user churn rate in the format of 'Conclusion + Cause + Recommendation' |


<span id="a5ad6dd3"></span>
## Configuration interpretation examples

<span id="bd64d534"></span>
### Template interpretation examples


|Dashboard screenshot |Interpretation approach configuration example |Interpretation effect |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13061c8d7e094bb299f9cfb8eb5a80fd~tplv-goo7wpa0wc-image.image) </span> |* Initial template content<br><br>   ```Plain```<br>```   Month-on-month performance: write off GMV xx, month-on-month xx%```<br>```   ```<br>```   According to industry```<br>```   Top 3 industries with month-on-month increase in verified GMV: xxxx（xxx->xxx，xx%），xxxx（xxx->xxx，xx%），xxxx（xxx->xxx，xx%）```<br>```   Top 3 industries with a month-on-month decrease in verified GMV:xxxx（xxx->xxx，xx%），xxxx（xxx->xxx，xx%），xxxx（xxx->xxx，xx%）```<br>```   ```<br>```   According to region```<br>```   Top 3 regions with month-on-month increase in verified GMV: xxxx（xxx->xxx，xx%），xxxx（xxx->xxx，xx%），xxxx（xxx->xxx，xx%）```<br>```   Top 3 regions with month-on-month decrease in verified GMV: xxxx（xxx->xxx，xx%），xxxx（xxx->xxx，xx%），xxxx（xxx->xxx，xx%）```<br>```   ```<br>```   Anomaly city (Cities with prominent month-on-month increase/decrease in GMV)```<br>```   xxxx（xxx->xxx，xx%）```<br>```   xxxx（xxx->xxx，xx%）```<br>```   xxxx（xxx->xxx，xx%）```<br>```   ```<br>   <br><br>* Intelligent paragraph prompt<br><br>   ```Plain```<br>```   @Verified GMV industry distribution dataset, sort by month-on-month growth rate from high to low, and filter out the top three secondary industries.```<br>```   Display format: secondary industry name（yesterday's value -> today's value，+xx%）。```<br>```   Numerical processing rules:```<br>```   1. Yesterday's value and today's value: When the value is too large, it should be converted into units of "ten thousand" (10^4), "one million" (10^6), and "ten million" (10^7). The converted integer should be greater than 0, and the result should be rounded to two decimal places.```<br>```   2. Month-on-month growth rate: rounded to one decimal place.```<br>```   Format: red for increase while green for decrease```<br>```   ```<br>    |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d799b82b39d64becb774fba43f49f7a2~tplv-goo7wpa0wc-image.image) </span> |
||||
||||


<span id="f0835445"></span>
### Free interpretation examples


|Dashboard screenshot |Interpretation approach configuration example |Interpretation effect |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13061c8d7e094bb299f9cfb8eb5a80fd~tplv-goo7wpa0wc-image.image) </span> |```Markdown```<br>```The final output consists of two parts of data:```<br>```## Overview```<br>```Summarize the content of the dashboard without presenting specific data```<br>```## Key Findings```<br>```Analyze the data in the dashboard and summarize some key findings```<br>``````<br>``````<br>```## Interpret Method Reference```<br>```1. Verified GMV is the core metric we focus on.```<br>```2. Attention should be paid to abnormal increases or decreases in GMV (fluctuations exceeding 3 pp), or continuous increases or decreases for 3 days or more.```<br>```3. When there is abnormal fluctuation in the verified GMV, it is possible to drill down through dimensions such as industry, merchant segmentation, and region to analyze the reasons for the fluctuation. Analysis can also be conducted from the perspective of relevant metrics```<br>```4. The calculation logic between relevant metrics is as follows:```<br>```- verified GMV = pay GMV - refund GMV```<br>```- verified rate = verified GMV/pay GMV（verified rate>80% is considered as meeting the standard，<80% is considered below the standard）```<br>``````<br>```## The data format of metrics```<br>```1. GMV, display numerical values with 2 decimal places. When the value is large, unit conversion can be performed for "ten thousand", "one million", and "ten million".```<br>```2. Verified rate, the percentage is displayed in the percentage form, and the decimal places are retained to 1 decimal place.```<br> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7644e82447544989eee189d5335bf47~tplv-goo7wpa0wc-image.image) </span><br><br>```Plain```<br>```Key Findings```<br>``````<br>```Abnormal fluctuations in verified GMV:```<br>```In data from last 10 days, there are various abnormal fluctuations of verified GMV. For example:```<br>```-8.30%（2025-08-18）。```<br>```3.45%（2025-08-19）。```<br>```-9.64%（2025-08-20）。```<br>```These fluctuations indicate significant instability in the verified GMV and require further analysis of the reasons.```<br>``````<br>```Verified rate compliance status:```<br>```The verified rate has not met the standard for 5 out of the past 10 days(below 80%). For example:```<br>```78.87%（2025-08-18）。```<br>```79.83%（2025-08-21）。```<br>```The low compliance rate indicates that business efficiency needs to be improved.```<br>``````<br>```Continuous increase trend:```<br>```On August 23, 2025, there was a continuous three-day increase trend in verified GMV, which may be related to promotional activities or other factors.```<br>``````<br>```The impact of refund GMV:```<br>```The change in refund GMV has a direct impact on verified GMV and verified rate. For example, the refund GMV on 2025-08-26 was 149,100, resulting in a decrease in verified rate to 79.54%.```<br>``````<br>```The relation of pay GMV and verified GMV:```<br>```The growth of pay GMV does not always lead to synchronous growth of verified GMV. For example, on 2025-08-22, the pay GMV was 76,3400, but the verified GMV only increased by 1.80% month-on-month.```<br>``````<br>```Next step suggestion```<br>```Drill-down analysis:```<br>```For the abnormal fluctuations in verified GMV, we can drill down from dimensions such as industry, merchant segmentation, and region to identify specific reasons.```<br>```Analyze dates with high refund GMV and identify merchants or industries with high refund rates.```<br>``````<br>```Optimize verified rate:```<br>```Check for systemic issues or merchant performance problems with dates where verified rate does not meet the standard.```<br>``````<br>```Monitor continuous trend:```<br>```Pay attention to the continuous increase or decrease trend of verified GMV and adjust operational strategies in a timely manner.```<br> |
||||
||||


<span id="8f68858c"></span>
# Special statement

(1) All content output by this service is generated by artificial intelligence models.

(2) This feature is intended for use only by customers for internal, proprietary business, and personal use. Customers may not provide generative artificial intelligence services to the public via the Analysis Assistant.

(3) This feature is a value\-added module, supporting both SaaS and on\-premises deployment versions. For purchase or trial, please contact our sales representative for consultation.

(4) Currently, the AI capabilities of DataWind for intelligent data insights support the following dataset types:


* Supports extracted datasets and datasets uploaded as Excel or CSV files.

* Supports directly connected datasets, currently including: ClickHouse / ByteHouse, Doris / selectdb.
