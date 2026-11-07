---
title: "Step 1: Enterprise organization admin configures the enterprise organization"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Step-1-configures-the-enterprise-organization"
---

## Scenarios

Enterprise organization admins can authorize the IPAM delegated admin to plan and manage the organization's IP addresses by enabling trusted services.

## Procedures

### Step 1: Enable trusted service

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the left\-side navigation pane, select **Trusted service management**.

3. Click **Enable trusted service**.

4. Click **Enable** to complete the action.

   After the IPAM service is enabled, the system automatically creates the role [ServiceRoleForVPC](https://console.byteplus.com/iam/identitymanage/role/ServiceRoleForVPC) under all member accounts within the enterprise organization. This role is used by Resource Discovery to obtain VPC resources from those member accounts.

### Step 2: Specify IPAM delegated admin

1. Log in to the [Enterprise Organization console](https://console.byteplus.com/organization/department/).

2. In the left navigation tree, select **Enterprise organization \> Trusted service**.

3. Click **Manage** to the right side of **IPAM**.

4. Click **Add proxy account**, then select the target member account as the IPAM delegated admin.

5. Click **Submit** to complete the action.

### Step 3: Create control policy (optional)

1. Log in to the [Enterprise Organization console](https://console.byteplus.com/organization/department/).

2. In the left navigation tree, select **Control Policy.**

3. Click **Enable control policy**.

4. Click **Add policy** and enter the policy name. For example, Enforce\-IPAM\-VPC\-Creation.

5. On the **JSON Editor** tab, enter the policy content to enforce that business accounts select the IPAM address pool when creating VPCs.

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

### Step 4: Attach control policy (optional)

1. Log in to the [Enterprise Organization console](https://console.byteplus.com/organization/department/).

2. In the left navigation tree, select **Control Policy.**

3. On the **Policy binding** tab, click the name of the business account on the left.

4. Click **Add binding policy** and select the target control policy.

5. Click **Submit** to complete the action.
