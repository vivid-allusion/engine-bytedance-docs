---
title: "Best Practices: Deep Research Configuration and Tuning"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Best_Practices_Deep_Research_Configuration_and_Tuning"
---

The deep research capability of the Intelligent Analysis Agent builds upon intelligent data querying, integrates the deep reasoning abilities of large models, and can automatically parse natural language requirements, construct a comprehensive analysis framework, and generate deep research reports. To obtain analysis results that better align with business analysis objectives and are more accurate, refer to the following sections for configuring and tuning analysis requirements and report generation requirements.

<span id="b9f4a618"></span>
# Background knowledge

<span id="68d93fb6"></span>
## Key configuration points affecting results


* By leveraging the knowledge configuration capabilities provided by the Intelligent Analysis Agent, you can upload analysis requirements and historical analysis reports as knowledge for reference into the Intelligent Analysis Agent.

* When raising deep research questions, you can specify analysis requirements and report generation requirements in the question description.


<span id="d1d74616"></span>
# Analysis template configuration practices

<span id="35fda06c"></span>
## General approach

Before writing a query, it is recommended to identify the main analysis elements to improve the efficiency of query writing.

Note: The following information is intended to help you clarify requirements and ensure they are clear and complete. These items are preparatory notes and do not need to be copied and pasted into the query template.

<span id="fb1fa956"></span>
### Analysis objectives

First, clarify the core problem to be solved or the objective to be achieved. It is necessary to explain the analysis scenario, analysis role, and analysis purpose in one or two sentences. This is usually described in the first section of the query template.

<span id="6f37ff9a"></span>
### Analysis objects

This refers to the key elements such as metrics and dimensions that require further analysis to achieve the analysis objectives. To ensure the accuracy and effectiveness of analysis results, it is essential to clearly define the following core information when handling analysis tasks:


1. **Metric definition**: For DataAgent, metric definition refers to the combination of [dataset] + [metric field] + [filtering condition]

   1. When there are multiple datasets or multiple metric fields with similar names within a dataset, it is recommended to specify which dataset and metric field are being used.

   2. Filter criteria often contain the "private domain knowledge" of the business domain (that is, specialized understanding or rules specific to the domain). This information must be explicitly provided; otherwise, it may lead to analytical bias.

2. **Data extraction period**: The time range of the data is critical for interpreting analysis results. Different analysis methods may have different requirements for the period, which must be specified according to the specific needs, such as:

   * Trend analysis: It may be necessary to specify whether the period for trend analysis is the past 7 days, 30 days, or 3 months, and so on;

   * Attribution analysis: It is necessary to clarify the period for comparing the baseline and comparison periods, such as the past 7 days versus last week, or the past month versus last month, and so on.

3. **Changes in analysis objects**: As the analysis progresses, the analysis objects may shift from the overall to the local, or from the original analysis metrics to related metrics. It is important to pay attention to and specify changes in analysis objects in the query.


<span id="f707b220"></span>
### Analysis methods

When there are clear analysis expectations, the query should directly specify which analysis method is to be used. Common analysis methods include: descriptive statistics (calculation and comparison of metrics such as proportion, median, mean), attribution, anomaly detection, prediction, clustering, and more.

<span id="c8c9d31b"></span>
### **Output requirements**

The quality of the output should focus on both content and form. Proper arrangement of insights and the use of appropriate data visualization can make conclusions clearer and easier to understand. Therefore, requirements for both content and form must be specified and made explicit in the query.
