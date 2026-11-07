---
title: "Permission Strategy"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Permission_Strategy"
---

As resources and tasks are used in a project, the system automatically creates corresponding pre\-built policies within the project, which can be directly used to associate roles. It also supports adding custom permission policies to set detailed permissions for resource pools, resource files, tasks, and other resources.

<span id="9785e6f3"></span>
## Prerequisites

You must be the project lead or a project administrator (Project_Admin) to perform policy\-related operations in the project. Please ensure that project members have been added and their roles associated, see [添加项目成员](https://docs.byteplus.com/docs/undefined/655468147c29cc0301edef1f#a45bfca3).

<span id="394a75d4"></span>
## Create Custom Policies


1. Log in to [BytePlus Flink Console](https://console.volcengine.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation panel, select **Project Management**, perform a fuzzy search based on the project name in the search box, and then click on the project block to enter the project.

4. In the project's left navigation panel, select **Access Management**.

5. On the **Access Management** page, click the **Policy** tab, then click **Create Policy**.

6. On the Create Policy page, set the policy name, service object, configuration method, and other key parameters, then click the confirm button at the bottom right of the page.

   After the policy is created, return to the policy list page. After creating the policy, it can be bound to a role; please refer to [为角色关联策略](https://docs.byteplus.com/docs/undefined/655468147c29cc0301edef20#e021cf89).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f5ca9d22e0749bbb55af128597cb112~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Strategy Name |Customize the strategy name.<br><br>Supports Chinese characters, uppercase and lowercase letters, numbers, underscore (_), and hyphens (\-), but cannot start with a number or a hyphen (\-). Character length must be between 1 and 65. |
   |Description |Provide a descriptive statement for the strategy. |
   |Configuration Method |Select the method to configure the strategy:<br><br><br>* (**Recommendation**) Visual Configuration: Simply select resource objects and operations directly on the current visual web page, making the configuration simple and efficient.<br><br>* JSON Configuration: Utilizes the JSON configuration method, requiring familiarity with JSON syntax and an understanding of permission policies. If you choose this configuration method, you must directly implement the permission policy configuration in the JSON statements, which demands high technical skill. |
   |Effect |The current effect mechanism is all about **allowing**, meaning all configured policies permit operations on certain resources and services. |
   |Service |From the drop\-down list, select the target object for the policy, with selectable objects including tasks, JAR resources, Hive, resource pools, etc. |
   |Resource |After selecting the policy service object, you need to choose the target resource for the service object.<br><br><br>* All resources: You have permission for all resources under the service object.<br><br>* Specific Resources: Access limited to selected resources only. |
   |Actions |After identifying the specific subjects and resources targeted by the policy, you need to establish the most crucial part of the policy: the permitted actions.<br><br><br>* All Actions: Full operational permissions for resources within the policy.<br><br>* Specific Actions: Limited permissions for selected actions, such as starting, stopping, debugging, and updating tasks. |
   


<span id="09e7193b"></span>
## Associate members with the policy


1. In the policy list, click **Associate Members** next to the custom policy, or click the policy name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61eff83e4fb741b2be6e5aa7fb9c1992~tplv-goo7wpa0wc-image.image) </span>

2. Under the **Associate Members** tab, click **Add Members**.

3. In the **Add Members** dialog, check the target members, then click **Confirm**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_925b1bdf176b460fbf883ed4d581a8cc.png) </span>


<span id="6f06badf"></span>
## Remove members associated with the policy


1. In the policy list, click **Associate Members** next to the custom policy, or click the policy name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61eff83e4fb741b2be6e5aa7fb9c1992~tplv-goo7wpa0wc-image.image) </span>

2. Under the **Associated Members** tab, click **Remove** behind the target member.

3. In the confirm removal of member dialog, click **Delete**.


<span id="424042b1"></span>
## Associate roles with the policy


1. In the policy list, click **Associate Role** behind the custom policy, or click on the policy name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccfe98ab9b3e4195a17507e06bd112cf~tplv-goo7wpa0wc-image.image) </span>

2. Under the **Associated Roles** tab, click **Add Role**.

3. In the **Add Role** dialog, select the target role, then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25349740b7854772920b81245e40a024~tplv-goo7wpa0wc-image.image) </span>


<span id="32345ac9"></span>
## Remove associated roles from the policy


1. In the policy list, click **Associate Role** behind the custom policy, or click on the policy name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccfe98ab9b3e4195a17507e06bd112cf~tplv-goo7wpa0wc-image.image) </span>

2. Under the **Associated Roles** tab, click **Remove** behind the target role.

3. In the confirm removal of role dialog, click **Delete**.


<span id="9b18b361"></span>
## View policy content


1. On the policy list page, click **Operation** in the **Policy Content** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abfb7e0c112948f78deebb49cfa183ab~tplv-goo7wpa0wc-image.image) </span>

2. Select **Visual Configuration** or **JSON Configuration** to view the detailed configuration of the policy.


<span id="c7f66d9d"></span>
## Edit custom policy

Non\-system predefined policies support editing of policy content.


1. On the policy list page, click the more button in the **Operation** column, then select **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce696ab2f5804241908451320bbe99d6~tplv-goo7wpa0wc-image.image) </span>

2. On the **Edit Policy** page, you can reset the policy name, resources, actions, etc. After editing, click **Save**.


<span id="7aee073f"></span>
## Delete custom policy

Non\-system predefined policies support deletion.


1. On the policy list page, click the more button in the **Operation** column, then select **Remove**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60208aed0f5b4a12b827b7659546484a~tplv-goo7wpa0wc-image.image) </span>

2. In the Confirm Strategy Deletion dialog, click **Confirm**.
