---
title: "AI Behavior Research"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/AI_Behavior_Research"
---

The AI behavior research function of the user research agent can provide insight into the characteristics of designated users behind scenarios such as content consumption and function penetration through large models, and gain a deep understanding of behavioral flows. By summarizing the characteristics of the sample population, the behavioral characteristics of specific groups can be mined. This article introduces the functional capabilities and operational guidance of AI behavioral research.

<span id="9cc83584"></span>
# Background information

AI behavior research is based on user behavior data and user attribute data collected by DataFinder, which can summarize user portraits through model capability analysis, identify and analyze key user behavior streams in problem scenarios for insight analysis, and finally summarize and analyze the cause insights of designated users in certain problem scenarios.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df9d56f19dd343c094bfccaba24c0bcc~tplv-goo7wpa0wc-image.image" width="600px" /></div>


Of which:


* The behavioral scrutiny function can further enhance and summarize the complex and difficult\-to\-understand user behavior logs into semantic and refined user behavior stream descriptions, which can greatly reduce the context length in the model analysis process and improve the model's understanding of user behavior data, thereby enhancing the efficiency and accuracy of insight analysis conclusions.

* AI behavior research further examines the details of the analysis basis after drawing insight analysis conclusions; at the same time, it supports direct questioning.


<span id="6b7d0a9b"></span>
# Precautions


* The current AI behavior research function relies on the Volcano Engine DataFinder product, and the function is currently in the beta version and is in the invitation testing stage. If you want to use this function, you need to purchase and activate the DataFinder product first, and contact the technical support staff to apply for the invitation testing permission.

* If you have applied for opening an invitation to test, and it still prompts that "AI Behavior Research" cannot be used when using it, please contact your project administrator to open the function permission.


<span id="61c532e5"></span>
# Prerequisites and preparations

The current AI behavior research function relies on the Volcano Engine DataFinder product. Before using the AI behavior research function, you need to purchase the DataFinder product and complete the following prerequisites on the DataFinder.

<span id="d947aa5b"></span>
## User behavior data access

Due to the fact that AI behavior research is mainly used for deep analysis and insight into specific users, you need to connect user behavior data to the Volcano Engine DataFinder before using it.


|operation suggestion |Operation guidance |
|---|---|
|* You need to report the user behavior data collection that needs to be collected and analyzed to the DataFinder, and the subsequent user research agent can analyze the user behavior data reported to the DataFinder.<br><br>* If you want to combine some existing user portraits, tags, and other data in the business, you can report the corresponding data as user attribute data in the DataFinder, and analyze it based on behavioral event data and user attribute data for subsequent user research and analysis. |Data access supports various methods such as client side SDK collection and reporting, server level reporting, etc. For activity details, please refer to the [Finder data access overview ](https://www.volcengine.com/docs/84129/1261814). |


<span id="d5b16e97"></span>
## Create user groups

If you want to conduct cluster exploration, you need to create a user cluster on the DataFinder based on the client base characteristics to be explored before using AI behavior research, so that you can directly select it when using AI behavior research later. For activity details, see [user grouping ](https://www.volcengine.com/docs/84129/1261555).

<span id="1c6fa2ee"></span>
## Permission control

Since the AI behavior research function is a new beta function, the historical user role has no function operation permission by default. If you want users in the project to use the AI behavior research function, you need the project management to create a new user role and give the AI behavior research function permission. Take the SaaS cloud native environment as an example. For activity details, please refer to [fine grain permission control: DataFinder role management ](https://www.volcengine.com/docs/84129/1261715#%E7%BB%86%E7%B2%92%E5%BA%A6%E6%9D%83%E9%99%90%E7%AE%A1%E6%8E%A7%EF%BC%9Adatafinder%E8%A7%92%E8%89%B2%E7%AE%A1%E7%90%86).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the operation permission to directly add AI behavior research to historical roles is not supported.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7ec7fbc57cf414d9960cd74b8eba391~tplv-goo7wpa0wc-image.image) </span>

<span id="5942f349"></span>
# Using AI for Behavioral Research

<span id="caee6744"></span>
## AI Behavior Research Entrance

Once logged in to the User Research Agent console, click the top navigation **User Research Agent** \> **AI Behavior Research** to enter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df74cee93e184a7ea9a909ed6273d4e9~tplv-goo7wpa0wc-image.image) </span>

Currently supports grouping probing based on user grouping, and individual probing based on user user_id.

<span id="5dd691d2"></span>
## Create a business space

The user research agent provides you with the concept of business space. You can combine business scenarios, business classification and other factors to plan and create business space for business scenarios that need to be analyzed centrally. After the creation is completed, you can upload the event tracking range and event tracking related knowledge related to this business scenario in the business space to help the model understand the background knowledge and the significance of event tracking, improve the model's focus in the subsequent analysis process, and improve the quality of analysis results.

<span id="56349387"></span>
### Create a business space

Here are the instructions for creating a business space.


1. After logging in and entering the AI Behavior Research page, click "Manage Business Space" in the business space drop\-down box on the left side of the page, and click the Create Business Space button in the pop\-up window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fc1a8067c7e479e9baa276a40e30a77~tplv-goo7wpa0wc-image.image) </span>

2. Configure the name, description, space location, etc. of the business space in the pop\-up window. After completing the configuration, click the "Create" button to complete the creation of the business space.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2879d55c841248c0b406b84a0fff3f00~tplv-goo7wpa0wc-image.image) </span>

   The location of the space indicates whether the currently created business space is a public space visible to all users or a personal space visible to them.


<span id="7ee9da00"></span>
### Upload event tracking and knowledge

After the business space is created, you can upload business\-related event tracking and event tracking knowledge to the business space.


1. On the corresponding business space configuration page, click the "Import from File" button, and select the event tracking scope or business knowledge document related to this business scenario that needs to be imported according to the interface prompts.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f9bff14ca6d4c6b8b3d2806690d726c~tplv-goo7wpa0wc-image.image) </span>

   * Support for uploading multiple files in sequence. File types support CSV, XLSX, XLS, Markdown and other formats. Currently, documents in Word and PDF formats are not supported.

   * When uploading documents, a maximum of 200 words is supported for a single upload.

2. After uploading the offline document, click the "Confirm Import" button and wait for the uploaded document to be parsed. The model will perform event tracking and analysis and summary of business\-related content on the uploaded document.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently supports the analysis of event tracking scope and business\-related background knowledge based on uploaded documents.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The range of event tracking that will be parsed includes: general events, user properties, dimension tables, and currently does not support parsing virtual events.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When parsing the event tracking range, if the corresponding event is disabled or hidden, it will not be parsed.   </div>
   

3. After the parsing is complete, you can click "View and Confirm" to check the model parsing results.

   1. You can check whether the parsed event tracking and business knowledge are correct on the pop\-up confirmation page. If most of the content is accurate and there is a small amount of content that needs to be adjusted, you can directly edit and modify it. After completing the modification and confirming, click the "OK" button to complete the event tracking and upload the business knowledge.

   2. If you find a lot of errors in the parsed event tracking and business knowledge on the confirmation page, it means that the currently uploaded documents are of poor quality. You can return to the business space configuration page, click "Re\-Upload", re\-upload higher\-quality relevant documents, and re\-parse.

4. After uploading and parsing the relevant knowledge, when using the agent for analysis, you can automatically edit and modify it in the business space later.


<span id="9cf22b33"></span>
### Authorize business space

For personal business space, you can also choose to license the business space to certain users individually. After authorization, the corresponding users can view and use this business space.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e185b9e9f73344379e23b62153c13702~tplv-goo7wpa0wc-image.image) </span>

<span id="20321905"></span>
## Configuration Analysis Task: Cluster Probe

You can select the circled user groups on the "Group Probe" page, and refer to the following task configuration parameters to explain the configuration of the analysis task. After completion, click the "Send" button to start the group insight analysis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a41ec02a2fc45bdb3b7e2bb5b60f10c~tplv-goo7wpa0wc-image.image) </span>


|parameter |configuration instructions |
|---|---|
|User Grouping & Random Selection |* In the "User Groups" drop\-down box, select the created user groups to be analyzed.<br><br>* In the "Random Selection" configuration box, set the number of people to randomly select to analyze insights from the selected user subgroup. Currently, up to 100 users are randomly selected. |
|probe time |* The configuration is based on the behavioral data of the user to be analyzed in which time frame to perform user insight analysis.<br><br>* The default is yesterday; the exploration time cannot exceed 7 days. |
|Problem description |* In the problem description text box, enter the detailed description of the task that requires insight analysis. It is recommended to enter detailed analysis background, analysis insight goals, analysis requirements, and necessary prompt information (such as necessary business background knowledge and analysis ideas that can be tried) to ensure the depth of understanding of the business by the large model.<br><br>* At the top of the problem description text box, it is supported to further filter the scope of user behavior data to be analyzed through events, such as further clarifying the scope of user sessions to be analyzed based on events, and event tracking events that require insight analysis.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/171cdb1fb3cd4db382e3ea7fd17c2a80~tplv-goo7wpa0wc-image.image) </span><br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you upload the event tracking range and business knowledge in the business space, when performing event tracking filtering, it will automatically bring you the corresponding event tracking range and business background knowledge based on the configuration results of the current business space, which will help further narrow the scope of user data to be analyzed and improve the model's understanding of the business.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also make flexible adjustments to each individual analysis task based on this.   </div><br>   <br><br>* The problem description format is basically Markdown format, which supports content module separation through " `##`". The example is as follows.<br><br>   ```Markdown```<br>```   ## Background：```<br>```   These users are ordinary educated mothers who love to watch movies, TV shows, and celebrity content on xxAPP. They have been active on xxAPP, but play very few videos or have not played any videos on xxx video player APP```<br>```   ```<br>```   ## Task：```<br>```   Reason why users play fewer or no videos on the xxx video player app```<br>```   ```<br>```   ## Requirement：```<br>```   If users have actively expressed their behavior within the xxx video player app, such as searching, submitting, filming, commenting, replying to comments, etc., it should be specifically pointed out```<br>```   ```<br>```   ## Hint：```<br>```   1. From the perspective of the correlation between the consumption interests and preferences of xxAPP content and the content recommendations of xxx video player APP, it can be analyzed whether the displayed content is something that users may like```<br>```   2. From the perspective of accepting new materials, it can be considered whether the displayed content is unrelated to the user's new materials```<br>```   3. From the perspective of displaying similar content in a concentrated manner, can we consider whether similar art styles and types of content are frequently displayed, and whether users frequently experience rapid scrolling without playing?```<br>```   4. It can be considered from the perspective of search behavior whether users have search behavior but have not found satisfactory results```<br>```   ```<br>   <br><br>* The system has built\-in question templates for problem discovery, behavior summary, and intent analysis modules. You can choose the matching template according to your needs, and modify it based on the template to quickly build question content. |


<span id="00bf3687"></span>
## Configuration Analysis Task: Individual Probe

You can refer to the following task configuration parameters on the page to explain the configuration of the analysis task. After completion, click the "Send" button to start the insight analysis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d6f988b13fb4930a6168f332c44e55a~tplv-goo7wpa0wc-image.image) </span>


|parameter |configuration instructions |
|---|---|
|Insight into users |* You can enter the user UID of the insight to be analyzed in the Insights user text box.<br><br>* Supports multiple users to enter simultaneously.<br><br>   * When there are multiple users, multiple users are separated by line breaks.<br><br>   * When specifying multiple users, if the dates of each user to be probed are inconsistent, you can add the time and date range of each user to be probed after the user UID. When using this method, the configuration result of the probing date selection box below will not take effect.<br><br>      Examples are as follows:<br><br>      ```Plain```<br>```      107103****1,20251015,20251015```<br>```      107103****2,20251014,20251014```<br>```      ```<br>      <br><br>      Among them, `107103 **** 1`is the user UID, and `20251015 and 20251015`are the specified exploration date ranges, which are October 15, 2025. |
|probe time |* The configuration is based on the behavioral data of the user to be analyzed in which time frame to perform user insight analysis.<br><br>* The default is yesterday; the exploration time cannot exceed 7 days. |
|Problem description |* In the problem description text box, enter the detailed description of the task that requires insight analysis. It is recommended to enter detailed analysis background, analysis insight goals, analysis requirements, and necessary prompt information (such as necessary business background knowledge and analysis ideas that can be tried) to ensure the depth of understanding of the business by the large model.<br><br>* At the top of the problem description text box, it is supported to further filter the scope of user behavior data to be analyzed through events, such as further clarifying the scope of user sessions to be analyzed based on events, and event tracking events that require insight analysis.<br><br>* The problem description format is basically Markdown format, which supports content module separation through " `##`". The example is as follows.<br><br>   ```Markdown```<br>```   ## Background：```<br>```   These users are ordinary educated mothers who love to watch movies, TV shows, and celebrity content on xxAPP. They have been active on xxAPP, but play very few videos or have not played any videos on xxx video player APP```<br>```   ```<br>```   ## Task：```<br>```   Reason why users play fewer or no videos on the xxx video player app```<br>```   ```<br>```   ## Requirements：```<br>```   If users have actively expressed their behavior within the xxx video player app, such as searching, submitting, filming, commenting, replying to comments, etc., it should be specifically pointed out```<br>```   ```<br>```   ## Hints：```<br>```   1. From the perspective of the correlation between the consumption interests and preferences of xxAPP content and the content recommendations of xxx video player APP, it can be analyzed whether the displayed content is something that users may like```<br>```   2. From the perspective of accepting new materials, it can be considered whether the displayed content is unrelated to the user's new materials```<br>```   3. From the perspective of displaying similar content in a concentrated manner, can we consider whether similar art styles and types of content are frequently displayed, and whether users frequently experience rapid scrolling without playing?```<br>```   4. It can be considered from the perspective of search behavior whether users have search behavior but have not found satisfactory results```<br>```   ```<br>   <br><br>* The system has built\-in question templates for problem discovery, behavior summary, and intent analysis modules. You can choose the matching template according to your needs, and modify it based on the template to quickly build question content. |


<span id="b61b0115"></span>
## Check task progress

After submitting an analysis task, you can view the progress of each user's insight analysis on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f38c4812cdb5463e85c36d76aea730e4~tplv-goo7wpa0wc-image.image) </span>


* Each user's insight analysis is mainly divided into three sub\-analysis tasks: portrait analysis, behavior detailed investigation, and behavior insight. You can quickly view the analysis progress of sub\-tasks at the "task progress" in the upper left corner of the page. After completing the task analysis, the status of the corresponding sub\-tasks will change to the green "√" status.

* When all the sub\-tasks are completed, the overall insight analysis task of the current user is also completed. In the leftmost navigation bar, the insight analysis status of the corresponding user will change to the green "√" status, and you can switch to view the task progress status of each user.


<span id="ae700e66"></span>
## View analysis results

<span id="c14d3103"></span>
### Image analysis results

AI behavior research is based on user behavior data and user attribute data collected by DataFinder, and user portraits can be summarized through model capability analysis, including user identities, behavioral characteristics, user interests and other portrait conclusions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6fa493079d6473f8a224eea3444546a~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In order to obtain a more accurate and detailed user portrait analysis conclusion, it is recommended that you report the user portrait data that can assist in analysis, such as the user label to the user attribute data of DataFinder, to improve the reliability of the portrait analysis results.</div>


<span id="6ca00a4f"></span>
### Behavioral breakdown results

The behavior detail function can further enhance and summarize the complex and difficult\-to\-understand user behavior logs into semantic and refined user behavior stream descriptions, which can greatly reduce the context length in the model analysis process and improve the model's understanding of user behavior data, thereby enhancing the efficiency and accuracy of insight analysis conclusions.

You can do the following on the behavior details page:

Review the core session links in the current user insights analysis process, including the list of core sessions and the key behavioral links in each session.


* View the session details. Click on the event tag in the details and view the corresponding event properties on the right side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d9f5468c5174fac88dbcdf6025088fa~tplv-goo7wpa0wc-image.image) </span>

* On the **moving line** page, the user's behavior link in each core session can be easily viewed through the visual user behavior link diagram.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0244297fa7b4f4fb04b44accc84b2e3~tplv-goo7wpa0wc-image.image) </span>

* View the list of key events and event property details for the corresponding session in the **sequence details** on the right side of the page.

   * Supports viewing the event list of all sessions, and also supports selecting the specified session to view.

   * Support entering event or parameter keywords in the search box for query.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e57341da26f4fc58a762c1c5beb060a~tplv-goo7wpa0wc-image.image) </span>


<span id="4ce0dc3b"></span>
### Behavioral insights and drill\-down analysis

You can view individual insights and their arguments, and drill down to see detailed conversation and behavioral flow details in the arguments.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72a30d25e2fe439ba096d018b972577f~tplv-goo7wpa0wc-image.image) </span>

<span id="1297d093"></span>
## Summarize group characteristics

If you want to perform a summary analysis of these client bases after completing the insights analysis of multiple individual users, you can click "Summary Report" at the top of the page, and AI Behavior Research will summarize and analyze all current designated users for you, and generate a summary report on the group characteristics of the corresponding designated population.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f91d83ecdc0c47c390464f9723916383~tplv-goo7wpa0wc-image.image) </span>

The summary report will present you with the core insights and findings, and provide a comprehensive conclusion after the summary.

<span id="0da4f11e"></span>
## Interrogation and reanalysis


* **Individual Insight**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41c506231e3e4cea889cdcd7e7cf8755~tplv-goo7wpa0wc-image.image) </span>

   * If you have questions about the results of the analysis, or have other questions to be analyzed for this user, you can follow up in the question text box at the bottom of the page. When asking questions, the model will answer the questions for you based on the obtained portrait analysis results and behavioral scrutiny results.

   * You can also click the "Reanalyze" button in the upper right corner to reanalyze the current analysis task.

* **Summary report**

   * As depicted in the figure above, on the summary report page, you can also ask questions about an insight point.

      * You can click the "Ask" button after an insight point to ask questions in the pop\-up question text box.

      * In the future, you can view the follow\-up questions, problem analysis progress and other information associated with the current summary report in the "follow\-up tasks" in the upper right corner.

   * In the upper left corner of the page, click **re\-run** , and you can select the supplementary prompt word, the system will re\-run the summary report according to the prompt word requirements.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/323ab69bbac544cd9cb5402412c430b5~tplv-goo7wpa0wc-image.image) </span>


<span id="700bdfd8"></span>
# Trial experience

The User Research Agent provides you with a demo project for the trial experience. If you want to try the experience, you can contact the Volcano Engine technical support staff to apply for trial permission. After completion, you can switch to the "AI User Deep Research" project in the project toggle drop\-down box at the top right. In this project, you can try the experience.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/575b02dd26604aa8aaa79f066bb1fddc~tplv-goo7wpa0wc-image.image) </span>
