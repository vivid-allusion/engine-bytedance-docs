---
title: "Configuring a control policy"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-a-control-policy"
---

## Scenarios

Enterprise Organization supports control policies. IPAM instance owners can use control policies to enforce that business accounts create VPCs and allocate secondary CIDR blocks from a specified IPAM address pool.

## Create control policy

1. Use an enterprise organization admin account to log in to the [Enterprise Organization console](https://console.byteplus.com/organization/department/).

2. In the left navigation tree, select **Control Policy.**

3. Click **Enable control policy**.

4. Click **Add policy** and enter the policy name. For example, Enforce\-IPAM\-VPC\-Creation.

5. On the **JSON Editor** tab, enter the policy content to mandate that business accounts must select the IPAM address pool when creating VPCs and allocating secondary CIDR blocks.

   ```JSON
   {
     "Version": "1",
     "Statement": [
       {
         "Effect": "Deny",
         "Action": [
           "vpc:CreateVpc",
           "vpc:AssociateVpcCidrBlock"
         ],
         "Resource": ["trn:vpc:*:*:vpc/*"],
         "Condition": {
           "Null": {
             "vpc:Ipv4IpamPoolId": "true"
           }
         }
       }
     ]
   }
   ```

6. Click **Submit** to complete the action.

## Attach control policy

1. Use an enterprise organization admin account to log in to the [Enterprise Organization console](https://console.byteplus.com/organization/department/).

2. In the left navigation tree, select **Control Policy.**

3. On the **Policy binding** tab, click the name of the business account on the left.

4. Then click **Add binding policy** and select the target control policy.

5. Click **Submit** to complete the action.

## Policy example: Restrict VPC creation to a specific address pool

Business accounts can only allocate CIDRs from the designated IPAM address pool, ensuring that each business line uses its own planned address space.

```JSON
{
  "Version": "1",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "vpc:CreateVpc",
        "vpc:AssociateVpcCidrBlock"
      ],
      "Resource": [
        "trn:vpc:*:*:vpc/*"
      ],
      "Condition": {
        "StringNotEquals": {
          "vpc:Ipv4IpamPoolId": "ipam-pool-xxxxxxxxx"
        }
      }
    },
    {
      "Effect": "Deny",
      "Action": [
        "vpc:CreateVpc",
        "vpc:AssociateVpcCidrBlock"
      ],
      "Resource": [
        "trn:vpc:*:*:vpc/*"
      ],
      "Condition": {
        "Null": {
          "vpc:Ipv4IpamPoolId": "true"
        }
      }
    }
  ]
}
```
