---
title: "Configuring subnet IPv4 address shortage alert"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-subnet-IPv4-address-shortage-alert"
---

## Scenarios

When the IPv4 addresses in a subnet are insufficient, it may impact automatic resource scaling and pose risks to your services. You can configure an event rule in the CloudMonitor Console to trigger an automatic alert when IPv4 address usage within a subnet exceeds 80%. This will remind relevant personnel to migrate automatic scaling tasks to a newly created subnet or a subnet with available IPv4 addresses, ensuring business continuity.

## Action description

Once IPv4 address usage in a subnet triggers a CloudMonitor alert, the platform will immediately send an alert notification. Subsequently, alert notifications will be sent every 5 minutes until the IPv4 address usage across all subnets under the account falls below 80%.

## Procedures

1. Log in to the [CloudMonitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left\-side navigation pane, select **Event Center \> Event Rule**.

3. On the Event Rules page, click **Create event rule**.

4. Configure relevant parameters based on the table below.

   > **tip**

   > This article only introduces parameters and values related to VPC.

   |Parameter ||Description |Example |
   |---|---|---|---|
   |Name ||Enter the name of event rule. |VPC_InsufficientIP_alert |
   |Event rule |Resource Type |Select a resource type. **This topic uses VPC**. |VPC |
   ||Event name |VPC currently only supports **Subnet IP usage exceeding 80%** . |**Subnet IP usage exceeds 80%**  |
   ||Effective on |Specify the active time period during the day. The platform will only monitor IPv4 address usage within the subnet during the specified active time periods. |00:00\-23:59 |
   ||Severity Level |Select the severity level of the event. |Warning |
   |Delivery method |Delivery channel |Select one or more channels. |Email, phone, SMS |
   ||Alert contact group |When one or more channels, such as Email, phone, or SMS are selected, you need to select an alert contact group. |Default alert contact group |

5. Click **Confirm** to complete the action.
