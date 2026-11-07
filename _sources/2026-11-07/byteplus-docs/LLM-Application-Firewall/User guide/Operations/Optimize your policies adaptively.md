---
title: "Optimize your policies adaptively"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Optimize_your_policies_adaptively"
---

Adaptive Policy Optimization analyzes historical traffic logs or uploaded offline samples to identify potential false positives and false negatives:


* A **false positive** is a normal request that was incorrectly blocked.

* A **false negative** is a risky request that was incorrectly allowed.


Based on the selected optimization objective and your additional preferences, the system generates policy recommendations that balance risk detection and normal business traffic. This helps reduce incorrect decisions and improve the overall effectiveness of LLM Application Firewall policies.

<span id="ac878377"></span>
## Prerequisites


* Before creating an optimization task, confirm that the following requirements are met:

   * An LLM Application Firewall instance has been created and is running normally.

   * The asset you want to optimize has generated both attack logs and normal traffic logs during the selected time range. More complete and representative samples help the system identify false\-positive and false\-negative patterns more accurately. This improves the quality of the generated policy and increases the likelihood that regression testing will pass.

   * Adaptive Policy Optimization is billed based on usage. For pricing details, see the relevant billing documentation.


<span id="630aec27"></span>
## Limitations


|Item |Limits |
|---|---|
|Maximum number of offline samples |50,000 samples |
|Maximum number of attack logs retrieved from online traffic |2,000 logs |
|Maximum number of normal logs retrieved from online traffic |8,000 logs |
|Supported offline sample formats |`xlsx` and `csv` |


<span id="799ba129"></span>
## Step 1: Create an optimization task


1. Log in to the LLM Application Firewall console.

2. In the left navigation bar, select **Operations \> Automated Operations**.

3. On the **Adaptive Policy Optimization** page, configure the following parameters:


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/782c202303d34c89b866322876327fde) </span>

<span id="f95c9aaf"></span>
### 1. Set the optimization objective

Use the slider to select an optimization objective. The default objective is **Standard**.


|Optimization objective |Description |
|---|---|
|Very high detection rate |Maximizes the detection of risky content but may increase false positives. |
|High detection rate |Prioritizes risk detection while allowing a moderate number of false positives. |
|Standard |Balances the detection rate and false positive rate. This is the default option. |
|High precision |Prioritizes reducing false positives but may miss some risky content. |
|Very high precision |Minimizes false positives but may increase false negatives. |


Moving the slider to the left prioritizes recall and risk coverage. Moving it to the right prioritizes precision and reduces the impact on normal traffic.

<span id="3d48a519"></span>
### 2. Select an asset

Search for and select the asset whose policy you want to optimize.

Each optimization task supports only one asset. Limiting the task to one asset keeps the sample source consistent and makes it easier to evaluate the effect of the optimized policy.

<span id="af9204bb"></span>
### 3. Select the optimization type

Switch between data sources using the tabs. Both **Online Logs** and **Offline Samples** are supported:


<Tabs>
<Tab zoneid="gkopLrkOwl" title="Online logs">
<TabTitle>Online logs</TabTitle>

Select **Log retrieval range** (time range selector). The system will retrieve detection logs within the selected time range as the optimization data source.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">Within the selected time range, up to 2,000 attack logs and 8,000 normal logs can be retrieved.</div>



</Tab>
<Tab zoneid="tJqBdtlwDj" title="Offline samples">
<TabTitle>Offline samples</TabTitle>

Click the **Upload sample** area and then the **Click to upload** button to upload a local sample file. To view the required file structure, download the template from the **Sample File** link.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">Offline samples must use the <code>xlsx</code> or <code>csv</code> format. We recommend including both risky samples that should be blocked and normal samples that should be allowed. Diverse and representative samples help the system identify decision errors more accurately.</div>


<div data-tips="true" data-tips-type="warning">You can upload up to 50,000 samples.</div>



</Tab>
</Tabs>


<span id="16f4c12f"></span>
### 4. Customize the optimization policy (optional)

Expand the **Custom Optimization Policy** section to set optimization levels and prompts for different detection categories:


|Column |Description |
|---|---|
|Type |Detection category type, including: Porn or vulgarity, Sensitive data, Prompt attack, Insult, Violence |
|Level |Single selection. The default is **Medium**. Optional values: Strict, Medium, Lenient |
|Prompt |Additional instructions that describe your review requirements or business preferences for the category. |


<span id="df56eb71"></span>
### 5. Add other preferences (optional)

Enter additional business requirements or optimization preferences in the multiline text box. Provide concise instructions that clarify the expected handling of specific content or scenarios.

<span id="8adcffa5"></span>
### 6. Start optimization

Review the configuration and click **Start Optimization** at the bottom of the page. The system creates an optimization task and begins analyzing the selected samples.

<span id="b7f092b7"></span>
## Step 2: Monitor the task


* The **Task Board** at the top of the page displays overall statistics for optimization tasks:

   * **Pending confirmation**: Number of tasks waiting for manual confirmation

   * **Optimizing**: Number of tasks currently being analyzed

   * **Completed**: Number of tasks for which optimization is complete

   * **Resolved false positives**: Total number of false positives corrected through optimization

   * **Resolved false negatives**: Total number of false negatives corrected through optimization

* When one or more tasks require confirmation, the page displays the message `There are currently N tasks pending confirmation`. Click **Confirm Now** to open the task center.

* You can also click **Details** on the task board. The task center opens in a drawer or dialog and provides the following tabs:

   * **Completed**: Displays completed optimization tasks.

   * **Optimizing**: Displays tasks that are currently running.

   * **Pending confirmation**: Displays tasks awaiting manual confirmation.


<span id="1b011acb"></span>
## Step 3: Confirm the results

After analyzing the samples, the system compares its new classifications with the original detection results. Samples for which the two results differ are displayed for manual review.

This process combines automated analysis with manual confirmation, preventing an optimized policy from being generated solely from model assessments.


* If the system classifies a sample as normal but the original policy classified it as risky, the sample is identified as a suspected **false positive**.

* If the system classifies a sample as risky but the original policy classified it as normal, the sample is identified as a suspected **false negative**.


In the task center, select **Pending Confirmation**, locate the task, and click **View Details**. To return to the task list, click **Back** at the top of the details page.

<span id="6bdf525c"></span>
### 1. Review suspected samples

The summary bar at the top of the page displays the following statistics:


* **Suspected issues**: Number of suspected false positives and false negatives identified by the system.

* **As expected**: Number of samples whose original detection result has been confirmed as correct.


You can review samples in **List View** or **Grid View**.

In List View, the table contains the following columns:


|Column |Description |
|---|---|
|Checkbox |Selects samples for a batch operation. |
|Sample type |Content type of the sample, such as text or image. |
|Content |Content of the sample. |
|Risk label |Risk category triggered by the sample. |
|Assessment result |Indicates whether the system identified the sample as a suspected false positive or false negative. |
|Cause analysis |Explains why the system produced the assessment. |
|Action |Provides actions for reviewing an individual sample. |


If you determine that the original detection result was correct, click **Mark as ** **Expected**. For example:


* A sample identified as a suspected false positive should remain blocked.

* A sample identified as a suspected false negative should remain allowed.


You can mark samples individually from the **Action** column or select multiple samples and click **Mark as ** **Expected**.

Samples marked as expected are removed from **Suspected Issues** and added to the **As Expected** count. They are not used when the system generates the optimized policy.

<span id="196666df"></span>
### 2. Generate the optimized policy

After reviewing the suspected issues, click **Next: Generate Optimization Policy**.

The system generates an optimized policy based on the confirmed results and automatically starts regression testing. The optimized policy adjusts the current policy according to the objective selected when the task was created.

Regression testing applies the optimized policy to the existing samples and checks whether its false positive rate and true positive rate fall within the ranges defined for the selected objective:


* If regression testing passes, the optimized policy meets the target metrics for the current samples and can proceed to manual testing and publication.

* If regression testing fails, review the samples and their classifications, adjust the inputs if necessary, and start another optimization task.


<span id="a28a22d5"></span>
## Step 4: Publish the policy

After the system generates the optimized policy, review its false positive rate, true positive rate, and other key metrics. Evaluate these metrics together with your business requirements before publishing the policy.


1. Click **Manually Test Policy**.

2. Submit representative normal requests, historical risk samples, and frequently occurring business content.

3. Compare the results produced before and after optimization.

4. If the results meet your requirements, click **Publish Policy** at the bottom of the page.


Where possible, publish the policy during a period when system behavior can be closely monitored and business traffic is stable. After publication, monitor security alerts, false\-positive reports, and business feedback to evaluate the policy’s production performance.

<span id="0a94671b"></span>
## Frequently asked questions

<span id="5e00a240"></span>
### What causes log extraction or automatic labeling failures?


* **Cause**: Log extraction or automatic labeling may fail because there are no logs within the selected time range, or because the log samples lack sufficient representativeness, preventing the system from performing stable analysis.

* **Solution**: We recommend first checking whether the time period contains a sufficient number of both normal and risk requests. If the samples are insufficient, you can expand the time range before starting again. Having more samples not only helps complete automatic labeling, but also improves the credibility of subsequent policy optimization results.


<span id="182f96e4"></span>
### How are false positive and false negative results determined?

After creating an adaptive policy optimization task, the system relabels the extracted logs and compares the new labels with the original detection results to identify potential false\-positive and false\-negative samples.


* **Labeling result is a normal request, but the original detection result is a risk request**: Determined as a **false positive**.

* **Labeling result is a risk request, but the original detection result is a normal request**: Determined as a **false negative**.


On the results page, you can view results by category: "All / False Positive / False Negative", and make judgments based on the original content, risk tags, cause analysis, and business context. The value of this mechanism lies in first narrowing the scope of investigation through automatic comparison, and then improving the reliability of the final conclusion through manual confirmation.

<span id="332d5077"></span>
### What are the false positive rate and detection rate? How are they calculated?


* **False positive rate (False Positive Rate, FPR):**  is the proportion of normal requests that are incorrectly identified as risk requests. **False positive rate = normal requests incorrectly identified as risk content / all normal requests \* 100%** , where all normal requests include normal requests incorrectly identified as risk content and normal requests correctly identified as normal content. This metric reflects the degree to which the policy interferes with normal business operations. The lower the value, the more beneficial it is for ensuring business continuity and user experience.

* **True positive rate (TPR):**  refers to the proportion of risk requests accurately identified as risk requests. **True positive rate = risk requests accurately identified as risk content / all risk requests \* 100%** , where all risk requests include risk requests accurately identified as risk content and risk requests incorrectly identified as normal content. This metric reflects the policy's coverage of actual risks. The higher the value, the more beneficial it is for improving security protection effectiveness and risk detection efficiency.


<span id="834b9227"></span>
### What are the false positive rate and true positive rate ranges for different optimization targets?

Each optimization target level has corresponding false positive rate and true positive rate ranges. Regression testing automatically determines whether the policy meets the optimization target based on its false positive rate and true positive rate.


|Optimization objectives |FPR |TPR |Protection effectiveness |Recommended scenarios |
|---|---|---|---|---|
|Very high detection rate (most stringent) |≤ 25%<br><br> |≥ 95% |Maximize the identification capability for attack and risk content, allowing a certain proportion of normal requests to be falsely blocked. |High\-risk scenarios such as major protection activities, attack\-defense exercises, full\-scale protection of core systems, and rapid screening of malicious samples. We recommend having sufficient staff on duty and alert handling capabilities. |
|High detection rate |≤ 20% |≥ 90% |While maintaining a high attack identification capability, keep false blocking within a relatively acceptable range. |Routine security monitoring for critical perimeter protection, high\-risk business interfaces, important servers, or key business scenarios. |
|Standard (default) |≤ 15% |≥ 85% |Achieves a relatively balanced trade\-off between false positive rate and detection rate, making it suitable as the default choice for most business scenarios. |Routine detection for general business, ongoing protection for non\-core systems, and initial tuning scenarios when preferences are not yet specified. |
|High accuracy rate |≤ 10% |≥ 80% |Prioritizes minimizing the impact of false blocking on business operations while maintaining basic risk identification capabilities. |Enterprise office networks, internal business systems, and business scenarios that require high stability for normal requests. |
|Very high accuracy rate (most lenient) |≤ 5% |≥ 75% |Minimizes false blocking to the greatest extent, with greater emphasis on business continuity and a lightweight protection experience. |Public products for end users, businesses with limited operational workforce, or lightweight protection scenarios with extremely low tolerance for false blocking. |


<span id="471aeca5"></span>
### What does it mean if regression testing fails?

Regression testing uses the optimized policy to automatically validate existing samples to confirm whether the false positive rate and true positive rate fall within the ranges corresponding to the selected optimization target. If regression testing fails, it means the policy has not achieved the expected results.

For example, when the optimization target is **standard**, the false positive rate should be less than or equal to 15%, and the true positive rate should be greater than or equal to 85%. If the regression test results show a false positive rate higher than 15% or a true positive rate lower than 85%, it means the current policy does not meet the requirements of the target, and therefore the test fails.

The reasons for regression testing failure may include:


1. The access control rules you set may cause a large number of requests to be automatically allowed or blocked. However, during the policy optimization process, the large language model (LLM) independently evaluates each request based on its actual content. This may result in a request allowed by the rules being identified as a risk by the large language model (LLM), or a blocked request being identified as normal. When such evaluation conflicts occur too frequently, there will be a large number of inconsistencies in the detection results before and after policy optimization.

2. Due to insufficient log samples, regression tests cannot accurately assess the policy's false positive rate and detection rate.
