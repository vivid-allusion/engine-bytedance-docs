---
title: "Access policy templates"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/access-policy-templates"
---

Before an IAM user can use Message Queue for Kafka, the BytePlus account must grant the IAM user relevant access permissions. Message Queue for Kafka supports custom permission policies. This topic offers examples of custom access policies for various common scenarios.

<span id="b9959b3f"></span>
## Read\-only permission on a specified instance

With the following permission policy, IAM users can view basic information, such as configurations and endpoints of the specified instance, topic lists and partition details, group lists and their consumption status, and query messages through the console or open APIs.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kafka:Get*",
                "kafka:List*",
                "kafka:Describe*",
                "kafka:Query*"
            ],
            "Resource": [
                "trn:Kafka:cn-beijing:210004****:instance/kafka-cnoetpgh3bid****"
            ]
        }
    ]
}
```


<span id="83822fa8"></span>
## Management permission on a specified instance

With the following permission policy, IAM users can view and manage all information about the specified instance through the console or open APIs, including upgrading instance specifications, enabling or disabling internet\-facing access, and managing other resources in the instance like topics, groups, and Simple Authentication and Security Layer (SASL) users.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "*"
            ],
            "Resource": [
                "trn:Kafka:cn-beijing:210004****:instance/kafka-cnoetpgh3bid****"
            ]
        }
    ]
}
```


<span id="bc83a80a"></span>
## Group management permission on all instances

With the following permission policy, IAM users can perform actions such as creating groups, viewing the group list, and resetting consumer offsets, through the console or open APIs.

```Bash
{ 
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kafka:CreateGroup",
                "kafka:ModifyGroup",
                "kafka:DeleteGroup",
                "kafka:DescribeGroups",
                "kafka:DescribeConsumedTopics",
                "kafka:DescribeConsumedPartitions",
                "kafka:ResetConsumedOffsets"
            ],
            "Resource": [
                "trn:Kafka:cn-beijing:210004****:instance/*"
            ]
        }
    ]
}
```


<span id="e8e704b3"></span>
## SASL user management permission on all instances

With the following permission policy, IAM users can create SASL users, grant permissions to SASL users, reset passwords, view passwords, or delete users through the console or open APIs.

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kafka:CreateUser",
                "kafka:DeleteUser",
                "kafka:ModifyUserAuthority",
                "kafka:DescribeUsers",
                "kafka:DescribeInstances",
                "kafka:DescribeInstanceDetail",
                "kafka:DescribeTopics",
                "kafka:DescribeAvailabilityZones",
                "kafka:ModifyTopicAccessPolicies",
                "kafka:ModifyUserPassword",
                "kafka:DescribeUserPassword"
            ],
            "Resource": [
                "trn:Kafka:cn-beijing:210004****:instance/*"
            ]
        }
    ]
}
```
