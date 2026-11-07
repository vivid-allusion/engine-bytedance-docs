---
title: "Viewing the scope monitoring chart"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Viewing_the_scope_monitoring_chart"
---

You can use the scope monitoring charts to accurately grasp the operational status of IPAM and make timely adjustments and maintenance to your CIDR configurations accordingly. For monitoring metrics, see **IPAM ** **monitoring metrics**.

## Action description

* If an IAM user is only granted VPC permissions but not CloudMonitor permissions, they will be unable to view the VPC service's monitoring data. Please use the main account (to which the IAM user belongs) to add the system\-predefined CloudMonitor policy permissions to the IAM user according to your actual needs.

   |Policy name |Supported action |
   |---|---|
   |CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
   |CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |

* CloudMonitor collects monitoring metric data for IPAM once per hour.

## Procedures

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select your target Region.

3. In the left navigation tree, select **IPAM Scope**.

4. Click the name of the target scope.

5. Click the **Monitoring chart** tab, then select the tabs as needed to view monitoring chart data.

   * **Scope**: Number of managed CIDRs, number of unmanaged CIDRs, number of ignored CIDRs, number of VPC CIDRs, number of subnet CIDRs, number of compliant CIDRs, number of non\-compliant CIDRs, number of overlapping CIDRs, number of non\-overlapping CIDRs.

   * **Address pool:**  Number of compliant CIDRs, number of non\-compliant CIDRs, IP usage rate allocated to the pool, IP usage rate allocated to resources, occupancy rate of unallocated IPs.

   * **VPC resources:**  Number of IPs in use, number of available IP addresses in the pool, IP usage rate.

   * **Subnet resources:**  Number of IPs in use, number of available IPs, IP usage rate.

## Configuring an alarm strategy

You can see [Creating an alert template](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-template) to create and enable an alert template that meets your requirements, or see [Creating an alert policy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) to modify a preset alert template into a suitable alert policy.
