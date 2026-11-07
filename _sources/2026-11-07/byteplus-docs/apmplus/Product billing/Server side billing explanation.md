---
title: "Server side billing explanation"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Server_side_billing_instructions"
---

## Postpaid Billing Method

The APMPlus server\-side monitoring service adopts a postpaid billing model based on reported data volume, determined by the actual volume of:

### Billing Items & Pricing

* Traces/Tracks store 30 days (TracesTracks data will be deleted after 30 days)

* Metrics store 30 days (Metrics data will be deleted after 30 days)

|Billing Item |Free quota |Unit Price |
|---|---|---|
|Metrics 30days |100 million data points per month |$0.052 per million data points |
|Traces/Tracks 30days |25GB per month |$0.087 per GB data ingestion volume |

### Billing Rules

1. Billing Cycle: Daily

   * Bills are generated based on the previous day’s reported data volume.

2. Payment Deduction:

   * If your account balance is sufficient, the system will automatically deduct the billed amount.

## Arrears

If your account does not have sufficient balance to pay for a bill, your resources will enter the service suspension state due to arrears. This topic describes the service suspension state due to arrears and relevant instructions.

### Arrears cause

APMPlus server\-side monitoring performs settlement every day and the expense is deducted in real time after a bill is generated. If the available quota of your account (including the account balance and cash coupons) is less than that in the settlement bill, you will enter the arrears state and receive an email notification for insufficient balance.

### Arrears notification

After your account enters into arrears, the system sends an arrears notification through email, SMS, or internal message. Process the issue and recharge your account after receiving the notification.

### Service suspension due to arrears

If your account is in arrears for **24 hours**, your resources will enter the **service suspension due to arrears** state, and resource usage will be limited. After the resource retention period is due, your resources will be reclaimed forcibly. Reclaimed resources cannot be recovered. To ensure normal use of the APMPlus server\-side monitoring service, recharge your account and settle your overdue payments within the specified period (before forced resource reclaim).

After overdue payments are settled, the instance in the service suspension state due to arrears is started automatically and enters the **running** state.

> **tip**

* > You have to pay for the billed fees regardless of whether your instance resources are frozen or released.

* > The following figure shows the billing and arrears states of APMPlus server\-side monitoring.

![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_87a2fa3c9ca76a2349b2808ab4aed315.png)

### Reclamation due to arrears

When your account remains in the arrears state for 15 days and 24 hours (168 hours), your resources will enter the **reclaimed due to arrears** state, and relevant instances and the data stored on them will be deleted.

> **danger**

> If you do not recharge your account after it is in arrears for 168 hours, the system will forcibly release instances and delete all the data of these instances. The deleted data cannot be recovered.

## Project bill splitting

APMPlus server\-side monitoring supports using projects to manage workspace resources and perform bill splitting based on projects, solving the problem of financial cost sharing.

### Background information

Resource projects (Project) are a resource grouping management mechanism provided by BytePlus, helping users achieve logical resource isolation. You can perform operations including project\-based authorization and bill splitting through resource projects.

> **tip**

> For more project introductions, please refer to [Project Overview](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview).

### Prerequisites

The project has been created on the **Identity and Access Management** page. For details, please refer to [Project Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management).

### View results

#### View project resources

1. Log in to BytePlus [Identity and Access Management](https://console.byteplus.com/iam).

2. Select **Resource Management** \> **Project** on the left navigation bar. In the project list, select the target project and click **Manage** under the **Operation** column to view project details.

3. On the **Resources** tab, you can view the resource details of the project.

#### View splitting bills

After adding a project to the APMPlus server\-side monitoring workspace, it supports viewing splitting bills by project. The detailed operations are as follows:

1. Log in to the BytePlus [Cost Center](https://console.byteplus.com/finance).

2. Select **Bill Management** \> **Splitting Bills** in the left navigation bar.

3. On the **Splitting Bills** page, select a project from the **Project** dropdown menu to view the splitting bills for the specified project.
