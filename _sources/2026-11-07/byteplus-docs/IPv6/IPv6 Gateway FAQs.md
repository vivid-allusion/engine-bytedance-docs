---
title: "IPv6 Gateway FAQs"
product: "IPv6 Gateway"
product_code: "IPv6"
section: "Document"
source: "https://docs.byteplus.com/en/docs/IPv6/FAQs"
---

* [When is it necessary to manually create an IPv6 Gateway?](https://docs.byteplus.com/en/docs/149/32388#.5LuA5LmI5oOF5Ya15LiL6ZyA6KaB5omL5Yqo5Yib5bu6SVB2Nue9keWFs--8nw==)

* [Does the IPv6 Gateway affect IPv6 intranet communication?](https://docs.byteplus.com/en/docs/149/32388#.SVB2Nue9keWFs-aYr-WQpuW9seWTjUlQdjbnp4HnvZHkupLpgJrvvJ8=)

* [Why can't the IPv6-enabled ECS be pinged?](https://docs.byteplus.com/en/docs/149/32388#.5Li65LuA5LmISVB2NueahOS6keacjeWKoeWZqOaXoOazlXBpbmc26YCaSVB2NueahOWFrOe9keWcsOWdgO-8nw==)

* [Why can't IAM users view monitoring data?](https://docs.byteplus.com/en/docs/149/32388#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf)

* [How do IAM users use tag features?](https://docs.byteplus.com/en/docs/149/32388#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf)

* [Why can't I enable IPv6 Internet bandwidth?](https://docs.byteplus.com/en/docs/149/32388#hiercpWy)


<span id=".5LuA5LmI5oOF5Ya15LiL6ZyA6KaB5omL5Yqo5Yib5bu6SVB2Nue9keWFs--8nw=="></span>
## When is it necessary to manually create an IPv6 Gateway?

An IPv6 Gateway is required for communication between a Virtual Private Cloud (VPC) and the IPv6 internet. After the IPv6 is enabled for a VPC, the system automatically creates an IPv6 Gateway associated with that VPC. However, in the following two cases, you need to manually create an IPv6 Gateway:


* VPCs with IPv6 enabled before October 10, 2022.

* VPCs whose IPv6 Gateway has been deleted.


For the procedure, see [Creating an IPv6 Gateway](https://docs.byteplus.com/en/docs/IPv6/Creating_an_IPv6_gateway_instance) and [Enabling IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth).

<span id=".SVB2Nue9keWFs-aYr-WQpuW9seWTjUlQdjbnp4HnvZHkupLpgJrvvJ8="></span>
## Does the IPv6 Gateway affect IPv6 intranet communication?

The IPv6 Gateway only manages IPv6 internet traffic for the VPC and does not affect the intranet.

<span id=".5Li65LuA5LmISVB2NueahOS6keacjeWKoeWZqOaXoOazlXBpbmc26YCaSVB2NueahOWFrOe9keWcsOWdgO-8nw=="></span>
## Why can't the IPv6\-enabled ECS be pinged?

Possible causes are as follows:


|Cause |Description |
|---|---|
|ECS image does not recognize the IPv6 address |Some ECS images cannot automatically recognize IPv6 addresses. See [Configuring a private IPv6 address for ECS](https://docs.byteplus.com/en/docs/vpc/Configuring-private-IPv6-addresses-for-ECS-instances) to confirm if configuration is needed. If needed, the IPv6 address becomes valid only after you complete the configuration. |
|IPv6 Internet bandwidth is not enabled |An IPv6 address without IPv6 Internet bandwidth enabled only supports IPv6 intranet communication. You need to use an IPv6 Gateway to [enable IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth) for the IPv6 address. |
|Security group does not allow |The security group of the primary network interface where the ECS is located must allow outbound IPv6 traffic. If it is not allowed, see [Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules). |
|Network ACL does not allow |If the subnet of ECS is configured with Network Access Control List (ACL), you need to allow IPv6 traffic in the Network ACL. If it is not allowed, see [Add network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules#.5re75Yqg572R57ucQUNM6KeE5YiZ). |
|Route does not exist |The route table associated with the subnet of the IPv6 address must contain a route entry with the Destination CIDR Block setting as ::/0 and the Next Hop setting as IPv6 Gateway. If no such route entry, see [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry). |


<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf"></span>
## Why can't IAM users view monitoring data?

If an Identity and Access Management (IAM) user has permissions for an IPv6 Gateway and wants to view its monitoring data, the root account to which the IAM user belongs must also grant the required Cloud Monitor permissions to the IAM user.


1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) using the root account that owns the IAM user.

2. In the left navigation pane, select **User management \> User** to open the User page.

3. Click the username of the IAM user to be authorized to enter the User detail page.

4. Click **Authorize** to add the system Cloud Monitor policy permissions to the IAM user as needed.

   
   |Policy name |Supported action |
   |---|---|
   |CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
   |CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |
   

5. Click **Submit** to complete the action.


<span id=".5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf"></span>
## How do IAM users use tag features?

<span id=".5q2l6aqk5LiA77ya5Yib5bu65qCH562-562W55Wl"></span>
### Step 1: Create a tag policy


1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) using the root account that owns the IAM user.

2. In the left navigation pane, select **Permission policy**.

3. Click **Create Policy**, type the name and content for the policy. The reference content is as follows:

   ```Plain Text
   {        
                           "Statement":[        
                                           {        
                                                           "Effect":"Allow",        
                                                           "Action":[        
                                                                           "vpc:TagResources",
                                                                           "vpc:UntagResources",
                                                                           "vpc:ListTagsForResources"
                                                           ],        
                                                           "Resource":[        
                                                                           "*"
                                                           ]
                                           }
                           ]
           }
   ```
   

4. Click **Submit** to complete the action.


<span id=".5q2l6aqk5LqM77ya5Li65a2Q55So5oi35re75Yqg5qCH562-562W55Wl"></span>
### Step 2: Add the tag policy to the IAM user.


1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) using the root account that owns the IAM user.

2. In the left\-side navigation pane, select **User management \> User** to access the User page.

3. Click the username of the IAM user to be authorized.

4. In the **Policy \> Directly Add Policy**, click **Authorize** to access the Add authorization page, and check the new custom policy.

5. Click **Submit ** to complete the action.


<span id="hiercpWy"></span>
## Why can't I enable IPv6 Internet bandwidth?

You need to associate your cloud resources with the VPC or subnet with an enabled IPv6 Gateway before enabling IPv6 Internet bandwidth. After associating, you can [enable IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth).
