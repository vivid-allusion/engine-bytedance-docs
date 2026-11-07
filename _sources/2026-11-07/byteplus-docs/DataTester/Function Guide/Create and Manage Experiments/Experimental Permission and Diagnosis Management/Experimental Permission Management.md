---
title: "Experimental Permission Management"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Experimental-Permission-Management"
---

<span id="一-概述"></span>
# Overview

Permission management generally refers to the security rules or security policies set by the system, allowing users to access only authorized resources.

**Why do permission management?** 


* The function is divided into different levels or properties, and the authority control is carried out in a more fine grain, which can enhance the security of data to a certain extent and enhance the stability of related business;

* With different permissions, the items that can be viewed and operated are different, avoiding a series of negative problems caused by misoperation;

* Responsibilities require different pages/information, and providing the most effective information can improve operational efficiency and avoid distractions caused by irrelevant pages.


"A/B Testing" provides users with fine grain permission control of "Experiment" resource entities, and newly created experiments default to public experiments.

<span id="89cb7d75"></span>
# Permission model

The permission model is divided into two categories: "public experiment" and "private experiment". The relationship between different roles and different permission models is as follows:


|Classification |**Group administrator** |**App administrator** |**Experiment creator** |**User** |
|---|---|---|---|---|
|Public experiment |View permission |View permission |View permission |View permission |
|Private experiment |View permission |View permission |View permission |Invisible |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>In fact, the authorization is only for ordinary users/roles, and "view permission" can be granted.</strong></div>



|**Operation type** |**View permission** |
|---|---|
|View the experiment details |Support |
|View the experimental report |Support |
|View the experimental operation history |Support |
|Associated Features |Not supported |
|Freezing/thawing experiment |Not supported |
|Modify the experiment |Not supported |
|Diagnostic test |Not supported |
|Replication experiment |Not supported |
|Debugging experiment |Not supported |
|Start the experiment |Not supported |
|End the experiment |Not supported |
|Delete experiment |Not supported |
|Permission management |Not supported |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Group administrator</strong> refers to the administrator of the current group, such as the group administrator of the "Demo Experience" group.</div>


* <div data-tips="true" data-tips-type="tip"><strong>App administrator</strong> refers to the current group access application app administrator. For example, the app administrator of "e\-commerce APP, education APP, Mini Program Demo, web\-end Demo, mobile end Demo" applications under the "Demo Experience" group.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Role</strong>: You can add roles in "Group Management \- Role Management", and you can open the "app administrator, member" permission of an application for ordinary users.</div>



<span id="76f7013a"></span>
# Operation steps

<span id="279247db"></span>
## Operation entrance


1. After logging into the console, select "A/B Testing \> Experiment List" in the left navigation bar.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df497286691f451492cd6e04512bbc43~tplv-goo7wpa0wc-image.image) </span>

2. On the Experiment List page, click "More \- Permission Management" in the "Actions" column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a5d015322ca4d0fbad58184f9b1682d~tplv-goo7wpa0wc-image.image) </span>


<span id="18a73cbd"></span>
## Add permissions for public experiments


1. In the "Experiment Permission Management" pop\-up window, select "Public Experiments".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Public Experiment:</strong> Users who currently have access to the app have "View Permissions" by default.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ce710b2e8854a7e88682ee4a16d7727~tplv-goo7wpa0wc-image.image) </span>

2. If you want to add a user as a collaborator of the experiment, you need to set the user as an experimenter. You can click "System Administration \> Permission Management" on the left.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b0166b99b654d80844fea155e49d956~tplv-goo7wpa0wc-image.image) </span>


<span id="52999c84"></span>
## Add permissions for private experiments


1. In the "Experiment Permission Management" pop\-up window, select "Private Experiment".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Private experiment:</strong> The "group administrator, app administrator, experiment creator" of the current group application has "permissions" by default.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8fea01da6db4e72a1b5eeb94b018944~tplv-goo7wpa0wc-image.image) </span>

2. In the "Experimental Permission Management" pop\-up window, click "Add User Role".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65b91ecff089454c934a10a213ddf2f4~tplv-goo7wpa0wc-image.image) </span>

3. Select the user/role, enable the viewing permission, and then click "OK".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec674f02b851428fa7fd5a1234c8b1e9~tplv-goo7wpa0wc-image.image) </span>
