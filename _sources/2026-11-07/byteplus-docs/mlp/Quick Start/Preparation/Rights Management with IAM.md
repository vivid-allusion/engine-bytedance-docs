---
title: "Rights Management with IAM"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Rights_Management_with_IAM"
---

> IAM (Identity and Access Management, IAM) is a set of rights management system provided by BytePlus for customers to control the access rights of different identities to cloud resources.


If you use this product in a scenario where multiple people work together as a team to avoid business losses caused by high\-risk operations, it is recommended to split and isolate permissions. You can create sub accounts according to team roles by main account (see [Common concepts](https://docs.byteplus.com/docs/mlp/76491)) and assign them appropriate permissions. Ordinary developers use sub accounts with limited privileges to log in to the platform for development. The platform presets several common strategies to facilitate the main account to quickly create sub accounts and assign permissions.

The main steps are as follows:


1. Log in with main account and Create sub account.

2. Create sub accounts for administrators or developers with administrative responsibilities and grant administrator privileges to fully manage all the features and permissions of the platform.

3. Log in to the main account Create a sub account for each algorithm engineer in the team and give the appropriate permissions.


<span id="创建子账号"></span>
# Create sub account


1. Log in to the [BytePlus console ](https://console.byteplus.com/home)with the main account.

2. Click [Identity and Access Management] in the account name drop\-down box in the upper right corner to enter the corresponding page.

3. Click [User] \- [New User] in the left navigation bar to enter the basic information settings page.

4. Click Create by user name and fill in the name of the sub account.

5. If you need to access the console, turn on the switch of **console login** and set the access password.

6. **It is recommended to** turn on the switch of **automatic key generation** to directly generate the AK/SK of the sub account, so that the corresponding sub account can use BytePlus products such as Torch Object Storage and Machine Learning Platform through the API or command line through the AK/SK.


<span id="赋予第一个子账号机器学习平台的管理员权限"></span>
# Give administrator sub account permissions

Use the main account on the [Identity and Access Management ](https://console.byteplus.com/iam/identitymanage/user)console to give the administrator sub account Add permissions, making it easier for sub account users to manage the platform's capabilities. The following are common policies related to the use of the Machine Learning Platform, which can be selected according to the actual use of the business. The specific meaning of each policy can be queried in the [Identity and Access Management Rights Policy ](https://console.byteplus.com/iam/policymanage).


|permission name |Required/Optional |Applicable scenario description |
|---|---|---|
|MLPlatformAdminAccess |Required |Machine Learning Platform full\-featured management, including core operations such as Project Create, Resource Scheduling, and Task Monitoring. |
|IAMFullAccess |Required |Identity and Access Management Full\-featured management, used to Create sub accounts, assign permission policies, manage user groups and other permission configuration operations. |
|TOSFullAccess |Required |Torch Object Storage full\-featured management, used to store training data, model files, log files and other massive data storage. |
|BillingCenterFullAccess |optional |Expense center management, support bill inquiry, expense analysis, contract management, invoice application and other financial related operations. |
|AccessKeyFullAccess |optional |Create, delete, view and other management operations of all AccessKeys under the main account need to be configured if there is a need for BytePlus OpenAPI calls. |
|VPCFullAccess |optional |Full\-featured configuration of private network, including VPC Create, subnet partition, routing table management, NAT gateway and other network architectures. |
|APIGFullAccess |optional |Create API interface, configure public domain name, traffic monitoring and other network services.<br><br>> If you need to ensure the public network access experience, you need to use the exclusive public network and not use the platform sharing network. |
|CRFullAccess |optional |Container Registry full\-featured management, support mirror/model artifacts upload, download, version management and other operations. |
|TLSFullAccess |optional |Torch Log Service full\-featured management, support collection, storage, query, analysis of resource operation logs and monitoring indicators. |
|VMPFullAccess |optional |Managed Service for Prometheus service full\-featured management, support monitoring indicator collection, alarm rule configuration, etc. |
|CFSFullAccess |optional |Cloud File System full\-featured management, support Create file system, permission configuration, data read and write operations. |
|vePFSFullAccess |optional |File Storage full\-featured management, supports high\-performance file system Create, capacity management, protocol configuration, and more. |


> If there is more than one administrator, you can repeat the above operation to add permissions for each administrator, or create a [user group ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-group)with administrator permissions, grant the above permissions, and realize group management and authorization.


<span id="（可选）为每个算法工程师创建子账号并配置权限"></span>
# Create sub accounts and permissions for algorithm engineers

The administrator sub account is authorized successfully, and the main account or the administrator sub account can create the sub account according to the algorithm engineer in the team, and give the corresponding sub account permissions on the [Identity and Access Management ](https://console.byteplus.com/iam/identitymanage/user)console.

MLPlatformDeveloperAccess: Machine Learning Platform (veMLP) algorithm developer rights. The child users granted to this policy will have read and write permissions for Dev boxes, custom tasks, inference services, and deployments (only those created by themselves); they will also grant interface permissions such as Get and List for mirror, experiment management, and other modules.


> * If algorithm engineers or administrators in your organization need different permissions in different groups or teams, you can use the [User Groups] function of the [Identity and Access Management] product to assign permissions by group, refer to the [user group](https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management).
