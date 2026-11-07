---
title: "Feature Management"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Feature-Management"
---

<span id="fe0f66e6"></span>
# Background information

DataTester provides you with fine grained permission control of Feature resource entities to meet the following permission control scenarios.


* The function is divided into different levels or attributes, and the authority control is carried out in a fine grain, which can enhance the security of data to a certain extent and enhance the stability of related business.

* With different permissions, different items can be viewed and operated to avoid a series of negative problems caused by misoperation.

* Responsibilities require different pages/information, and providing the most effective information can improve operational efficiency and avoid distractions caused by irrelevant pages.


<span id="0737bdf4"></span>
# Set Feature Action Permissions for User Roles

<span id="07974b9c"></span>
## Permission description

The granularity of permission control for Features can be subdivided into viewing Feature List/Details ( **viewing permissions** ), creating/editing Features (**collaborator permissions**), and managing feature whitelists.

The scope of operations that can be performed on a Feature at the permission control granularity is as follows.


|**Feature operation type** |View Feature List/Details<br><br>( **View Permissions** ) |New/Editing Features<br><br>( **Collaborator permission** ) |Management feature whitelist<br><br>( **Collaborator permission** ) |
|---|---|---|---|
|View Feature details page |✔️ |✔️ |✔️ |
|View Feature History |✔️ |✔️ |✔️ |
|Enable Features |Not supported |✔️ |Not supported |
|Close Features |Not supported |✔️ |Not supported |
|association experiment |Not supported |✔️ |Not supported |
|Editing Features |Not supported |✔️ |Not supported |
|Remove Features |Not supported |✔️ |Not supported |
|rights management |Not supported |✔️ |Not supported |
|whitelist test |Support, create/edit my whitelist |✔️ |support |


When controlling the permissions of a Feature, it is actually granting the Feature's view permissions and collaborator permissions to the DataTester user roles.

<span id="1684810e"></span>
## Operation guidance

After logging in and entering the product console, enter the Administration Center \> Permissions Granted \> By Role page to modify the Feature operation permissions of the role.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23e6ee9880e3414b9fb55194feb3aa30~tplv-goo7wpa0wc-image.image) </span>

<span id="8c48a7a8"></span>
# Set Feature Type

<span id="c0f9e8b7"></span>
## Permission description

Features in DataTester can be divided into two categories: "Public Features" and "Private Features". The default relationships between different roles and different types of Features are as follows:


|Classification |**Group administrator** |**App administrator** |**Feature Creator** |**User** |
|---|---|---|---|---|
|Public Features |View permissions, collaborator permissions |View permissions, collaborator permissions |View permissions, collaborator permissions |View permission |
|Private Features |View permissions, collaborator permissions |View permissions, collaborator permissions |View permissions, collaborator permissions |Invisible |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Newly created features default to public features.</div>


<span id="ed472222"></span>
## Operation guidance

Log in and enter the Feature List page of DataTester, and click "Actions \- Rights Management" to make type modifications to the created Features. Newly created features default to public features.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only users with "Collaborator Permissions" can click this option to manage permissions.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/102dbb3dd6094b2cbb535e568e40af56~tplv-goo7wpa0wc-image.image) </span>


* Public Features, "Group Administrators, App Administrators, Feature Creators" of the current group application have "Collaborator Rights" by default. **Users who currently have access to the app have "View Permissions" by default.** 

* Private Feature, "Group Administrator, App Administrator, Feature Creator" of the current group application has "Collaborator Rights" by default.
