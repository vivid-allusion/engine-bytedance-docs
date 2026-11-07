---
title: "Best practices on IAM authorization"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Best-practices-on-IAM-authorization"
---

This topic introduces the best practices for granting permissions to IAM users for FaaS.

## Prerequisites

IAM users have been created.  For detailed instructions, see [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

## Scenario 1: Use global preset policies and grant permissions

### Scenario introduction

veFaaS provides the following system preset policies that can be directly used to grant permissions to IAM users

|Policy |Description |
|---|---|
|VeFaaSFullAccess |Full management permissions for veFaaS. |
|VeFaaSReadOnlyAccess |Read\-only permissions for veFaaS. |

### Procedure

1. Log in to the [IAM console](https://console.byteplus.com/iam) using a BytePlus account or an IAM account with the required permissions.

2. In the left navigation pane, select **User management** \> **User**.

3. In the user list, find the username that requires permissions. Click **Manage** in the **Actions** column.

4. On the **User details** page, select **Permissions** \> **Global permissions** tab, and click **Add permission**.

5. In the search box of the **Add permission** panel, enter **veFaaS** to search for system preset policies.

6. Select a policy as needed. Click **Confirm** to add the veFaaS permission policy to the IAM user.

## Scenario 2: Create and grant custom permissions effective within a project

### Scenario introduction

Some Actions and Resources in veFaaS are organized by projects, which enables project\-level permission control. IAM users need to obtain the permissions for such Actions and Resources via project authorization.

> **tip**

> The Actions included in project authorization are:

* > CreateFunction

* > UpdateFunction

### Procedure

1. Log in to the [IAM console](https://console.byteplus.com/iam) using a BytePlus account or an IAM account with the required permissions.

2. Create a custom policy.

   1. In the left navigation pane, select **Policy management**. On the Policy management page, click **Create custom policy**.

   2. On the create custom policy page, enter the policy name and policy content, then click **Submit**.

      Assume the policy name is `vefaas-create-project`, and the JSON content is as follows. You can add or remove specific Actions or Resources as needed.

      ```bash
      {
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "vefaas:CreateFunction",
                      "vefaas:UpdateFunction"
                  ],
                  "Resource": [
                      "*"
                  ]
              }
          ]
      }
      ```

3. Add project authorization to the created `vefaas-create-project` policy.

   1. Click the policy name `vefaas-create-project` to go to the policy details page.

   2. On the **Authorization \> Project authorization** tab, click **Add authorization.**

   3. Select the user to authorize and the related project.

   4. Click **Confirm** to complete project authorization.

4. Create a custom policy for Actions and Resources that cannot be organized by projects, and apply it to the target IAM user to grant a global permission.

   > **tip**

   > Some Actions and Resources in veFaaS cannot be organized by projects. Therefore, you need to make them accessible to the target IAM user by offering a global permission, in addition to implementing project authorization for that user. Otherwise, the IAM user may not access the veFaaS resources.

   1. Create a custom policy.

      Assume the name is `vefaas-read-global`. The JSON content of the policy is shown below. Please add or remove specific Actions or Resources as needed.

      ```bash
      {
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "vefaas:Release",
                      "vefaas:GetCodeUploadAddress",
                      "vefaas:CodeUploadCallback",
                      "vefaas:TestInvoke",
                      "vefaas:DeleteFunction",
                      "vefaas:AbortRelease",
                      "vefaas:UpdateRelease",
                      "vefaas:GetAvailabilityZones",
                      "vefaas:GetFunction",
                      "vefaas:GetFunctionInstanceLogs",
                      "vefaas:GetReleaseStatus",
                      "vefaas:GetRevision",
                      "vefaas:GetStorageVolumeStatus",
                      "vefaas:ListFunctionInstances",
                      "vefaas:ListReleaseRecords",
                      "vefaas:ListRuntimes",
                      "vefaas:ListFunctions",
                      "vefaas:ListRevisions",
                      "vefaas:ListTemplates",
                      "vefaas:DoesFunctionNameExist",
                      "vefaas:GetDependencyInstallTaskStatus"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "apig:GetGateway",
                      "apig:ListGateways",
                      "apig:ListGatewayServices",
                      "apig:GetGatewayService",
                      "apig:DeleteGatewayService",
                      "apig:CreateUpstream",
                      "apig:CheckUpstreamSpecExist",
                      "apig:GetUpstream",
                      "apig:DeleteUpstream",
                      "apig:CreateRoute",
                      "apig:UpdateRoute",
                      "apig:ListRoutes",
                      "apig:DeleteRoute"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "vpc:DescribeVpcs",
                      "vpc:DescribeVpcAttributes",
                      "vpc:DescribeSubnets",
                      "vpc:DescribeSubnetAttributes",
                      "vpc:DescribeSecurityGroups",
                      "vpc:DescribeSecurityGroupAttributes"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "tls:DescribeProject",
                      "tls:DescribeProjects",
                      "tls:DescribeTopic",
                      "tls:DescribeTopics",
                      "tls:DescribeIndex",
                      "tls:DescribeIndexConfig",
                      "tls:DescribeHistogram",
                      "tls:SearchLogs",
                      "tls:Statistics"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "cr:ListRegistries",
                      "cr:ListRepositories",
                      "cr:ListNamespaces",
                      "cr:ListTags"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "kafka:DescribeKafkaInstances",
                      "kafka:DescribeInstanceDetail",
                      "kafka:DescribeTopics",
                      "kafka:DescribeUsers"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "rocketmq:ListInstances",
                      "rocketmq:ListTopics",
                      "rocketmq:ListGroups",
                      "rocketmq:GetInstance"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "tos:PutBucketNotification",
                      "tos:ListBuckets",
                      "tos:ListBucket",
                      "tos:HeadBucket",
                      "tos:GetObject"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "apmplus_server:GetMetricsData",
                      "apmplus_server:Draw"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "bill_volcano_engine:ListResourcePackage"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "FileNAS:DescribeFileSystems"
                  ],
                  "Resource": [
                      "*"
                  ]
              }
          ]
      }
      ```

   2. Add global authorization to the created `vefaas-read-global` policy.

      On the `vefaas-read-global` policy details page, select the **Authorization \> Global authorization** tab, and click **Add authorization.**  Select the user to authorize, and click **Confirm** to complete global authorization.

### Validating results

When an IAM user attempts to create a function in a non\-default project, a permission denied message is displayed.

## Scenario 3: Create and grant tag\-based custom permissions

### Scenario introduction

Some Actions and Resources in veFaaS are attached with tags, enabling permission control by tag.

> **tip**

> Actions attached with tags are:

* > CreateFunction

* > UpdateFunction

### Procedure

1. Log in to the [IAM console](https://console.byteplus.com/iam) using a BytePlus account or an IAM account with the required permissions.

2. Create a custom policy.

   1. In the left navigation pane, select **Policy management**. On the Policy management page, click **Create custom policy**.

   2. On the create custom policy page, enter the policy name and policy content, then click **Submit**.

      Assume the name is `vefaas-function-operation-by-tag`, indicating that CreateFunction and UpdateFunction are only accepted by the tag `team:ai-prompt`, and denied by other tags.

      ```bash
      {
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "vefaas:CreateFunction",
                      "vefaas:UpdateFunction"
                  ],
                  "Resource": [
                      "*"
                  ],
                  "Condition": {
                      "StringEquals": {
                          "volc:RequestTag/team": [
                              "ai-prompt"
                          ]
                      }
                  }
              }
          ]
      }
      ```

3. Add global authorization to the created `vefaas-function-operation-by-tag` policy.

   1. Click the policy name `vefaas-function-operation-by-tag` to go to the policy details page.

   2. On the **Authorization \> Global authorization** tab, click **Add authorization.**

   3. Select the user to authorize.

   4. Click **Confirm** to complete project authorization.

4. Create a custom policy for Actions and Resources that cannot be authorized by tag, and apply it to the target IAM user to grant a global permission.

   > **tip**

   > Some Actions and Resources in veFaaS cannot be authorized by tags. Therefore, you need to make them accessible to the target IAM user by offering a global permission, in addition to implementing tag\-based authorization for that user. Otherwise, the IAM user may not access the veFaaS resources.

   1. Create a custom policy.

      Assume the name is `vefaas-other-generate-operation`. The JSON content of the policy is shown below. Please add or remove specific Actions or Resources as needed.

      ```bash
      {
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "vefaas:Release",
                      "vefaas:TestInvoke",
                      "vefaas:DeleteFunction",
                      "vefaas:AbortRelease",
                      "vefaas:UpdateRelease",
                      "vefaas:GetAvailabilityZones",
                      "vefaas:GetFunctionInstanceLogs",
                      "vefaas:GetReleaseStatus",
                      "vefaas:GetRevision",
                      "vefaas:GetStorageVolumeStatus",
                      "vefaas:ListFunctionInstances",
                      "vefaas:ListReleaseRecords",
                      "vefaas:ListRuntimes",
                      "vefaas:ListRevisions",
                      "vefaas:ListTemplates",
                      "vefaas:DoesFunctionNameExist",
                      "vefaas:GetTemplateDetail",
                      "vefaas:ListFunctions",
                      "vefaas:GetDependencyInstallTaskStatus"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "apig:GetGateway",
                      "apig:ListGateways",
                      "apig:ListGatewayServices",
                      "apig:GetGatewayService",
                      "apig:DeleteGatewayService",
                      "apig:CreateUpstream",
                      "apig:CheckUpstreamSpecExist",
                      "apig:GetUpstream",
                      "apig:DeleteUpstream",
                      "apig:CreateRoute",
                      "apig:UpdateRoute",
                      "apig:ListRoutes",
                      "apig:DeleteRoute"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "vpc:DescribeVpcs",
                      "vpc:DescribeVpcAttributes",
                      "vpc:DescribeSubnets",
                      "vpc:DescribeSubnetAttributes",
                      "vpc:DescribeSecurityGroups",
                      "vpc:DescribeSecurityGroupAttributes"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "tls:DescribeProject",
                      "tls:DescribeProjects",
                      "tls:DescribeTopic",
                      "tls:DescribeTopics",
                      "tls:DescribeIndex",
                      "tls:DescribeIndexConfig",
                      "tls:DescribeHistogram",
                      "tls:SearchLogs",
                      "tls:Statistics"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "cr:ListRegistries",
                      "cr:ListRepositories",
                      "cr:ListNamespaces",
                      "cr:ListTags"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "kafka:DescribeKafkaInstances",
                      "kafka:DescribeInstanceDetail",
                      "kafka:DescribeTopics",
                      "kafka:DescribeUsers"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "rocketmq:ListInstances",
                      "rocketmq:ListTopics",
                      "rocketmq:ListGroups",
                      "rocketmq:GetInstance"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "tos:PutBucketNotification",
                      "tos:ListBuckets",
                      "tos:ListBucket",
                      "tos:HeadBucket",
                      "tos:GetObject"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "apmplus_server:GetMetricsData",
                      "apmplus_server:Draw"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "bill_volcano_engine:ListResourcePackage"
                  ],
                  "Resource": [
                      "*"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "FileNAS:DescribeFileSystems"
                  ],
                  "Resource": [
                      "*"
                  ]
              }
          ]
      }
      ```

   2. Add global authorization to the created `vefaas-other-generate-operation` policy.

      On the `vefaas-other-generate-operation` details page, select the **Authorization \> Global authorization** tab, and click **Add authorization.**  Select the user to authorize, and click **Confirm** to complete global authorization.

### Validating results

* The IAM user successfully creates a function tagged as `team:ai-prompt` or a function containing this tag.

* If the IAM user creates a function with no tags or with a tag rather than `team:ai-prompt`, a message indicating insufficient permissions is displayed.
