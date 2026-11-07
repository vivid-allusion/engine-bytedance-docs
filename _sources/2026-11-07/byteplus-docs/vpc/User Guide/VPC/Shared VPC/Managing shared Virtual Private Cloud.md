---
title: "Managing shared Virtual Private Cloud"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-shared-VPC"
---

<span id=".5byA5ZCv5YWx5LqrVlBD"></span>
## Enable shared VPC

Enable the Shared VPC feature to share subnets with other accounts.

<span id=".5YeG5aSH5bel5L2c"></span>
### Preparations

The resource owner and the shared user accounts of the shared VPC belong to the same   Enterprise organization.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Resource Sharing console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned).

2. In the left\-side navigation pane, select **Resource Sharing \> Shared by me**.

3. In the top menu bar, select Region.

4. In the Shared Unit tab, click **Create shared unit**.

5. Configure relevant parameters based on the table below.

   
   |Parameter name |Notes |Example |
   |---|---|---|
   |Shared unit name |Enter the name of shared unit. |Shared VPC\-A |
   |Region |Select the region where the shared VPC resides. |China (Beijing) |
   |Product |Select **vpc \- subnet**. |Virtual Private Cloud \- Subnet |
   |Resource ID |Select the IDs of subnets to share. |subnet\-12ben6rc67nr417q7y2\*\*\*\* |
   |Shared policy name |Defaults to and only supports RSDefaultPermissionForSubnet. |RSDefaultPermissionForSubnet |
   |Resource user |Select only allow sharing with the same organization within the enterprise. |Only allow sharing with the same organization within the enterprise |
   |Add via enterprise organization |Enable Add via enterprise organization and select the master account. |Enable, 210000\*\*\* |
   

6. Click **Next**, confirm everything is correct, then click **Confirm** to complete the actions.


<span id=".5pu05paw5YWx5LqrVlBD"></span>
## Update Shared VPC

Update shared subnets or modify the list of shared accounts.


1. Log in to the [Resource Sharing console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned).

2. In the left\-side navigation pane, select **Resource Sharing \> Shared by me**.

3. In the top menu bar, select Region.

4. Click **View details** on the right side of the shared unit where the target shared VPC resides.

5. Click **Edit shared unit** in the upper\-right corner, add or reduce shared subnets as needed, and click **Next**.

6. Add or remove shared accounts as needed.

7. Click **Confirm** to complete the action.


<span id=".5YGc5q2i5YWx5LqrVlBD"></span>
## Stop sharing VPC

Disable the Shared VPC feature to stop sharing subnets with other accounts.

<span id=".5pON5L2c6K-05piO"></span>
### Instructions

After sharing is stopped, the sharing records will be retained in the console for 2 days. Users can view the sharing records.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Resource Sharing console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned).

2. In the left\-side navigation pane, select **Resource Sharing \> Shared by me**.

3. In the top menu bar, select Region.

4. Click **View details** on the right side of the shared unit where the target shared VPC resides.

5. Click **Delete shared unit** in the upper\-right corner.

6. Click **OK** to complete the action.
