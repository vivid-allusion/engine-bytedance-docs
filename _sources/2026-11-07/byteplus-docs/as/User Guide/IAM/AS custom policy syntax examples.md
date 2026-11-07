---
title: "AS custom policy syntax examples"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/AS_custom_policy_syntax_example"
---

If the system default policies provided by BytePlus cannot meet your needs, you can create custom policies based on the principle of least privilege. This enables fine\-grained permission control and enhances secure access by IAM identities to resources under the root account. This topic provides common custom policy examples related to Auto Scaling in daily scenarios for your reference.

<span id=".6Ieq5a6a5LmJ562W55Wl5a6e5L6L"></span>
## Custom policy examples

<span id=".56S65L6L5LiA77ya5ouS57ud5Yig6Zmk5omA5pyJ5Ly457yp57uE"></span>
### Example 1: Deny deletion of all scaling groups

```json
{
    "Statement": [
        {
            "Effect": "Deny",
            "Action": [
                "auto_scaling:DeleteScalingGroup"
            ],
            "Resource": [
                    "*"
      ]
        }
    ]
}
```


<span id=".56S65L6L5LqM77ya5YWB6K645Yib5bu6VlBD6LWE5rqQ"></span>
### Example 2: Allow creation of VPC resources

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vpc:*Vpc*",
                "vpc:*Subnet*",
                "vpc:*NetworkInterface*",
                "vpc:*Route*",
                "vpc:*SecurityGroup*",
                "vpc:*HaVip*",
                "vpc:*NetworkAcl*",
                "vpc:*PrivateIpAddresses",
                "vpc:*Ipv6Addresses"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```


<span id=".56S65L6L5LiJ77ya5YWB6K645p-l6K-i5LqR5pyN5Yqh5Zmo5a6e5L6L55u45YWz6LWE5rqQ"></span>
### Example 3: Allow querying resources related to ECS instances

```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:Describe*",
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```
