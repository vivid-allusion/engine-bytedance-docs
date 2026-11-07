---
title: "FAQs"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/FAQs"
---

* [Can I add a Subscription EIP to a Bandwidth Package?](https://docs.byteplus.com/en/docs/50/12011#.5YyF5bm05YyF5pyI5YWs572RSVDmlK_mjIHliqDlhaXlhbHkuqvluKblrr3ljIXlkJfvvJ8=)

* [Do Subscription Bandwidth Packages support automatic renewal? How do I renew?](https://docs.byteplus.com/en/docs/50/12011#Uf0mKFF6)

* [Why do I need to set maximum bandwidth for Pay-by-main-traffic and Pay-by-95th-peak Bandwidth Packages?](https://docs.byteplus.com/en/docs/50/12011#.5Li65LuA5LmI5oyJ5Li75rWB6YeP6K6h6LS55ZKM5oyJ5Lyg57ufOTXorqHotLnnmoTlhbHkuqvluKblrr3ljIXpnIDopoHorr7nva7luKblrr3kuIrpmZDvvJ8=)

* [Does the conversion to Pay-by-95th-peak take effect immediately?](https://docs.byteplus.com/en/docs/50/12011#.6K6h6LS56L2s5o2i5oiQ5oyJ5Lyg57ufOTXorqHotLnnq4vljbPnlJ_mlYjlkJfvvJ8=)

* [Why does the Bandwidth Package list page display "No permissions" when the IAM user accesses it?](https://docs.byteplus.com/en/docs/50/12011#.5a2Q6LSm5Y-36L-b5YWl5YWx5Lqr5bim5a695YyF5YiX6KGo6aG16Z2i77yM5Li65LuA5LmI5pi-56S65b2T5YmN5a2Q6LSm5Y-35pqC5peg5p2D6ZmQ77yf)

* [Why does the IAM user fail to call DescribeBandwidthPackages, prompting "No permissions"?](https://docs.byteplus.com/en/docs/50/12011#.5a2Q6LSm5Y-36LCD55SoIERlc2NyaWJlQmFuZHdpZHRoUGFja2FnZXMg5o6l5Y-j77yM5o-Q56S65peg5p2D6ZmQ77yf)

* [How do IAM users use tag features?](https://docs.byteplus.com/en/docs/50/12011#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf)

* [Why can't IAM users view monitoring data?](https://docs.byteplus.com/en/docs/bandwidthpackage/FAQs?lang=zh#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf)

* [How do I check the pricing of a Bandwidth Package instance?](https://docs.byteplus.com/en/docs/50/12011#.5aaC5L2V5p-l55yL5YWx5Lqr5bim5a695YyF5a6e5L6L55qE5Lu35qC877yf)

* [Why can’t I view Dual-stack Bandwidth Packages in the list page?](https://docs.byteplus.com/en/docs/50/12011#.5Li65LuA5LmI5Zyo5YWx5Lqr5bim5a695YyF5YiX6KGo6aG15peg5rOV5p-l55yL5Y2P6K6u57G75Z6L5Li65Y-M5qCI55qE5YWx5Lqr5bim5a695YyF77yf)

* [Why doesn't the calculated monthly guaranteed bandwidth match the estimate shown in the console?](https://docs.byteplus.com/en/docs/50/12011#weY7BRAy)

* [How to view estimates of Monthly 95th peak bandwidth and Monthly guaranteed bandwidth?](https://docs.byteplus.com/en/docs/50/12011#wKEWsiYf)

* [Will fees still be incurred if the BytePlus account owning a Bandwidth Package is overdue?](https://docs.byteplus.com/en/docs/50/12011#QzYTQE5d)

* [Do resources in a Bandwidth Package support cost allocation?](https://docs.byteplus.com/en/docs/50/12011#wqX79B2P)


<span id=".5YyF5bm05YyF5pyI5YWs572RSVDmlK_mjIHliqDlhaXlhbHkuqvluKblrr3ljIXlkJfvvJ8="></span>
## Can I add a Subscription EIP to a Bandwidth Package?

Unsupported. You can only add Pay\-as\-you\-go elastic IP addresses (EIPs) to the Bandwidth Package.

<span id="Uf0mKFF6"></span>
## Do Subscription Bandwidth Packages support automatic renewal? How do I renew?

Yes, supported. You can renew through the following two methods:


* Console: Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps), and manually renew a Subscription Bandwidth Package or configure automatic renewal for it. For more information, see [Renewal](https://docs.byteplus.com/en/docs/bandwidthpackage/Renewal).

* OpenAPI: Call the following APIs online via [API Explorer](https://api.byteplus.com/api-explorer?action=RenewInstance&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=billing&version=2022-01-01) for renewal:

   * [RenewInstance](https://docs.byteplus.com/en/docs/6269/1471386): Renew an instance.

   * [SetRenewalType](https://docs.byteplus.com/en/docs/6269/1471385): Set the renewal type for the instance, including automatic renewal, manual renewal, and no renewal upon expiration.


<span id=".5Li65LuA5LmI5oyJ5Li75rWB6YeP6K6h6LS55ZKM5oyJ5Lyg57ufOTXorqHotLnnmoTlhbHkuqvluKblrr3ljIXpnIDopoHorr7nva7luKblrr3kuIrpmZDvvJ8="></span>
## Why do I need to set maximum bandwidth for Pay\-by\-main\-traffic and Pay\-by\-95th\-peak Bandwidth Packages?

Prevent large traffic volume caused by program errors or malicious access, and control costs.

<span id=".6K6h6LS56L2s5o2i5oiQ5oyJ5Lyg57ufOTXorqHotLnnq4vljbPnlJ_mlYjlkJfvvJ8="></span>
## Does the conversion to Pay\-by\-95th\-peak take effect immediately?

Pay\-by\-95th\-peak takes effect at 00:00:00 the next day after conversion. Before the metering method becomes effective, you can neither modify the specification nor delete the Bandwidth Package instance.

<span id=".5a2Q6LSm5Y-36L-b5YWl5YWx5Lqr5bim5a695YyF5YiX6KGo6aG16Z2i77yM5Li65LuA5LmI5pi-56S65b2T5YmN5a2Q6LSm5Y-35pqC5peg5p2D6ZmQ77yf"></span>
## Why does the Bandwidth Package list page display "No permissions" when the IAM user accesses it?

As an Identity and Access Management (IAM) user, the Bandwidth Package list shows resources from all projects by default. Select a specific project to view or contact your root account for access permissions as prompted.

<span id=".5a2Q6LSm5Y-36LCD55SoIERlc2NyaWJlQmFuZHdpZHRoUGFja2FnZXMg5o6l5Y-j77yM5o-Q56S65peg5p2D6ZmQ77yf"></span>
## Why does the IAM user fail to call DescribeBandwidthPackages, prompting "No permissions"?

Two scenarios:


* The IAM user lacks both global and project\-scoped query permissions for Bandwidth Package. Contact your root account for authorization or use an IAM user with proper permissions.

* The IAM user has query permissions for Bandwidth Package only at the project scope (not global). When calling DescribeBandwidthPackages, you must specify either `ProjectName` or `BandwidthPackageIds.N`.


<span id=".5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf"></span>
## How do IAM users use tag features?

<span id=".5q2l6aqk5LiA77ya5Yib5bu65qCH562-562W55Wl"></span>
### Step 1: Create a tag policy


1. Log in to [the IAM console](https://console.byteplus.com/iam/identitymanage/user) with the root account to which the IAM user belongs.

2. In the left\-side navigation pane, select **Permission policy**.

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


1. Log in to [the IAM console](https://console.byteplus.com/iam/identitymanage/user) with the root account to which the IAM user belongs.

2. In the left\-side navigation pane, select **User management \> User**.

3. Click the username of the IAM user to be authorized.

4. In the **Policy \> Directly Add Policy**, click **Authorize** to enter the Add authorization page, and check the new custom policy created in Step 1.

5. Click **Submit** to complete the action.


<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf"></span>
## Why can't IAM users view monitoring data?

If an IAM user has permissions for Bandwidth Package and wants to view monitoring data of a Bandwidth Package, the root account to which the IAM user belongs must also grant the required Cloud Monitor permissions to the IAM user.


1. Log in to [the IAM console](https://console.byteplus.com/iam/identitymanage/user) with the root account to which the IAM user belongs.

2. In the left\-side navigation pane, select **User management \> User**.

3. Click the username of the IAM user to be authorized.

4. Click **Authorize** to add the system Cloud Monitor policy permissions to the IAM user as needed.

   
   |Policy name |Supported action |
   |---|---|
   |CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use its features |
   |CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |
   

5. Click **Submit** to complete the action.


<span id=".5aaC5L2V5p-l55yL5YWx5Lqr5bim5a695YyF5a6e5L6L55qE5Lu35qC877yf"></span>
## How do I check the pricing of a Bandwidth Package instance?

You can view the price of a Bandwidth Package instance on the [Pricing Calculator](https://www.byteplus.com/en/pricing?product=BandwidthPackage&tab=2) page. The amount presented by Pricing Calculator is for reference only. Specific fees are subject to the amount on the actual order in [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

<span id=".5Li65LuA5LmI5Zyo5YWx5Lqr5bim5a695YyF5YiX6KGo6aG15peg5rOV5p-l55yL5Y2P6K6u57G75Z6L5Li65Y-M5qCI55qE5YWx5Lqr5bim5a695YyF77yf"></span>
## Why can’t I view Dual\-stack Bandwidth Packages in the list page?

If you have not enabled IPv6 gateway or created Dual\-stack Bandwidth Packages, you cannot view such Bandwidth Packages on the list page.

<span id="weY7BRAy"></span>
## Why doesn't the calculated monthly guaranteed bandwidth match the estimate shown in the console?

The billing formula for a single Pay\-by\-95th\-peak Bandwidth Package is:

**MAX [(Monthly 95th peak × Effective days of 95th peak / Billing month days), (Monthly guaranteed bandwidth × Effective days of guarantee / Billing month days)] × Monthly bandwidth unit price**

In this formula, the monthly guaranteed bandwidth is calculated by dividing the sum of all daily guaranteed bandwidth by the effective days of guarantee.

The overview tab of Bandwidth Package details page shows the monthly guaranteed bandwidth estimate. If you modify the specification for the Bandwidth Package (e.g., increasing the maximum bandwidth), the daily guaranteed bandwidth may change, resulting in your calculated monthly guaranteed bandwidth mismatching the estimate shown in the console. For more information, see [Billing](https://docs.byteplus.com/en/docs/bandwidthpackage/Pay-by-traditional-95th-percentile).

<span id="wKEWsiYf"></span>
## How to view estimates of Monthly 95th peak bandwidth and Monthly guaranteed bandwidth?

You can follow these steps to view estimates of Monthly 95th peak bandwidth and Monthly guaranteed bandwidth in the console:


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select a target region and project.

3. Click the Name/ID of the target Pay\-by\-95th\-peak Bandwidth Package.

4. In the **Overview** tab of the instance details, view Monthly 95 peak bandwidth estimate and Monthly guaranteed bandwidth estimate of the Bandwidth Package.

   > Neither **Monthly 95th peak bandwidth estimate** nor **Monthly guaranteed bandwidth estimate** represents the actual metered usage applied to billing formula.   
   

<span id="QzYTQE5d"></span>
## Will fees still be incurred if the BytePlus account owning a Bandwidth Package is overdue?

Yes. If the account is overdue but the Bandwidth Package remains operational, usage will continue to be billed. Billing only stops after the Bandwidth Package enters the "Suspended"​ status.

[Recharge](https://docs.byteplus.com/en/docs/6269/100434) your account promptly if you continue using the Bandwidth Package, while [releasing it](https://docs.byteplus.com/en/docs/bandwidthpackage/Releasing-a-Bandwidth-Package) as soon as possible if no longer needed.

<span id="wqX79B2P"></span>
## Do resources in a Bandwidth Package support cost allocation?

Resources in **Pay\-by\-data\-transfer** and **Pay\-by\-95th\-peak** Bandwidth Package support cost allocation. For details, see [Split bills](https://docs.byteplus.com/en/docs/byteplus-platform/SplitBills).
