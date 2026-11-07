---
title: "Managing instance diagnosis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Managing-an-Instance-Diagnostics"
---

This topic introduces operations related to Instance Diagnostics.

## Create instance diagnosis

### Prerequisites

* A network instance (such as an EIP) to be diagnosed already exists.

* When using the Instance Diagnostics service for the first time, please follow the on\-screen instructions to complete the authorization for the required cross\-service associated role.

### Procedures

1. Log in to the [Instance Diagnosis console](https://console.byteplus.com/netadvisor/diagnosis).

2. Click **Create Instance Diagnosis**.

3. Configure relevant parameters based on the table below.

   |Parameters |Notes |Sample value |
   |---|---|---|
   |Diagnosed type |Select a diagnostic type to quickly filter the instances to be diagnosed. Currently EIP, NAT Gateway, Classic Load Balancer (CLB), VPN gateway, TR type IPsec\-VPN connection, Transit Router (TR), Direct Connect (DC), Endpoint and Cloud Enterprise Network (CEN) are supported. |CLB |
   |Region |Select the region where the target instances reside. |China (Beijing) |
   |Select instance |Select the specific instances to be diagnosed. |clb\-1 |

4. Click **Start Diagnosis**. The instance will enter the Diagnosing state. Please wait patiently for the process to complete.

5. After the diagnosis is complete, a diagnostic report will automatically pop up.

   > **tip**

   > The system will save your diagnostic reports for 30 days, giving you sufficient time to address and review network issues.

6. You can troubleshoot issues based on the suggestions provided in the diagnostic report. After addressing the issues, perform a re\-diagnosis to verify the results.

## Re\-diagnose

If you have previously performed a diagnosis and taken corrective actions based on the report, you can re\-diagnose the instance to check if the issues have been resolved.

1. Log in to the [Instance Diagnosis console](https://console.byteplus.com/netadvisor/diagnosis).

2. On the Instance Diagnostics list page, click the Re\-diagnose icon within the target instance diagnostics card. The instance will enter the Diagnosing state. Please wait patiently.

3. View the new diagnostic report. If any items still show a Failed status, address them according to the prompts.

## Delete instance diagnostics

When the diagnostic report shows that all items have passed, you can proceed to delete the instance diagnostics if needed. Instance diagnostics are automatically deleted if the corresponding instance is released.

1. Log in to the [Instance Diagnosis console](https://console.byteplus.com/netadvisor/diagnosis).

2. To manually delete instance diagnostics, on the Instance Diagnostics list page, click the Delete icon within the target instance diagnostics card.

3. Click **Delete** to complete the action.
