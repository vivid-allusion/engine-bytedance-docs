---
title: "Managing the Retail industry attributions"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-managing_the_retail_industry_attributions"
---

Attribution is the way BytePlus Recommend determines how recommendations contribute to sales, conversions, or other goals. Attribution is key in optimizing the recommendation objectives and results. Through the Attribution section in the BytePlus Recommend console, you can customize your attributions through the attribution keys, inherited attribution fields, attribution nodes, and more.

There are several types of attributions that you can choose from:


* impression.

* click.

* purchase.

* add\-to\-cart.

* remove\-from\-cart.

* add\-to\-favorites.

* remove\-from\-favorites.

* purchase.

* search.

* checkout.


<span id="1259b8b2"></span>
# Navigating to the Attribution screen

You can navigate to the Attribution screen using the BytePlus Recommend console.

**To navigate to the Attribution screen:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to modify.

3. Under the Attribution section, click the edit icon.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cba303fcf204a56a1c60998b8df411d~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The Edit attribution screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e60f1196408a448b9f229926fba32102~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   


<span id="2596b0b1"></span>
# Managing attributions

You can manage the attributions through the Edit Attribution screen. You can customize the default configuration of the attribution keys and the inherited attribution fields. Actions include choosing from the pre\-populated attribution keys available, scene configuration, and using the advanced options.

<span id="3a01bfdd"></span>
## Modifying attribution scene configurations

You can customize the default attribution scene through the Edit Attribution screen.

There are two types of scenes available:


* **Full scene**: The attribution applies to all scenes.

* **Custom scene**: The attribution only applies to selected scenes.


**To modify the attribution scene configuration:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The edit and delete icons appear.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b77940330b544ca2af05e79a6c230035~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. Click the edit icon.

   The edit attribution pop\-up window appears.

   The default setting is Full scene.

4. Select the scene that applies to this attribution.

   If you selected **Custom scene**, the drop\-down box appears.

5. Select the Custom scene that applies to this attribution.

6. Click **Save**.

   The attribution's scene configurations are saved.


<span id="19bbade2"></span>
## Modifying attribution keys

Attribution keys are a set of rules which determine whether to credit a user event to the product recommendations functionality\*.\* All attribution keys have at their centre several user events that are triggered by the users in regards to the product recommendations. These events are clicks on recommended products, additions to cart and purchases. Only event types sharing identical attribution keys can be attributed, thereby influencing all subsequent paths originating from the node. You can customize the default attribution keys through the Edit Attribution screen.

**To modify the attribution keys:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The edit and delete icons appear.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b77940330b544ca2af05e79a6c230035~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. Click the edit icon.

   The edit attribution pop\-up window appears.

4. Click the drop\-down menu for more attribution key options.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a6551bf9cef4edea7045288ecb05b1e~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

5. Select or unselect the attribution keys that you want.

6. Click **Save**.

   The attribution keys are saved.


<span id="3bf938b2"></span>
## Adding Additional Attribution Inheritance

The attribution node's advanced options ensures that additional attributes are applied to the subsequent nodes in all pathways. For example, to ensure `scene_name` is applied consistently to all upstream paths leading to the `conversion` node, it is essential to select this `scene_name` as an additional attribution inheritance.

**To add the attribution node's Additional Attribution Inheritance:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The edit and delete icons appear.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b77940330b544ca2af05e79a6c230035~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. Click the edit icon.

   The edit attribution pop\-up window appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5278815776841cebaad4972ac0189a4~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

4. Under the Advanced options section, click the drop\-down menu.

5. Select the applicable fields.

6. Click **Save**.

   The advanced options are saved and applied to the following nodes.


<span id="744cf4a7"></span>
## Deleting attribution nodes

You can delete the attribution node if needed through the Edit attribution screen.

**To delete a attribution node:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The edit and delete icons appear.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e8dca1f63224d609613c11375cfe835~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. Click the delete icon.

   The *Are you sure to delete this node* pop\-up window appears.

4. Click OK.

   The node is deleted.


<span id="17dde9f9"></span>
## Adding new node flows

You can add new node flows using the Edit attribution screen within the BytePlus Recommend console.

**To add a new node flow:** 


1. Navigate to the Edit attribution screen.

2. Click **Add new node**.

   The Add new node option appears.

3. Click the attribution category you want.

4. Click the edit icon.

   The edit attribution pop\-up window appears.

5. Modify the attribute if necessary.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6987064862e847df83c68792a99f2f9e~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

6. Click **Save**.

7. Add nodes to the existing attribution flow if needed.

   The attribution flow is created.


<span id="e96972d2"></span>
## Adding nodes to existing attribution flows

You can add nodes to an existing attribution flow through the Edit attribution screen.

**To add a node to the existing attribution flow:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The plus icons appear on the left and right of the node.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92dfaf78bf81482690e84f318fb0fcf2~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. Click the plus icon.

   The Add new node option appears.

4. Click the attribution category you want.

5. Click the edit icon.

   The edit attribution pop\-up window appears.

6. Modify the attribute if necessary.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6987064862e847df83c68792a99f2f9e~tplv-goo7wpa0wc-image.image) </span>

7. Click **Save**.

   The attribution flow is saved.


<span id="a4c345c1"></span>
## Modifying the attribution node path properties

You can modify the attribution node path properties through the Edit attribution screen. This includes modifying the node priority and attribution window from node to node:


* **Priority**: Each node has default priority 1. When there are two node flows, we will first look at the priority where the high priority path overrides the low priority's (for example, Priority 1 is higher than Priority 2). If the priorities are the same between multiple attributes, we will compare the products and use the last\-clicked product amongst all the flows.

* **Attribution window**: This is a predefined period of time during which product recommendation events and subsequent purchases can be claimed to be related. Depending on the implementation of the purchase attribution rules, there can be multiple attribution windows.


**To modify the attribution node path properties:** 


1. Navigate to the Edit attribution screen.

2. Click on the arrow between the nodes you want to configure.

   The edit icon appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f01527ea27542678eaa65c27378d280~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. Click on the edit icon.

   The edit node flow properties pop\-up window appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dea83c9accf43328759548fad381182~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

4. Modify the **Priority**.

5. Modify the **Attribution window** by entering the time in integer numbers.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can select from seconds, minutes, hours, and days.   </div>
   

6. Click outside the edit node flow properties pop\-up window.

   The attribution node flow properties are saved.


<span id="12c47ba2"></span>
## Clearing attribution configurations

You can clear all the attribution configurations using the Edit Attribution screen.

**To clear the attribution configurations:** 


1. Navigate to the Edit attribution screen.

2. Click **Clear**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d6ed824cf18476fa13486f675d123f4~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The Confirm pop\-up window appears.

3. Click **OK**.

   The configurations are removed.


<span id="a51b2e97"></span>
## JSON configuration

The JSON configuration setting is used to review or debug the settings. You can use the **Copy code** function to copy the sample code into your own device.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88ed58fc3102441587cbd6a2867387f3~tplv-goo7wpa0wc-image.image" width="864px" /></div>


<span id="e6971b6f"></span>
## Adding Global Attribution configurations

You can add configurations to all the existing attributions using the Global Attribution function. Configure the additional attributes to inherit from upstream in all pathways to every node. Once it is set using the Global config function, it will be automatically applied to every node.

**To add a global attribution configuration:** 


1. Navigate to the Edit attribution screen.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e60f1196408a448b9f229926fba32102~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

2. Click **Global config**.

   The Additional Attribution Inheritance pop\-up window appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ec624046ee04801a4ab58a9fe4d4b6d~tplv-goo7wpa0wc-image.image) </span>

3. Using the drop\-down menu, select the **Additional** **Attribution fields**.

4. Click **Save**.

   The global attribution configuration is set.
