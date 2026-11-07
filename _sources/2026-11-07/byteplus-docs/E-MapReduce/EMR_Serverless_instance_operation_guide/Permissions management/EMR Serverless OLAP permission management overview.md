---
title: "EMR Serverless OLAP permission management overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_OLAP_permission_management_overview"
---

EMR Serverless instances (OLAP) provide multidimensional permission management capabilities, allowing you to flexibly configure the permission details for different accounts as needed. This article provides a brief introduction to the scope and methods of EMR Serverless OLAP permission management.


|Specific scenarios |Note |Permission management methods |
|---|---|---|
|Authorization for dependent cloud products |Multiple functional modules provided by EMR Serverless instances (OLAP) depend on other cloud products such as VPC and CLB. Therefore, you need to grant the EMR product itself the corresponding permissions to access these dependent cloud products. |When enabling the EMR Serverless product, you can select the service\-linked role to have the system automatically complete the authorization for you.<br><br>After selection, EMR will have the permissions of the preset role ServiceRoleForEMRServerless in access control.<br><br>`ServiceRoleForEMRServerless` permissions. |
|Console permission management |You can use sub\-accounts and permission management policies in access control (IAM) to manage permissions for the EMR Serverless instance (OLAP) console. For example, you can control which sub\-accounts can access the EMR Serverless instance (OLAP) console and whether they have permissions to create or modify configuration parameters. |You can create multiple IAM sub\-accounts according to your business team's structure and separately manage the permission policies for different sub\-accounts to achieve permission management.<br><br>For details, see [Permission control in the management console: Grant permissions to IAM users](https://docs.byteplus.com/docs/E-MapReduce/109098). |
|Component permission management |To further implement fine\-grained control over sub\-account permissions for operating components, you can use the internal user/role permission management capabilities provided by EMR Serverless instances (OLAP). |You can create different users/roles within EMR Serverless instances (OLAP) and set the permission scope for each user/role to manage component permissions.<br><br>For details, see [Component permission management: users and roles](https://docs.byteplus.com/docs/E-MapReduce/109102). |
