---
title: "Prerequisites and setup"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Configuration_Setup"
---

To provide more accurate item suggestions to your users, you can enable the personalized recommendation feature. This guide provides the required setup process, walking you through how to link and activate item and user event datasets in the correct order to begin generating user profiles and delivering effective recommendations. 

&nbsp;

This feature applies to scenarios such as product recommendations on e\-commerce platforms, post distribution in content communities, and content stream recommendations in video apps, helping to improve user engagement and conversion rates. 


---



To ensure the quality of these personas and the effectiveness of the recommendations, the system requires a **sufficient volume of data that can be effectively interpreted by Large Language Models (LLMs)** . Before officially enabling recommendations, please complete the following data configuration and validation tasks **in the specified order**.

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Overview</div>


<div data-tips="true" data-tips-type="default">You must first activate at least one item dataset, then link the behavior dataset, and finally activate the behavior dataset to start user profile extraction and creation.</div>


<span id="52a24ab5"></span>
# Prerequisites

Before using the recommendation feature, you must ensure the following two conditions are met:


1. **At least one linked and successfully activated Image & Text Dataset** (such as graphics or products). This forms the basis for user behavior analysis and recommendations.

2. **Prepare a linkable user behavior dataset**. Please note that linking and activating the behavior dataset must occur only after the Image & Text Dataset is linked and activated.


<span id="3d8ac512"></span>
# Setup steps

<span id="da21b1a4"></span>
## Step 1: Link and configure an item dataset


1. Select an application or create a new application. 

2. In your application, select **Configuration** and click the **Link Dataset** button.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/382dbfc9bb6946249e090de7a16fed5e" width="700px" /></div>



3. Select an item dataset. This item dataset should contain items that are to be recommended to the users. 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ced283ba0b774f28b81c7bfc56d444f1" width="600px" /></div>



&nbsp;

4. Click the **Next: Configure fields** button. Check LLM generated field description and data configuration to ensure it is accurate. 


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Searchable (Text) configuration is used in multi\-modal item\-to\-item recall. Ensure this is accurately configured with sufficient fields to represent each item in order to ensure high recommendation accuracy.</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/54e9b27bc51b430bb2d2b4c4da1b6635) </span>


&nbsp;

5. Click the  **Next: Configure display settings ** button. Configure default display fields that will be used in the Experience Page. 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/df8ef5d00c764adebe02feff17a310f2" width="700px" /></div>



6. Click **Done** to complete the two\-step configuration. The system will create the data configuration, conduct image understanding, trigger embedding of the item data and build data index. This process is necessary for subsequent user behavior analysis and recommendations.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d58f1f89d9564798943cee4f26a4548c" width="700px" /></div>



7. Depending on the data size, activation may take some time. Please wait until the status shows **Configuration Active**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not proceed to Step 2 before configuration has taken effect.    </div>
   

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/55bdf0069e1f4714b063c4e25d634a4d" width="700px" /></div>


&nbsp;

<span id="3a030193"></span>
## Step 2: Link User Event Dataset

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Ensure that <strong>the items referenced in the user event data</strong> have been uploaded to the Item dataset. </div>


<div data-tips="true" data-tips-type="warning"><strong>A low join rate between item IDs </strong>found in the user event data and those in the item dataset will <strong>severely degrade </strong>the quality of the recommendations. </div>



&nbsp;

1. Go to the User Event Dataset tab in the Configuration section and click the **Linked Dataset** button.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7f2424ed7f4f48d2bf990f7ed2bf3ae1" width="700px" /></div>



2. Select the target **User Event Dataset** and confirm.

   1. The popup **only** shows the applicable **User Event** datasets.

   2. Each app is limited to **1** User Event dataset linked at any point of time.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/738149a6ddb14fbeae4fe0a61a666efb" width="500px" /></div>



&nbsp;

3. Confirm data description to ensure the fields align with business definitions. 


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/19498205d7424a19bb2957563dd5a411" width="700px" /></div>



4. Click "**Done**"


&nbsp;

<span id="6f3e68bc"></span>
## Step 3: Historical user event backfill (optional)

After confirming the data configuration, the platform will provide one\-time historical data processing of historical data found in the dataset  **(up to past 7 days)** . If selected, the platform will automatically backfill historical user event data found in the user event dataset and utilise these user events to pre\-create user profiles to enable personalized recommendations. 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Fees</div>


<div data-tips="true" data-tips-type="default">By processing historical user event data, you will incur <strong>"</strong><strong>u</strong><strong>ser event data processing" </strong>fees. Processing fees for historical user event data will be charged per processed record.</div>



1. Select whether to process historical data in the user event dataset. 


&nbsp;


<columns>
<columnsItem zoneid="qexIEB2HHr">

<div style="text-align: center">
<strong>No Processing</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e071621fc5bf4bd2be6e34ea505210dc) </span>



</columnsItem>
<columnsItem zoneid="Y4a20LKRIn">

<div style="text-align: center">
<strong>Complete Processing</strong></div>


<div style="text-align: right">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f40c2c18e4304d619d5232d21b2dde17" width="400px" /></div>




</columnsItem>
<columnsItem zoneid="K4F3DhSwV3">

<div style="text-align: center">
<strong>Partial Processing</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/44726e017ca04a3fb8a7811e7f7b9990) </span>



</columnsItem>
</columns>



2. The platform will activate the user event dataset and start (or skip) the backfill task based on your choice.


<span id="40d6e196"></span>
## Step 4: Activate user event dataset


1. You can view the linked user event dataset through the interface. 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1929e1d6c29e49b8aebc9b6f1a5a6ac1) </span>


2. After the user event dataset is successfully activated, its status will automatically update to  **"Configuration active. Updates in real\-time". **  


&nbsp;

You have successfully completed the set\-up tasks and will be able to experience Viking AI Search personalized recommendation features. For more details, refer to [Features Overview](https://docs.byteplus.com/docs/viking-aisearch/Feature_Overview).


---



<span id="648c7bce"></span>
# Other Related Documentations

After successfully activating the user event dataset, you can:


1. Continue uploading user events via the platform interface and API. For details, please refer to [Write - Import and update data in real time](https://docs.byteplus.com/docs/viking-aisearch/Write_-_Import_and_update_data_in_real_time)

2. Experience personalized recommendation capabilities. For details, refer to [Features Overview](https://docs.byteplus.com/docs/viking-aisearch/Feature_Overview)


&nbsp;
