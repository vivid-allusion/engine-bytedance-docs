---
title: "Managing the Content industry attributions"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-managing_the_content_industry_attributions"
---

Attribution is the way BytePlus Recommend determines how recommendations contribute to a user's clicks on a recommended content, the duration of time spent on the recommended content, or others. Attribution is key in optimizing the recommendation objectives and results. Through the Attribution section in the BytePlus Recommend console, you can customize your attributions through the attribution keys, inherited attribution fields, attribution nodes, and more.

There are several types of attributions that you can choose from:


* impression.

* click.

* stay.

* other customized event types.


<span id="2d1dcf3d"></span>
# Navigating to the Attribution screen

You can navigate to the Attribution screen using the BytePlus Recommend console.

**To navigate to the Attribution screen:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to modify.

3. Under the Attribution section, click the edit icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f8467b061fc4c20ba32dd1a38be91b9~tplv-goo7wpa0wc-image.image) </span>

   The Edit attribution screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22b3a192933947ae92925042c4a453d4~tplv-goo7wpa0wc-image.image) </span>


<span id="009c3543"></span>
# Managing attributions

You can manage the attributions through the Edit Attribution screen. You can customize the default configuration of the attribution keys and the inherited attribution fields. Actions include choosing from the pre\-populated attribution keys available, scene configuration, and using the advanced options.

<span id="14825517"></span>
## Modifying attribution scene configurations

You can customize the default attribution scene through the Edit Attribution screen.

There are two types of scenes available:


* **Full scene**: The attribution applies to all scenes.

* **Custom scene**: The attribution only applies to selected scenes.


**To modify the attribution scene configuration:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The edit and delete icons appear.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5efbc3423b046288eb2d35348a9c097~tplv-goo7wpa0wc-image.image) </span>

3. Click the edit icon.

   The edit attribution pop\-up window appears.

   The default setting is Full scene.

4. Select the scene that applies to this attribution.

   If you selected **Custom scene**, the drop\-down box appears.

5. Select the Custom scene that applies to this attribution.

6. Click **Save**.

   The attribution's scene configurations are saved.


<span id="2dbeb744"></span>
## Modifying attribution keys

Attribution keys are a set of rules which determine whether to credit a user event to the product recommendations functionality\*.\* All attribution keys have at their centre several user events that are triggered by the users in regards to the product recommendations. These events are clicks on recommended products, additions to cart and purchases. Only event types sharing identical attribution keys can be attributed, thereby influencing all subsequent paths originating from the node. You can customize the default attribution keys through the Edit Attribution screen.

**To modify the attribution keys:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The edit and delete icons appear.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/406e4b05625d4b2fbef879f3cb64dafa~tplv-goo7wpa0wc-image.image) </span>

3. Click the edit icon.

   The edit attribution pop\-up window appears.

4. Click the drop\-down menu for more attribution key options.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95db565df89f4837bb6edae877884621~tplv-goo7wpa0wc-image.image) </span>

5. Select or unselect the attribution keys that you want.

6. Click **Save**.

   The attribution keys are saved.


<span id="30e75ec1"></span>
## Adding Additional Attribution Inheritance

The attribution node's advanced options ensures that additional attributes are applied to the subsequent nodes in all pathways. For example, to ensure `scene_name` is applied consistently to all upstream paths leading to the `conversion` node, it is essential to select this `scene_name` as an additional attribution inheritance.

**To add the attribution node's Additional Attribution Inheritance:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The edit and delete icons appear.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/406e4b05625d4b2fbef879f3cb64dafa~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. Click the edit icon.

   The edit attribution pop\-up window appears.

4. Under the Advanced options section, click the drop\-down menu.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aed00b7fda2248bbbe33dbd4ca84c0f9~tplv-goo7wpa0wc-image.image) </span>

5. Select the applicable fields.

6. Click **Save**.

   The advanced options are saved and applied to the following nodes.


<span id="c4f4204d"></span>
## Deleting attribution nodes

You can delete the attribution node if needed through the Edit attribution screen.

**To delete a attribution node:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The edit and delete icons appear.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef622d693762416592913a39dd668497~tplv-goo7wpa0wc-image.image) </span>

3. Click the delete icon.

   The *Are you sure to delete this node* pop\-up window appears.

4. Click OK.

   The node is deleted.


<span id="1b009696"></span>
## Adding new node flows

You can add new node flows using the Edit attribution screen within the BytePlus Recommend console.

**To add a new node flow:** 


1. Navigate to the Edit attribution screen.

2. Click **Add new node**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a3576e8a986451999d257ec6da7f4c5~tplv-goo7wpa0wc-image.image) </span>

   The Add new node option appears.

3. Click the attribution category you want.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a8f15a56ae14fbda9064d96ba3760e3~tplv-goo7wpa0wc-image.image) </span>

   The new node is added.

4. Click the edit icon.

   The edit attribution pop\-up window appears.

5. Modify the attribute if necessary.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b467c0418df417e8136c6cd22a5d1d3~tplv-goo7wpa0wc-image.image) </span>

6. Click **Save**.

7. Add nodes to the existing attribution flow if needed.

   The attribution flow is created.


<span id="50bfeb40"></span>
## Adding nodes to existing attribution flows

You can add nodes to an existing attribution flow through the Edit attribution screen.

**To add a node to the existing attribution flow:** 


1. Navigate to the Edit attribution screen.

2. Click the node you want to configure.

   The plus icons appear on the left and right of the node

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb8a9aa083614185a8731ff6812e6b6d~tplv-goo7wpa0wc-image.image) </span>

3. Click the plus icon.

   The Add new node option appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d36d125235740bfafb72590d1812c3e~tplv-goo7wpa0wc-image.image) </span>

4. Click the attribution category you want.

   The new node flow is added.

5. Click the edit icon.

   The edit attribution pop\-up window appears.

6. Modify the attribute if necessary.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b467c0418df417e8136c6cd22a5d1d3~tplv-goo7wpa0wc-image.image) </span>

7. Click **Save**.

   The attribution flow is saved.


<span id="070b49ef"></span>
## Modifying the attribution node path properties

You can modify the attribution node path properties through the Edit attribution screen. This includes modifying the node priority and attribution window from node to node:


* **Priority**: Each node has default priority 1. When there are two node flows, we will first look at the priority where the high priority path overrides the low priority's (for example, Priority 1 is higher than Priority 2). If the priorities are the same between multiple attributes, we will compare the products and use the last\-clicked product amongst all the flows.

* **Attribution window**: This is a predefined period of time during which product recommendation events and subsequent purchases can be claimed to be related. Depending on the implementation of the purchase attribution rules, there can be multiple attribution windows.


**To modify the attribution node path properties:** 


1. Navigate to the Edit attribution screen.

2. Click on the arrow between the nodes you want to configure.

   The edit icon appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b0527e1682642aba98b8b7e10d78d60~tplv-goo7wpa0wc-image.image) </span>

3. Click on the edit icon.

   The edit node flow properties pop\-up window appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c69b2dcf92b44b7b8d1f50c30060e3e8~tplv-goo7wpa0wc-image.image) </span>

4. Modify the **Priority**.

5. Modify the **Attribution window** by entering the time in integer numbers.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can select from seconds, minutes, hours, and days.   </div>
   

6. Click outside the edit node flow properties pop\-up window.

   The attribution node flow properties are saved.


<span id="5ad252e0"></span>
## Clearing attribution configurations

You can clear all the attribution configurations using the Edit Attribution screen.

**To clear the attribution configurations:** 


1. Navigate to the Edit attribution screen.

2. Click **Clear**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4052013798c4ce68c868c54f315e99f~tplv-goo7wpa0wc-image.image) </span>

   The Confirm pop\-up window appears.

3. Click **OK**.

   The configurations are removed.


<span id="67d83677"></span>
## JSON configuration

The JSON configuration setting is used to review or debug the settings. You can use the **Copy code** function to copy the sample code into your own device.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/675b66e793f9412fb9a5836e96d26501~tplv-goo7wpa0wc-image.image) </span>

<span id="a13925be"></span>
## Adding Global Attribution configurations

You can add configurations to all the existing attributions using the Global Attribution function. Configure the additional attributes to inherit from upstream in all pathways to every node. Once it is set using the Global config function, it will be automatically applied to every node.

**To add a global attribution configuration:** 


1. Navigate to the Edit attribution screen.

2. Click **Global config**.

   The Additional Attribution Inheritance pop\-up window appears

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90b856faf89f49e880a30be7b089a9b2~tplv-goo7wpa0wc-image.image) </span>

3. Using the drop\-down menu, select the **Additional** **Attribution fields**.

4. Click **Save**.

   The global attribution configuration is set.
