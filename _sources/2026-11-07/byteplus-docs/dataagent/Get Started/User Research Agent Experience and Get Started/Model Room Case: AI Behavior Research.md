---
title: "Model Room Case: AI Behavior Research"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Model_Room_Case_AI_Behavior_Research"
---

The user research agent provides you with a demo project of trial experience. This article uses a specific example to demonstrate how to quickly experience the main operation process and functional capabilities of the user research agent.

<span id="9c5025bd"></span>
# Prerequisites and preparations

The current AI deep scrutiny function relies on the Volcano Engine DataFinder product. Before using the AI deep scrutiny function, you need to purchase and activate the DataFinder product and complete the following prerequisites on the DataFinder.

<span id="1ca6affb"></span>
# Trial application

If you want to try it out, you can contact the Volcano Engine technical support staff to apply for trial permission. After completion, you can switch to the "AI User In\-depth Research" project in the project drop\-down box at the top right, and you can try it out in this project later.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df74cee93e184a7ea9a909ed6273d4e9~tplv-goo7wpa0wc-image.image) </span>

<span id="3f3649ce"></span>
# Preset example

User Research Agent has pre\-set several examples of typical analysis scenarios for you. After you apply for a trial, you can click the following pre\-set example link to understand the analysis capabilities of user research. If you want to experience the operation process and analysis process, you can refer to the **demo experience** section below for practical experience.


|subdivision |Referral program optimization analysis |User behavior analysis, advertising effectiveness |user retention analysis |Experience optimization analysis of low deactivated user incentive scenarios |
|---|---|---|---|---|
|Preset sample link |[Example 1: List activity optimization analysis](https://console.volcengine.com/datafinder/project/3702264/detective/volc_duck_detective/1983/1731420751576244897) |[Example 2: User behavior analysis](https://console.volcengine.com/datafinder/project/3702264/detective/volc_duck_detective/2035/Demo-xiaoshuo-user_unique_id-54) |[Example 3: Retention analysis for new users](https://console.volcengine.com/datafinder/project/3702264/detective/volc_duck_detective/2033/Demo-bigdetective-user-3) |[Example 4: Experience optimization analysis of deactivated user incentive scenarios](https://console.volcengine.com/datafinder/project/3702264/detective/volc_duck_detective/2036/Demo-duanshiping-user_unique_id-1) |
|value expression |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a462643e0cf4970996caf8fb7fc1f90~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Typical scenario: analyze the reasons and clues that affect the effect of the activity in the referral program<br><br>* Value embodiment: identify sensitive groups of activities and summarize and analyze the entry strategy of activities |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75a150b9c5bd4adca96b18ef6c1adf05~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Typical scenario: based on advertising event tracking data, analyze and summarize the behavioral characteristics of a certain type of user<br><br>* Value: analysis and summary of user characteristics, analysis of user portrait distribution, evaluation of advertising effectiveness |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99ddefc912b44890ba4218242287106b~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Typical scenario: new function/new product pull effect analysis<br><br>* Value Embodiment: Insights and Attribution for Low Retention Scenarios |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99ddefc912b44890ba4218242287106b~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Typical scenario: new user experience analysis<br><br>* Value embodiment: experience problem insight and attribution, and help improve product experience |


<span id="154b5e44"></span>
# Demo experience

<span id="a1cd43fd"></span>
## Example scenario description

This example takes the incentive referral campaign operation activity of an application as an example, and deeply analyzes the reasons and clues of active sharing red envelope users in this activity, which is used to summarize the operation experience and optimize the entrance strategy of subsequent red envelope operation activities. The following are specific example operation steps.

<span id="825e2638"></span>
## Submit a detailed analysis task

After entering the trial project "AI User In\-depth Research", click the top navigation **User Research Agent** \> **AI In\-depth Detection** You can enter the AI In\-depth Detection page, configure the Insight User UID, Probe Event, Problem Description to be Insight under the current analysis example scenario on the page, and click the Task Run button after completion.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df74cee93e184a7ea9a909ed6273d4e9~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Demo configuration requirements |
|---|---|
|Insight into users |You can enter the user UID of the insight to be analyzed in the Insights user text box. This example allows you to enter the following list of user UIDs for the test experience.<br><br>```Plain```<br>```Demo-duanju-user_unique_id-1```<br>```Demo-duanju-user_unique_id-2```<br>```Demo-duanju-user_unique_id-3```<br>```Demo-duanju-user_unique_id-4```<br>```Demo-duanju-user_unique_id-5```<br>```Demo-duanju-user_unique_id-6```<br>```Demo-duanju-user_unique_id-7```<br>```Demo-duanju-user_unique_id-8```<br>```Demo-duanju-user_unique_id-9```<br>```Demo-duanju-user_unique_id-10```<br> |
|Probe time |The configuration is based on the behavioral data of the user to be analyzed in which time frame the user performs deep user insight analysis. This example selects the probing date as October 14, 2025. |
|Problem description |* In the problem description text box, enter the detailed description of the task that requires insight analysis. It is recommended to enter detailed analysis background, analysis insight goals, analysis requirements, and necessary prompt information (such as necessary business background knowledge, analysis ideas that can be tried) to ensure that the large model has a deep understanding of the business.<br><br>* The problem with this example is described below.<br><br>   ```Markdown```<br>```   In the red envelope fission activity, the current user group has shared and participated in multiple activities. Please determine the reasons and clues for their repeated sharing. The ultimate goal is to continue to improve the activity's ability to attract users and achieve the goal of increasing user retention and sustained user engagement.```<br>```   ```<br>```   Additional business knowledge:```<br>```   1. This activity refers to the withdrawal of reward amounts by inviting friends, and the promotional slogan states that friends invited by users can also earn money, which is a common method of attracting new customers; This activity usually requires N people to gather a sum of money and withdraw it directly, rather than sharing it once and receiving immediate profits.```<br>```   There are three ways to share activities, which are to click to invite and directly invite friends in the APP, scan the code face-to-face, and copy the invitation link to WeChat to invite friends.```<br>```   ```<br>    |


<span id="de067bce"></span>
## View analysis results

You can click on the corresponding user in the left user navigation bar to view the analysis results for the corresponding user.


|Subdivision |Example result |Analysis result description |
|---|---|---|
|Image analysis results |The running result of this example is as follows.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f38c4812cdb5463e85c36d76aea730e4~tplv-goo7wpa0wc-image.image) </span> |AI scrutiny will generate a user portrait summary description based on preset example user event tracking data and user attribute data. |
|Log enhancement results |The running result of this example is as follows.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f38c4812cdb5463e85c36d76aea730e4~tplv-goo7wpa0wc-image.image) </span> |You can view the core session links in the current user insights analysis process on the Log Enhancement page, including a list of core sessions and key behavioral links in each session.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The log enhancement function can further enhance the complex and difficult\-to\-understand user behavior logs into semantic and refined user behavior stream descriptions, which can greatly reduce the context length in the model analysis process and improve the model's understanding of user behavior data, thereby enhancing the efficiency and accuracy of insight analysis conclusions.</div><br> |
|Behavioral insights |The running result of this example is as follows.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f38c4812cdb5463e85c36d76aea730e4~tplv-goo7wpa0wc-image.image) </span> |You can view individual insights and their arguments, and drill down to see detailed conversation and behavioral flow details in the arguments. |
