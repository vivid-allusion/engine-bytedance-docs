---
title: "Managing Recommendation Scenarios"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Recommendation_Scene"
---

To manage the complete lifecycle of your recommendation scenarios, you can follow the instructions in this guide. It provides step\-by\-step process for creating new scenarios, deploying it to your production environment, and safely deleting it when it is no longer required.

<span id="bc2ae15c"></span>
## Create Scenario 


1. Navigate to the ** Experience center** \> **Recommendation** module.

2. Click to create a new recommendation scenario


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b68de56a2c7a4291a65a44645b61a30d) </span>


3. Configure basic information


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bae68afdf352437facc52f80fc8563ab) </span>


|**Configuration** |**Description** |
|---|---|
|Configuration name |Customize the recommended scenario name (up to 50 characters, we recommend including business scenario keywords for easier management). |
|Recommendation scene |Select recommendation scene type<br><br><br>1. Recommended for you: Recommendation based on user profile. <br><br>2. Related items: Recommendation based on item relevance and user profile.  |
|Recommendation scene name |**Identify the "Interaction Interface" for this scenario:** <br><br>This setting drives the **automatic exposure data extraction task**, which tracks which items a user has already seen. Ensure that this configuration is accurate. <br><br>For more information, refer to [Deduplicate Previously Exposed Items](https://docs.byteplus.com/docs/viking-aisearch/Remove_items_exposed_to_users).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Not seeing any options?</div><br><br><br><div data-tips="true" data-tips-type="default">Selections are automatically extracted from the field tagged with the <code>scene name</code> attribute in the user event dataset. Ensure this field is accurately populated in the user event data. </div><br> |
|Item dataset for recommendation |**Source item dataset for recommendations**<br><br>Link a specific item dataset to this scenario to define the pool of items available for recommendation. In the "Item Dataset" dropdown menu, select an **already active** item dataset. |



4. Click **OK** to create the scenario. After creating the recommendation scenario, you should be automatically redirected to the recommendation experience page.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c20fb8ea372645e68514914de7099691) </span>

&nbsp;


---



<span id="36be5bc4"></span>
## Deploy Scenario

After completing testing on the platform, deploy the latest configuration to production in 2 easy steps.


1. **Trigger deployment process**: Click the **Sync changes to API ** button at the top right of the page to publish the configuration.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a211eed1d4074aa3805983b2d16f8e2d) </span>


&nbsp;

2. **Review release**: Select strategies you want to publish. The platform supports simultaneous deployment of strategies for Search, Conversational Search, and Recommendation. N**ew configuration will take effect immediately upon update and will overwrite the previous version.** 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/67fdfbd304ff4f9eaa278cabbf9f24a1) </span>


---



<span id="b9e99682"></span>
## Delete Scenario

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="danger">Recommendation API requests towards this scenario will fail immediately after deletion and will return an error. <strong>Deletion is permanent and deleted scenarios cannot be recovered.</strong></div>



1. Click on the 3 dots to display additional actions. Click on Delete **.**  


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f1700b1965c94ccf9b0ef196e83bdffa" width="700px" /></div>



&nbsp;

2. A confirmation popup will be triggered to prevent accidental deletion. To confirm deletion, type "Delete" and click "Delete".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b60fb4a1468c4ee18d45fecd2d6521c8" width="800px" /></div>


&nbsp;

&nbsp;
