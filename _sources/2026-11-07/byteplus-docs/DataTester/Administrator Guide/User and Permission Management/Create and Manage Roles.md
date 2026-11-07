---
title: "Create and Manage Roles"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Create-and-Manage-Roles"
---

<span id="c4c9f56a"></span>
# Background information


* 4.8.0 and subsequent versions, there is only one default role: Administrator. New users in this version can plan roles and corresponding permissions according to business needs, manually create additional roles in the management center, and subsequently grant permissions to roles. To create a role, see the Creating a Role section below.

* 4.7.0 and previous versions, the system provides four roles by default, and administrators can modify the scope of permissions of the system default role or add new roles according to business needs.

   
   |Role name |Role Description |
   |---|---|
   |Administrator |Product members and roles can be managed |
   |Safety officer |All experiments can be closed, generally used to suspend the experiment urgently when the experiment affects the user's normal use. |
   |Experimenter |You can create experiments, view experiment details, experiment reports, and more. It is generally recommended that students who are involved in opening experiments and modifying experimental information apply. |
   |Analyst |You have read\-only permissions for experiments under the product, you can edit test users, and you cannot create experiments. It is generally used for experimental analysis, experimental function acceptance testing, and other scenarios. |
   


4.8.0 and later, you need role management in the admin center.

<span id="a773d2f3"></span>
# Precautions

Only accounts with the permission to create new roles can operate to create roles, and accounts with role management rights can perform management operations such as editing and modifying roles.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1902b78aba3e41ebb7b077cecf338a58~tplv-goo7wpa0wc-image.image) </span>

<span id="cdcb1d4d"></span>
# Create role

After entering the **management center** of the privatization platform, you can click **New Role** on the **Users and Organizations** \> **Role Management** page. Configure the basic information of the role, role permissions, and role members in the pop\-up page. When finished, click **Create** in the upper right corner to complete the role creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05fc9d5b766640cfbcacfce2635a1f8e~tplv-goo7wpa0wc-image.image) </span>

Of which:


* **Select Open Products** : Select which products the role needs to be opened to according to your needs. After selecting Open to the **A/B test platform**, the subsequent newly created roles will be synchronized to the role list page of the A/B test.

* **Member role** : Select Add user, which is then associated with this role and has all permissions for this role.


<span id="a0964ed8"></span>
# Role authorization

4.8.0 and later, you need to authorize roles in the admin center.


1. Authorize roles.

   After entering the **management center** of the privatization platform, you can **grant permissions** \> **by role** page, select the role that needs to be authorized, and grant the corresponding permissions to the role.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d91ac4823114019a8f6b2b6ee9517de~tplv-goo7wpa0wc-image.image) </span>

   1. On the **Console** tab, click **Edit** to privatize the platform console overall permission details for the role.

   2. Click the **A/B Test Platform** tab to grant the role the **project, function, property desensitization** permission details for A/B testing.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">4.9.0 version has upgraded the details of DataTester's authorizability, adding configurations that support permission control such as attribute desensitization.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When operating for the first time, you need to perform synchronization and other operations according to the interface prompts.      </div>
      

2. Add members to roles and grant role permissions to members.

   Click Details to the right of **Role Members** at the top, and click Edit Member in the pop\-up sidebar to jump to the Role Edit page to add members to the role. The added member has the permissions that this role has.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf0fc072f3c345e6bbd09e6ab72655ff~tplv-goo7wpa0wc-image.image) </span>


<span id="6373a982"></span>
# Edit, copy, delete roles

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5202099891844f8088879cb4c8ec9741~tplv-goo7wpa0wc-image.image) </span>
