---
title: "FAQs about CEN instances"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/CEN-instances-faq"
---

* [k?](https://docs.byteplus.com/en/docs/44/16681#.5Lik5Y-w5LqR5pyN5Yqh5Zmo5aaC5L2V6YCa6L-H5LqR5LyB5Lia572R5a6e546w5YaF572R5LqS6YCa77yf)[k?](https://docs.byteplus.com/en/docs/44/16681#.5Lik5Y-w5LqR5pyN5Yqh5Zmo5aaC5L2V6YCa6L-H5LqR5LyB5Lia572R5a6e546w5YaF572R5LqS6YCa77yf)

* [Does CEN support network communication between instances that belong to different accounts?](https://docs.byteplus.com/en/docs/44/16681#.5LqR5LyB5Lia572R5pSv5oyB6Leo6LSm5Y-3572R57uc5a6e5L6L5LqS6YCa5ZCX77yf)

* [How do I test the data transfer rate of a CEN instance?](https://docs.byteplus.com/en/docs/44/16681#.5aaC5L2V5rWL6K-V5LqR5LyB5Lia572R55qE6YCf546H77yf)

* [What is rate limiting of CEN?](https://docs.byteplus.com/en/docs/44/16681#.5LuA5LmI5piv5LqR5LyB5Lia572R6ZmQ6YCf77yf)

* [If I want to establish network communication between network instances that belong to different accounts, do I have to create a CEN instance in each of the accounts?](https://docs.byteplus.com/en/docs/44/16681#.6Leo6LSm5Y-35LqS6YCa5Zy65pmv5LiL77yM6ZyA6KaB5Zyo5Lik5Liq6LSm5Y-35LiL5Z2H5Yib5bu65LqR5LyB5Lia572R5a6e5L6L5ZCX77yf)

* [Do I have to buy an EIP if my ECS instances use CEN to communicate with each other?](https://docs.byteplus.com/en/docs/44/16681#.6YCa6L-H5LqR5LyB5Lia572R5LqS6K6_55qE5LqR5pyN5Yqh5Zmo5a6e5L6L6L-Y6ZyA6KaB6LSt5Lmw5YWs572RSVDlkJfvvJ8=)

* [Does CEN use physical lines, and are the lines logically isolated?](https://docs.byteplus.com/en/docs/44/16681#.5LqR5LyB5Lia572R55qE57q_6Lev5piv54mp55CG57q_6Lev6L-Y5piv6YC76L6R6ZqU56a777yf)

* [Can I attach a VPC to multiple CEN instances?](https://docs.byteplus.com/en/docs/44/16681#.5LiA5LiqVlBD5piv5ZCm5Y-v5Lul5Yqg6L295Yiw5Lik5Liq5Y-K5Lul5LiK55qE5LqR5LyB5Lia572R5a6e5L6L77yf)

* [Why does an IAM user fail to call some API actions?](https://docs.byteplus.com/en/docs/44/16681#.5Li65LuA5LmI5a2Q6LSm5Y-35peg5rOV5q2j5bi46LCD55So6YOo5YiG5o6l5Y-j77yf)


<span id=".5Lik5Y-w5LqR5pyN5Yqh5Zmo5aaC5L2V6YCa6L-H5LqR5LyB5Lia572R5a6e546w5YaF572R5LqS6YCa77yf"></span>
## How do I use CEN to enable two ECS instances to communicate with each other over the internal network?

CEN instances within the same VPC can communicate without CEN. To enable communication between instances in different VPCs, you can attach the VPCs to the same CEN instance. For more information, see the following topics: For more information, see the following topics:


* [Establishing network communication among VPCs in the same Region](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-within-the-same-account-and-Region-01)

* [Establishing network communication among VPCs in different Regions](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01)


<span id=".5LqR5LyB5Lia572R5pSv5oyB6Leo6LSm5Y-3572R57uc5a6e5L6L5LqS6YCa5ZCX77yf"></span>
## Does CEN support network communication between instances that belong to different accounts?

Yes, CEN supports network communication between instances that belong to different accounts. However, you must grant CEN permissions on VPCs in the peer account first. For more information, refer to the following topics:


* VPC: See [Adding cross-account authorization](https://docs.byteplus.com/en/docs/vpc/Managing-CEN-cross-account-authorization).

* Direct Connect: See [CEN cross-account authorization](https://docs.byteplus.com/en/docs/directconnect/Cross-account-authorization).


<span id=".5aaC5L2V5rWL6K-V5LqR5LyB5Lia572R55qE6YCf546H77yf"></span>
## How do I test the data transfer rate of a CEN instance?

You can test the data transfer rate of a CEN instance by using the network performance utility iperf.

<span id=".5LuA5LmI5piv5LqR5LyB5Lia572R6ZmQ6YCf77yf"></span>
## What is rate limiting of CEN?

The data transfer rate of inter\-region connections on a CEN instance is determined by the inter\-region bandwidth. Within the valid range of bandwidth that you allocate to inter\-region connections, network traffic is not throttled by CEN. The peak inbound or outbound bandwidth can reach the maximum bandwidth that you allocate to the inter\-region connections.

<span id=".6Leo6LSm5Y-35LqS6YCa5Zy65pmv5LiL77yM6ZyA6KaB5Zyo5Lik5Liq6LSm5Y-35LiL5Z2H5Yib5bu65LqR5LyB5Lia572R5a6e5L6L5ZCX77yf"></span>
## If I want to establish network communication between network instances that belong to different accounts, do I have to create a CEN instance in each of the accounts?

No. In scenarios where accounts communicate with each other, a CEN instance in one account can mount network instances from both the local account and authorized accounts.

<span id=".6YCa6L-H5LqR5LyB5Lia572R5LqS6K6_55qE5LqR5pyN5Yqh5Zmo5a6e5L6L6L-Y6ZyA6KaB6LSt5Lmw5YWs572RSVDlkJfvvJ8="></span>
## Do I have to buy an EIP if my ECS instances use CEN to communicate with each other?

You do not have to buy an EIP if the ECS instances communicate with each other only over the internal network of BytePlus.

If you want to use an EIP to manage an ECS instance or allow the ECS instance to communicate with the internet, you must buy an EIP.

<span id=".5LqR5LyB5Lia572R55qE57q_6Lev5piv54mp55CG57q_6Lev6L-Y5piv6YC76L6R6ZqU56a777yf"></span>
## Does CEN use physical lines, and are the lines logically isolated?

The lines of CEN are deployed on the backbone network of BytePlus. The lines are logically isolated from each other.

<span id=".5LiA5LiqVlBD5piv5ZCm5Y-v5Lul5Yqg6L295Yiw5Lik5Liq5Y-K5Lul5LiK55qE5LqR5LyB5Lia572R5a6e5L6L77yf"></span>
## Can I attach a VPC to multiple CEN instances?

No.

<span id=".5Li65LuA5LmI5a2Q6LSm5Y-35peg5rOV5q2j5bi46LCD55So6YOo5YiG5o6l5Y-j77yf"></span>
## Why does an IAM user fail to call some API actions?

This is because the IAM user you are using is a non\-global IAM user and does not have the appropriate policy permissions configured. To successfully call all CEN interfaces, please configure policy permissions according to the following steps:

> **An IAM user that does not have global permissions** refers to an IAM user that does not have full permissions on CEN.



1. Log in to the root user account of the IAM user and access the [IAM console](https://console.byteplus.com/iam/identitymanage/user).

2. In the **IAM** console left\-side navigation pane, click **Policy Management**.

3. Click **Custom policy**, then click the **New custom policy** button. The following code block displays how to create a custom IAM policy that grants an IAM user full permissions on the GrantInstanceToCen, RevokeInstanceFromCen, DescribeInstanceGrantedRules, TagResources, UntagResources, and ListTagsForResource API actions.

   ```Plain Text
   {
     "Statement":[
       {
         "Effect":"Allow",
         "Action":[
           "cen:GrantInstanceToCen",
           "cen:RevokeInstanceFromCen",
           "cen:DescribeInstanceGrantedRules",
           "cen:TagResources",
           "cen:UntagResources",
           "cen:ListTagsForResources"
         ],
         "Resource":[
           "*"
         ]
       }
     ]
   }
   
   ```
   

4. In the left\-side navigation pane, click **User**.

5. Click the username of the IAM user to be authorized.

6. Under the **Permission** tab's **Global Policy** section, click **Add Permission**.

7. Attach the custom IAM policy to the IAM user.
