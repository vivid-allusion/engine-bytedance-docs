---
title: "NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-instacnce-FAQs"
---

## Does the NLB instance have specifications?

The Network Load Balancer (NLB) instance has no specifications, so specifying them is unnecessary. The NLB uses an elastic mechanism, and the system will automatically perform elastic scaling based on the business load situation. The NLB focuses on Layer 4 (Transport Layer) capabilities and is far superior to the CLB in terms of high throughput and low latency in Layer 4 load scenarios. The main differences between NLB and CLB can be found in the [comparison between NLB and CLB](https://docs.byteplus.com/en/docs/clb/Features#4XaCYGhU).

The scaling up process of the NLB instance typically takes a few minutes. During this period, if there is a sudden traffic surge, there may be brief impacts.

## Why are the inbound rules of the security group associated with the NLB instance not taking effect?

It may be because you only added allow policies but did not add deny policies. If the security group associated with the NLB instance does not add any deny policies, the NLB listening port by default allows all requests. If you only want specific IP addresses to access the NLB, be sure to add a deny policy with a lower priority than the allow policy as a safety net. For more information about Identity and Access Management (IAM) for NLB instances, refer to [Instance access control](https://docs.byteplus.com/en/docs/clb/NLB-Instance-Overview#.5a6e5L6L6K6_6Zeu5o6n5Yi2).

## Why can't the NLB forward access requests?

* The health checks of all backend servers associated with the NLB instance are marked as abnormal, and NLB automatically blocks abnormal backend servers, disabling forward access requests. You can refer to [Health check troubleshooting guide](https://docs.byteplus.com/en/docs/clb/NLB-Troubleshooting-exceptions-found-in-health-check) to identify the cause of the abnormalities.

* If all zones forwarding capability of the NLB instance is disabled and no backend servers are added within a given availability zone, the private IP address of the NLB in that availability zone cannot forward access requests. You can enable all zones forwarding for the NLB instance or add backend servers within the availability zone.

* If the subnet where the NLB instance's VIP resides enables the Network Access Control List and does not allow `100.64.0.0/10` or `fd00:64::/32` CIDR blocks, the system detection of the instance VIP fails. The A record for the VIP in that availability zone will be removed from the NLB domain name resolution entry, rendering the VIP in that availability zone unable to forward traffic accessing the NLB domain name.

## Can NLB instance information be exported?

Yes. On the NLB Instances page, click the download icon on the right of the search bar to export NLB instance information as needed.

> **tip**

> The exported file is in .csv format.

## Why can IAM users still apply for new Elastic IP (EIP) addresses by creating internet NLBs after being granted permission to deny applications for EIP addresses?

When enabling the NLB service, you need to manually grant the NLB service permission to request access across services, which includes APIs related to EIP addresses. Therefore, even if an IAM user is granted permission to deny applications for EIP addresses, they can still apply for new EIP addresses by creating internet NLBs.

If you do not want IAM users to apply for new EIP addresses by creating internet NLBs, please create a custom policy and grant it to IAM users. The policy content is as follows:

```JSON
{
  "Statement": [
    {
      "Effect": "Deny",
      "Action": [
        "clb:CreateNetworkLoadBalancer",
        "clb:ModifyNetworkLoadBalancerNetworkType"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringEqualsIfExists": {
          "clb:NlbNetworkType": [
            "internet"
          ]
        }
      }
    }
  ]
}
```

## Why can't IAM users view monitoring data?

If the IAM user is only authorized with permissions for NLB, without authorization for cloud monitor permissions, they cannot view monitoring data for NLB. Please use the primary account to manage users and add permissions to the IAM user as needed.

|Policy Name |Supported Operations |
|---|---|
|CloudMonitorFullAccess |CloudMonitor management permission. When granted this permission, the IAM user can not only view monitoring data, but also use CloudMonitor. |
|CloudMonitorReadOnlyAccess |CloudMonitor access permission. When granted with this permission, the IAM user can only view monitoring data. |
