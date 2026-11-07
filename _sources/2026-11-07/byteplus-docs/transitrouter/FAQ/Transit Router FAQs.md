---
title: "Transit Router FAQs"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instance-faq"
---

<span id="s6KQ8bsj"></span>
## What's the difference between Transit Router (TR) and Cloud Enterprise Network (CEN)?

TR and CEN differ in application scenarios, network instances, and routing configurations. For details, see [Comparison between TR and CEN](https://docs.byteplus.com/docs/transitrouter/Product-Overview-01).

<span id=".5Lit6L2s6Lev55Sx5Zmo5pSv5oyB6L-e5o6l5ZOq5Lqb57G75Z6L55qE572R57uc5a6e5L6L77yf"></span>
## What types of network instances can I attach to TR?

Supported network instance types for TR attachments:


* Virtual Private Cloud (VPC)

* VPN Connect (IPsec\-VPN connection)

* Direct Connect Gateway

* Transit Router


<span id=".5Lit6L2s6Lev55Sx5Zmo5aaC5L2V5pS26LS577yf"></span>
## How is TR billed?

Billing items for TR vary depending on the interconnection scenario, as detailed in the table below.


|Interconnection scenario |Billable resources |Billing items |
|---|---|---|
|Intra\-region |Network instance attachment |* Connection fee<br><br>* Traffic processing fee |
|Inter\-region |Network instance attachment |* Connection fee<br><br>* Traffic processing fee |
||Bandwidth package |Bandwidth fee |


For detailed billing rules, see [TR Billing notes](https://docs.byteplus.com/en/docs/transitrouter/Billing-rules).

<span id=".5L2_55So5Lit6L2s6Lev55Sx5Zmo6L-e5o6l5LiN5ZCM55qEVlBD77yM6YWN572u5a6M5oiQ5ZCO5LiN5ZCMVlBD5YaF55qE5LqR5pyN5Yqh5Zmo5LmL6Ze05rWB6YeP5LiN6YCa5piv5LuA5LmI5Y6f5Zug77yf"></span>
## After connecting VPCs via TR, why can't the Elastic Compute Service (ECS) instances in those VPCs communicate?

If VPCs connected via TR cannot communicate with each other, check for the following possible causes in order:


* Verify that your ECS instance type supports TR.

   The following ECS instance types do not support TR: General\-purpose g1, Compute\-optimized c1, Memory\-optimized r1, Local SSD i1, Big Data Storage d1s, GPU Accelerated g1t, and GPU Accelerated g1tl.

* Verify that your routing configuration is correct.

   * Ensure that the VPC route table contains a route entry with the destination CIDR block of the target VPC and the next hop set to the TR.

   * Ensure that the TR route table contains a route entry with the destination CIDR block of the target VPC and the next hop set to the network instance attachment.


<span id=".5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf"></span>
## Why can't IAM users view monitoring data?

If an Identity and Access Management (IAM) user has permissions for TR but not for Cloud Monitor, the user cannot view TR monitoring data. To view monitoring data, the root account must grant the system\-defined Cloud Monitor policy to this IAM user as needed. For procedure, see [Managing users](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management).


|Policy name |Supported action |
|---|---|
|CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
|CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |


<span id=".5Li65LuA5LmI5L2_55SoaXBlcmblkb3ku6TmtYvlh7rnmoTluKblrr3ov5zlsI_kuo7ot6jlnLDln5_ov57mjqXliIbphY3nmoTluKblrr3vvJ8="></span>
## Why is the bandwidth measured using the `iperf` command much lower than the bandwidth allocated for the inter\-region attachment?

This is because you are testing single\-threaded traffic, which cannot reach the maximum bandwidth for the inter\-region attachment. We recommend using multi\-threaded concurrent traffic for testing. Example of a multi\-threaded traffic test command:

```Plain Text
iperf -c 192.168.1.10 -p 80 -u -b 100m -P 10
```


Parameter explanations:


* `-c`: Starts iperf in client mode. 192.168.1.10 is the IP address of the server.

* `-p`: Specifies the port. 80 is the port number.

* `-u`: Uses a UDP connection.

* `-b`: Sets the bandwidth per thread. Total bandwidth = Bandwidth per thread × Number of threads. 100m is the bandwidth size, which is typically set to the allocated bandwidth.

* `-P`: Specifies the number of threads.


If the bandwidth tested by multi\-threaded concurrent traffic is still much lower than the bandwidth allocated for the inter\-region attachment, please contact your account manager.

<span id="c0458758"></span>
## Can I change the bandwidth package for an inter\-region attachment?

Yes. For procedure, see [Modifying bandwidth for an inter-region attachment](https://docs.byteplus.com/docs/transitrouter/Inter-region-peering-attachments-03).

<span id="Q6k0J8eY"></span>
## **If the** ** BytePlus** ** account associated with the TR is in arrears, will charges still be incurred?** 

Yes. If the account linked to the Transit Router is in arrears but the Transit Router continues to operate normally, billing will still apply. Charges will only stop after the Transit Router enters the suspended status.

If you still need to use this Transit Router, [recharge](https://docs.byteplus.com/en/docs/6269/100434?lang=en) your account promptly. If you no longer need it, we recommend [deleting the TR](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-04) as soon as possible.
