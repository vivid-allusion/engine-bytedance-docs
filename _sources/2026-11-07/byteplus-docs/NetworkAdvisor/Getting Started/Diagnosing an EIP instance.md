---
title: "Diagnosing an EIP instance"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Diagnosing-an-EIP-instance"
---

This topic uses an EIP as an example to describe how to use the Network Advisor (NA) to diagnose the operational status of an EIP instance.

## Application scenarios

Company A has an Elastic Compute Service (ECS) instance bound to an EIP. They perform regular diagnostics on this EIP to check its status and monitor bandwidth usage, ensuring their business operates normally.

## Preparations

* Create an ECS instance associated with an EIP. For related operations, see [Purchasing an instance via wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* When using the Instance Diagnostics service for the first time: Navigate to the Instance Diagnostics console, click **Create Instance Diagnostics**. In the pop\-up window, click **Authorize**. On the cross\-service access request page that appears, click **Authorize Now** to complete the authorization.

## Procedures

1. Log in to the [Instance Diagnostics console](https://console.byteplus.com/netadvisor/diagnosis).

2. Click **Create Instance Diagnostics**.

3. configure relevant parameters based on the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Diagnosed type |Select a diagnostic type to quickly filter the instances to be diagnosed. |Elastic IP Address |
   |Regions |Select the region where the target instances reside. |China (Beijing） |
   |Select instance |Select the specific instances to be diagnosed. |eip\-1 |

4. Click **Start Diagnosis**. The instance will enter the Diagnosing state. Please wait patiently for the process to complete.

5. After the diagnosis is complete, a diagnostic report will automatically pop up.

6. In the example of this article, all diagnostic items in the report show a Passed status. If any items in your report show a Failed status, you can address the issues based on the provided prompts.
