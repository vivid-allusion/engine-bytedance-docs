---
title: "Add system policy"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/authorize-iam-users"
---

CR supports authorizing IAM (Identity and Access Management) users to enable multi\-user collaborative management of CR resources. This article mainly describes the steps for authorizing IAM users to use instances.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

This article mainly describes how to quickly authorize IAM users to use CR instances through system preset policies. For custom policy\-related operations, see [add custom policy ](https://docs.byteplus.com/en/docs/cr/add-custom-policies).

A policy is a method of describing the access control capabilities of IAM. IAM supports the following two types of permission policies:


* System\-preset policies: The policies are created by the system in a centralized manner. You can only use but cannot modify them, and the version updates of these policies are maintained by the system.

* User\-defined policies: You can create, update, and delete the policies. The version updates of these policies are maintained by yourself.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have completed the account authentication. For details, see [Account authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [IAM Console ](https://console.byteplus.com/iam/overview/).

2. Create an IAM user and attach the following policies to the user. For the method for creating and authorizing policies, see [Creating a user ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user). For more information about policies and configuration, see [Managing policies ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-policy-management).

   
   |Policy |Description |
   |---|---|
   |CRFullAccess |This policy allows read and write access to CR. Policy details are as follows:<br><br>```JSON```<br>```{```<br>```  "Statement": [```<br>```    {```<br>```      "Effect": "Allow",```<br>```      "Action": [```<br>```        "cr:*",```<br>```        "vpc:Describe*",```<br>```        "artifacts:*",```<br>```        "bill_volcano_engine:CheckPurchasePermission",```<br>```        "bill_volcano_engine:CalculateV2",```<br>```        "bill_volcano_engine:ListConfiguration",```<br>```        "bill_volcano_engine:GetBalanceStatus",```<br>```        "bill_volcano_engine:ListResourcePackage",```<br>```        "storage_ebs:CalculatePrice"```<br>```      ],```<br>```      "Resource": [```<br>```        "*"```<br>```      ]```<br>```    }```<br>```  ]```<br>```}```<br> |
   |CRReadOnlyAccess |This policy allows read\-only access to CR. Policy details are as follows:<br><br>```JSON```<br>```{```<br>```  "Statement": [```<br>```    {```<br>```      "Effect": "Allow",```<br>```      "Action": [```<br>```        "cr:List*",```<br>```        "cr:Get*",```<br>```        "cr:Pull*",```<br>```        "cr:SetUser",```<br>```        "artifacts:Get*",```<br>```        "artifacts:List*",```<br>```        "artifacts:pull",```<br>```        "artifacts:*Credential",```<br>```        "bill_volcano_engine:CheckPurchasePermission",```<br>```        "bill_volcano_engine:CalculateV2",```<br>```        "bill_volcano_engine:ListConfiguration",```<br>```        "bill_volcano_engine:GetBalanceStatus",```<br>```        "bill_volcano_engine:ListResourcePackage",```<br>```        "storage_ebs:CalculatePrice"```<br>```      ],```<br>```      "Resource": [```<br>```        "*"```<br>```      ]```<br>```    }```<br>```  ]```<br>```}```<br> |
   

3. Authorize the **ServiceRoleForCR** role for the user. For the authorization method, see [Managing roles ](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management). Role details are as follows.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After authorization, the role will appear in the IAM  <a href="https://console.byteplus.com/iam/identitymanage/role">role list </a>. Deleting the role will cause cross\-service access to become unavailable. Please proceed with caution.   </div>
   

   
   |Role |Description |
   |---|---|
   |ServiceRoleForCR |CR policy for TOS access.<br><br><br>* Associated policy: ServiceRolePolicyForCR<br><br><br>```JSON```<br>```{```<br>```  "Statement": [```<br>```    {```<br>```      "Effect": "Allow",```<br>```      "Action": [```<br>```        "vpc:DescribeVpcs",```<br>```        "vpc:DescribeSubnets",```<br>```        "vpc:DescribeSecurityGroups",```<br>```        "vpc:CreateNetworkInterface",```<br>```        "vpc:DeleteNetworkInterface",```<br>```        "vpc:DescribeNetworkInterfaces",```<br>```        "vpc:CreateNetworkInterfacePermission",```<br>```        "vpc:DeleteNetworkInterfacePermission",```<br>```        "vpc:DescribeNetworkInterfacePermissions",```<br>```        "vpc:DescribeVpcAttributes",```<br>```        "vpc:DescribeSubnetAttributes",```<br>```        "vpc:DescribeNetworkInterfaceAttributes",```<br>```        "vpc:AttachNetworkInterface",```<br>```        "vpc:DetachNetworkInterface",```<br>```        "vpc:AssociateTrunkInterface",```<br>```        "vpc:DisassociateTrunkInterface",```<br>```        "vpc:DescribeTrunkAssociations",```<br>```        "private_zone:CreatePrivateZone",```<br>```        "private_zone:UpdatePrivateZone",```<br>```        "private_zone:DeletePrivateZone",```<br>```        "private_zone:QueryPrivateZone",```<br>```        "private_zone:ListPrivateZones",```<br>```        "private_zone:CreateRecord",```<br>```        "private_zone:DeleteRecord",```<br>```        "private_zone:ListRecords",```<br>```        "private_zone:UpdateRecord",```<br>```        "private_zone:BatchCreateRecord",```<br>```        "private_zone:BatchDeleteRecord",```<br>```        "dns:ListZones",```<br>```        "dns:ListRecords",```<br>```        "dns:CreateRecord",```<br>```        "dns:DeleteRecord",```<br>```        "dns:UpdateRecord",```<br>```        "certificate_service:CertificateGetInstance",```<br>```        "tls:CreateProject",```<br>```        "tls:ModifyProject",```<br>```        "tls:DescribeProject",```<br>```        "tls:DescribeProjects",```<br>```        "tls:CreateTopic",```<br>```        "tls:ModifyTopic",```<br>```        "tls:DeleteTopic",```<br>```        "tls:DescribeTopics",```<br>```        "tls:DescribeTopic",```<br>```        "tls:CreateIndex",```<br>```        "tls:ModifyIndex",```<br>```        "tls:DescribeIndex",```<br>```        "tls:PutLogs",```<br>```        "tls:CreateDashboard",```<br>```        "tls:ModifyDashboard",```<br>```        "tls:DeleteDashboard",```<br>```        "tls:DescribeDashboard",```<br>```        "tls:DescribeDashboards",```<br>```        "tls:GetAccountStatus",```<br>```        "kms:DescribeKey",```<br>```        "kms:AsymmetricSign"```<br>```      ],```<br>```      "Resource": [```<br>```        "*"```<br>```      ]```<br>```    }```<br>```  ]```<br>```}```<br><br><br><br>* Trust relationship: CR<br><br><br>```JSON```<br>```{```<br>```  "Statement": [```<br>```    {```<br>```      "Effect": "Allow",```<br>```      "Action": [```<br>```        "sts:AssumeRole"```<br>```      ],```<br>```      "Principal": {```<br>```        "Service": [```<br>```          "cr"```<br>```        ]```<br>```      }```<br>```    }```<br>```  ]```<br>```}```<br> |
