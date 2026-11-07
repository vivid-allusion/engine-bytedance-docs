---
title: "IAM FAQs"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Identity-and-Access-Management-FAQ"
---

* [What permissions must an IAM user have to create an NAT Gateway?](https://docs.byteplus.com/en/docs/51/10039#.5a2Q55So5oi35Yib5bu6TkFU572R5YWz5pe277yM6ZyA6KaB5ZOq5Lqb5p2D6ZmQ77yf)

* [Are the security groups, network interfaces, SNAT entries, and DNAT entries of the NAT Gateway consistent with the project to which the NAT Gateway belongs?](https://docs.byteplus.com/en/docs/51/10039#.TkFU572R5YWz55qE5a6J5YWo57uE44CB572R5Y2h44CBU05BVOinhOWImeOAgUROQVTop4TliJnmmK_lkKblkoxOQVTnvZHlhbPmiYDlsZ7nmoTpobnnm67kuIDoh7TvvJ8=)

* [Why does the IAM user receive a no permission notice when calling the DescribeNatGateways interface?](https://docs.byteplus.com/en/docs/51/10039#.5a2Q55So5oi36LCD55SoIERlc2NyaWJlTmF0R2F0ZXdheXMg5o6l5Y-j77yM5o-Q56S65peg5p2D6ZmQ77yf)

* [Why does the IAM user receive a no permission notice when calling the DescribeSnatEntries interface?](https://docs.byteplus.com/en/docs/51/10039#.5a2Q55So5oi36LCD55SoIERlc2NyaWJlU25hdEVudHJpZXMg5o6l5Y-j77yM5o-Q56S65peg5p2D6ZmQ77yf)

* [Why does the NAT Gateway list page show that the current IAM user has no permission?](https://docs.byteplus.com/en/docs/51/10039#.6L-b5YWlTkFU572R5YWz5YiX6KGo6aG16Z2i77yM5Li65LuA5LmI5pi-56S65b2T5YmN5a2Q55So5oi35peg5p2D6ZmQ77yf)

* [Why can't I select a VPC when creating an NAT Gateway?](https://docs.byteplus.com/en/docs/51/10039#.5Yib5bu6TkFU572R5YWz5pe277yM5peg5rOV6YCJ5oup56eB5pyJ572R57uc77yf)

* [Why do I get a "No permission" error when confirming the NAT Gateway order?](https://docs.byteplus.com/en/docs/51/10039#.5Yib5bu6TkFU572R5YWz5pe277yM5o-Q5Lqk56Gu6K6k6K6i5Y2V77yM5o-Q56S65peg5p2D6ZmQ77yf)

* [Why can't IAM users view monitoring data?](https://docs.byteplus.com/en/docs/51/10039#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf)

* [How do IAM users use tag features?](https://docs.byteplus.com/en/docs/51/10039#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf)


<span id=".5a2Q55So5oi35Yib5bu6TkFU572R5YWz5pe277yM6ZyA6KaB5ZOq5Lqb5p2D6ZmQ77yf"></span>
## What permissions does an IAM user need to create an NAT Gateway?

To successfully create an NAT Gateway as an Identity and Access Management (IAM) user, one of the following conditions must be met.


* Case 1: The IAM user has permission to create an NAT Gateway with a global scope.

* Case 2: The IAM user has the following three permissions.

   * The IAM user has permission to create an NAT Gateway in the project that owns the Virtual Private Cloud.

   * The IAM user has permission to create an NAT Gateway in the project that owns the subnet.

   * The IAM user has permission to create an NAT Gateway in the project where the NAT Gateway to be created belongs.


Example: An IAM user without global permission to create an NAT Gateway needs to create an NAT Gateway, where the VPC belongs to project A, the subnet belongs to project B, and the NAT Gateway to be created belongs to project C.

The IAM user has permission to create an NAT Gateway in project A, project B, and project C.

<span id=".TkFU572R5YWz55qE5a6J5YWo57uE44CB572R5Y2h44CBU05BVOinhOWImeOAgUROQVTop4TliJnmmK_lkKblkoxOQVTnvZHlhbPmiYDlsZ7nmoTpobnnm67kuIDoh7TvvJ8="></span>
## Are the security group, network interface, SNAT entries, and DNAT entries of the NAT Gateway consistent with the project the NAT Gateway belongs to?

Consistency is maintained by default. When the NAT Gateway is moved into or out of a project, its sub\-resources (SNAT entries, DNAT entries, secondary network interfaces, and security groups) move accordingly.


* SNAT entries and DNAT entries do not support manually modifying the associated project.

* Modifying the associated project for NAT Gateway’s network interfaces and security groups is supported but not recommended.


<span id=".5a2Q55So5oi36LCD55SoIERlc2NyaWJlTmF0R2F0ZXdheXMg5o6l5Y-j77yM5o-Q56S65peg5p2D6ZmQ77yf"></span>
## Why does the IAM user get a no permission error when calling the DescribeNatGateways interface?

Two scenarios:


* The IAM user lacks both global and project\-scoped query permissions for NAT Gateways. Contact the root account for authorization or use an IAM user with proper permissions.

* The IAM user lacks global query permission but has project\-scoped query permission for NAT Gateways. When calling DescribeNatGateways, you must pass the `ProjectName` or `NatGatewayIds.N` parameter.


<span id=".5a2Q55So5oi36LCD55SoIERlc2NyaWJlU25hdEVudHJpZXMg5o6l5Y-j77yM5o-Q56S65peg5p2D6ZmQ77yf"></span>
## Why does the IAM user get a no permission error when calling the DescribeSnatEntries interface?

Two scenarios:


* The IAM user lacks both global and project\-scoped query permissions for SNAT entries. Contact the root account for authorization or use an IAM user with proper permissions.

* The IAM user lacks global query permission but has project\-scoped query permission for SNAT entries. When calling DescribeSnatEntries, you must pass the `NatGatewayId` or `SnatEntryIds.N` parameter.


<span id=".6L-b5YWlTkFU572R5YWz5YiX6KGo6aG16Z2i77yM5Li65LuA5LmI5pi-56S65b2T5YmN5a2Q55So5oi35peg5p2D6ZmQ77yf"></span>
## Why does the NAT Gateway list page show that the current IAM user has no permission?

After entering the NAT Gateway list, the system filters all projects by default. Switch projects according to the prompt or contact the root account to authorize.

<span id=".5Yib5bu6TkFU572R5YWz5pe277yM5peg5rOV6YCJ5oup56eB5pyJ572R57uc77yf"></span>
## Why can't I select a VPC when creating an NAT Gateway?

The details are as follows:


* No Virtual Private Cloud (VPC) instance has been created in the current environment.

* When the IAM user creates an NAT Gateway, there is no Virtual Private Cloud instance created in the projects where the IAM user has permission to create NAT Gateways.


<span id=".5Yib5bu6TkFU572R5YWz5pe277yM5o-Q5Lqk56Gu6K6k6K6i5Y2V77yM5o-Q56S65peg5p2D6ZmQ77yf"></span>
## Why do I get a "No permission" error when confirming the NAT Gateway order?

The IAM user lacks the Create NAT Gateway permission in the project to which the subnet selected when creating the NAT Gateway belongs.

<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf"></span>
## Why can't IAM users view monitoring data?

The IAM user does not have the necessary CloudMonitor permissions. After an IAM user is granted NAT Gateway permissions, to view monitoring data, the root account to which the IAM user belongs must also authorize the IAM user with CloudMonitor related permissions.


1. Use the root account to which the IAM user belongs logs in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user).

2. In the left\-side navigation pane, select **User Management \> User** to enter the user page.

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


1. Use the root account to which the IAM user belongs logs in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user).

2. In the left\-side navigation pane, select **Permission policy** to enter the policy management page.

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


1. Use the root account to which the IAM user belongs logs in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user).

2. In the left\-side navigation pane, select **User Management \> User** to enter the user page.

3. Click the username of the IAM user to be authorized to enter the user detail page.

4. Click **Authorize** and check the newly created policy in Step 1.

5. Click **Submit** to complete the action.
