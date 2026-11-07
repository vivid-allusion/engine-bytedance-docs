---
title: "ECS custom policy examples"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Custom_policy_example_for_ECS"
---

If the system default policies provided by the platform cannot meet your needs, you can create custom policies based on the principle of least privilege. This enables fine\-grained permission control and enhances secure access by IAM identities to resources under the root account. This topic shows examples of common custom policies related to ECS instances as a reference.

### Allow access to resources under specified projects

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:DescribeInstances"
            ],
            "Resource": [
                "trn:ecs:*:210005****:instance/*",
                "trn:iam::210005****:project/default"
            ]
        }
    ]
}
```

This policy allows viewing instances belonging to the "default" project under Account 210005\*\*\*\*. When you grant authorizations by project, you need to select a project scope in addition to the existing authorization policy, thereby restricting permissions to the specified project.

### Deny ECS instance deletion

> **tip**

> Deny takes precedence over Allow. If an identity has Deny permissions for certain actions, the Allow permissions for those same actions will not take effect. To resolve this, remove the relevant Deny statements or modify them to Allow.

#### Deny all instance deletion

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "ecs:DeleteInstance",
                "ecs:DeleteInstances"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

#### Deny ECS resource deletion for instances with IDs i\-yczzpbpgqoqc6ilc\*\*\*\* and i\-yczv4tg64gqc6iks\*\*\*\* under account 200000000X

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "ecs:Delete*"
            ],
            "Resource": [
                "trn:ecs:*:200000000X:instance/i-yczzpbpgqoqc6ilc****,i-yczv4tg64gqc6iks****"
            ]
        }
    ]
}
```

### Allow ECS instance creation

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:RunInstances"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

### Deny ECS instance information change

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "ecs:ModifyInstanceAttribute"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

### Restrict ECS instance access

#### Allow actions on the ECS instance with the ID i\-yczzpbpgqoqc6ilc\*\*\*\* under account 200000000X

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:*"
            ],
            "Resource": [
                                "trn:ecs:*:200000000X:instance/i-yczzpbpgqoqc6ilc****"
      ]
        }
    ]
}
```

#### Allow ECS resource viewing

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:Describe*"
            ],
            "Resource": [
                                "*"
      ]
        }
    ]
}
```

### Access ECS from a specific IP address

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:*"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "IpAddress": {
                    "volc:SourceIp": [
                        "210.22.XX.XX"
                    ]
                }
            }
        }
    ]
}
```

### Only ECS resources with the tag key "ecs" and a condition value of "use" can be accessed

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:*"
            ],
            "Resource": [
                "*"
            ],
            "Condition": {
                "StringEquals": {
                    "volc:ResourceTag/ecs": [
                        "use"
                    ]
                }
            }
        }
    ]
}
```

### Allow access to tag feature

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:CreateTags",
                "ecs:DeleteTags",
                "ecs:DescribeTags"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

### Deny key pair deletion

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "ecs:DeleteKeyPairs"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```

### Only allow O&M orchestration tasks to apply for, query, and associate Elastic IPs (EIPs)

```json

{
  "Statement":[
    {
      "Effect":"Allow",
      "Action":[
        "vpc:AllocateEipAddress",
        "vpc:DescribeEipAddresses",
        "vpc:AssociateEipAddress"
      ],
      "Resource":["*"]
    }
  ]
}
```

### Restrict the use of target custom commands to the specified IAM users

```json
{
 "Statement": [
   {
       "Effect": "Allow",
       "Action": [
           "ecs:Describe*",
           "ecs:ModifyCommand",
           "ecs:InvokeCommand"
       ],
       "Resource": [
           "trn:ecs:cn-beijing:210001*****:command/cmd-ycn5dc9qf9l8j0v*****",
           "trn:ecs:cn-beijing:210001*****:command/cmd-tsx0gy9rslp90k3z*****"
       ]
   }
 ]
}
```

##
