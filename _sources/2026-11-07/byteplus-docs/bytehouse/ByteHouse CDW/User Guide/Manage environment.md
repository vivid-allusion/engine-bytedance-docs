---
title: "Manage environment"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/manage-environment"
---

Starting from version 2.12, ByteHouse supports users setting multiple environments according to their needs, where the computation, storage, databases, networks, auditing, and permissions are completely isolated in different environments, satisfying requirements for multiple instances and access to multiple VPCs. This article introduces the environmental management capabilities provided by ByteHouse and the ideas and practices of managing multiple environments.

<span id="90470afa"></span>
# Introduction to multi\-environment management

ByteHouse Cloud Data Warehouse is a SaaS\-based cloud data warehouse service. Customers open a ByteHouse service with one account. After the service is activated, customers buy different computation groups within ByteHouse to satisfy the query and writing needs of multiple businesses.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the CDW service is activated, a default environment is automatically assigned. This environment allows all sub\-account entrants during initialization, and ByteHouse uses this default environment by default for all resources.</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d93888e8917f45dca2ef23b9ae474d6e~tplv-goo7wpa0wc-image.image" width="2792px" /></div>


In real\-world business scenarios, users desire that resources between different businesses and environments (development and production) be independently isolated; "multi\-environment management" supports isolating completely independent operating environments under one tenant for different businesses, each environment having its own computing resources, storage resources, etc., operating independently, as shown in the figure below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf31ff5f0aaa4d68bc3e5756d534d35e~tplv-goo7wpa0wc-image.image) </span>

In this scenario:


* The main account is usually the ByteHouse cloud data warehouse administrator. After activating the ByteHouse service, the user enters the ByteHouse console, at which point the system automatically assigns a default environment:

   * This Default is the default environment, where any sub\-account with any ByteHouse IAM policy can access.

   * If a sub\-account only has ByteHouseReadOnly IAM permission, it can enter the Default environment but has no resource or data permission. The main account can then grant the necessary permissions to the sub\-account based on the RBAC strategy, and only then can the sub\-account access the required data.

* The main account can create a new environment, named, for example, Business_A:

   * Initially, sub\-accounts have no permission to enter this environment unless the main account grants entry permission.


<span id="9c37cc82"></span>
# Application Scenarios

In the actual business scenarios of cloud data warehouses, users often face the complex demands of multiple businesses and environments coexisting. In general, typical application scenarios for multiple environments include the following aspects:


|**Business Scenarios** |**Scene Requirements** |Scene **Example** |
|---|---|---|
|**Isolation of Development and Production** |Completely isolate development, testing, and production environments to prevent testing activities from affecting production operations. |The development environment is used for new feature development and testing, while the production environment manages real\-time queries and analysis. Performance issues or errors in the development environment will not interfere with the production environment. |
|**Isolation of Multiple Business Scenarios** |Provide independent environments for different business lines (such as finance, marketing, and operations) to avoid resource competition and data security issues. |The finance department runs monthly report analyses, and the marketing department monitors advertising effects in real\-time. Each uses independent computing resources and storage spaces without interfering with each other. |
|**Sensitive Data Protection** |Provide isolated environments for data of different sensitivity levels to ensure data security and access control. |The production environment stores customer privacy data, and the test environment develops new query logic using anonymized data to ensure that private data is not leaked to non\-production environments. |
|**Fault Isolation** |Provide independence between environments to ensure that abnormalities in one environment do not affect the operation of other environments. |The test environment experienced a performance decline due to erroneous queries, but business analysis in the production environment remains stable. |


<span id="f2b0a9b0"></span>
# Caution


|Segmentation |Advisory |
|---|---|
|Permission Requirements |* The AccountAdmin role has permissions to create, authorize, and delete environments.<br><br>* The AccountAdmin and SystemAdmin roles have permission to authorize environments.<br><br>* Other sub\-users must be granted "Environment" permissions before accessing the authorized environments. |
|Default Environment |The default environment is the system default and is not supported for direct deletion. |


<span id="be5fb75d"></span>
# Create New Environment

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The AccountAdmin role has permissions to create, authorize, and delete environments.</div>



1. In the upper right corner of the ByteHouse console, click **the drop\-down box for environment selection**, then click the "**Environment Management**" button to enter the environment management control page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec648964436a48498d8f327522a55159~tplv-goo7wpa0wc-image.image) </span>

2. Click the "**New Environment**" button at the top right, fill in the name of the new environment on the popup page, and you can also remark on the description of this environment; then click **OK** to complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06e95fcc04fd45079d19ab557ef0da9d~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Once created, the environment name cannot be changed subsequently. Please configure the environment name carefully.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The environment name must meet the following requirements:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only supports lowercase letters.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Up to 10 characters.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The environment name cannnot duplicate existing environment names.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The naming rules for the environment display name are as follows:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Up to 100 characters.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The display name cannot be the same as the existing environment name/display name.   </div>
   

3. If the "Created successful" message is displayed, then the operation is complete, and the name of the newly created environment can be seen in the environment list.


<span id="201c3116"></span>
# User assignment

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The AccountAdmin and SystemAdmin roles have permission to authorize environments.</div>


* <div data-tips="true" data-tips-type="warning">Other sub\-users must be granted "Environment" permission before they can access the authorized environment.</div>


1. On the environment management page, you can click the **User Assignment** button behind the corresponding environment to authorize the environment to a sub\-account.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbc02c540da14f98aa320cbb50d53a1e~tplv-goo7wpa0wc-image.image) </span>

2. Select to activate or terminate environment permissions for users in the user list. For different roles, the specific permissions obtained are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cde0dc70432486aa4d33bc46bfa96c6~tplv-goo7wpa0wc-image.image) </span>

   * AccountAdmin: Acquires all permissions (management permissions, user authorization permissions, usage permissions).

   * System Admin: Acquire user authorization permissions and usage rights.

   * Other users: Activate to have usage rights.


<span id="9f4943e4"></span>
# Modify environment display name and remark


1. Click the **Edit** button on the right side of the Environment list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b184f089dc4f42009e6b480386e0da7d~tplv-goo7wpa0wc-image.image) </span>

2. After modifying the environment description, click the **OK** button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67923003b5b2453db4db70b50cef411d~tplv-goo7wpa0wc-image.image) </span>


<span id="597f94e9"></span>
# Delete environment

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Deleting an environment is irreversible, please proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">The Default environment does not support deletion.</div>


1. Before deleting the environment, please empty the resources. It is not supported to delete an environment when resources are not emptied.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651be532095e4c2199669b48c8d135de~tplv-goo7wpa0wc-image.image) </span>

   You can hover your mouse over the grayed\-out **Delete** button in the operation column. In the pop\-up prompt, click the "**Go to Clean Up**" button, and you will be redirected to the tenant management page to view all the resources within the environment.

2. After the resources in the environment are emptied, you can click the corresponding **Delete** button on the right side of the environment list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16500ae2d4874dcd918af4029ba95442~tplv-goo7wpa0wc-image.image) </span>

3. After the deleting operation, it is necessary to wait for a while to clean up the resources in that environment.
