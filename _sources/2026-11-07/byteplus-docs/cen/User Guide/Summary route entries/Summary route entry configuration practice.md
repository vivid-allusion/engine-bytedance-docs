---
title: "Summary route entry configuration practice"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Summary-route-entry-configuration-practice"
---

This topic explains how to leverage the Cloud Enterprise Network (CEN) route summarization feature to conserve routing table space on on\-premises switches and simplify routing management for the local IDC.

> **tip**

> The summary route entry is currently in beta stage. If you need a trial, please contact your account manager.

## Scenarios

When Virtual Private Cloud (VPC) and cloud\-based IDC are interconnected and there are too many cloud\-based routes, these routes will occupy a large portion of the route table space on the cloud\-based IDC switch, making route management for the cloud\-based IDC complex. The summary route entry feature of the CEN can significantly reduce the number of cloud\-based routes, simplifying route management for cloud\-based IDC.

## Prerequisites

* Network connectivity between the cloud VPC and the on\-premises IDC has been established. For specific configuration, see [Direct Connect Gateway best practices](https://docs.byteplus.com/en/docs/directconnect/Best-Practices-4).

* It has been confirmed that the routes for the cloud VPC subnet segments have been synchronized to the routing tables of the on\-premises IDC switches.

## Configuration procedures

### Step 1: Configure summary route entry on CEN

1. See [Viewing the CEN route](https://docs.byteplus.com/en/docs/cen/Route-entries-02) to check the route entries in the target CEN instance. Identify and consolidate route entries where the source instance is a VPC. Combine multiple smaller network segment routes into one larger summary route.

   For example, the route entries in a CEN instance can be summarized into the Summary route shown in the table below.

   |CEN route entry ||Summary route |
   |---|---|---|
   |Destination CIDR |Source Instances |Destination CIDR |
   |192.168.1.0/24 |vpc01 |192.168.0.0/20 |
   |192.168.2.0/24 |vpc01 ||
   |192.168.3.0/24 |vpc02 ||
   |192.168.4.0/24 |vpc02 ||
   |192.168.5.0/24 |vpc02 ||
   |192.168.34.0/24 |dcg01 |\- |

2. On the **Summary route** tab, click **Configure summary route** to configure the cloud route consolidated in the previous step.

3. Check the Direct Connect Gateway routes to confirm that the configured summary route has been synchronized into the Direct Connect Gateway routing table.

   1. On the **Network Instances** tab, click the name of the Direct Connect Gateway loaded in the CEN to navigate to the Direct Connect Gateway details page.

   2. On the **Route Table** tab, view the route entries in the Direct Connect Gateway.

### Step 2: Reject specific routes on the on\-premises switch

> **tip**

> The following steps use Huawei switches and H3C switches as examples to illustrate the configuration commands for rejecting specific routes on the on\-premises switch.

1. Log in to the switch's command line interface

2. Execute the following commands to configure filtering of the received global routing information.

   > **tip**

   > In the commands below: <ip_address\> represents the IP of the summary route, e.g., `192.168.0.0`; <mask\> represents the mask of the summary route segment, e.g., 20.

   * Huawei switch

      ```Plain Text
      ip ip-prefix FROM_HUOSHAN_V4 index 10 permit <ip_address> <mask>
      route-policy FROM_HUOSHAN_V4 permit node 10
      if-match ip-prefix FROM_HUOSHAN_V4
      ```

   * H3C switch

      ```Plain Text
      ip prefix-list FROM_HS_V4 index 10 permit <ip_address> <mask>
      route-policy FROM_HUOSHAN_V4 permit node 10
      if-match ip address prefix-list  FROM_HS_V4
      ```

### Step 3: Verify the effect of summary route configuration

1. Log in to the switch and access the user view.

2. Execute the following command to verify that the synchronized cloud route is the summary route and that the specific routes for the VPC subnets no longer exist.

   > **tip**

   > The following command applies to both Huawei and H3C switches.

   ```Plain Text
   display routing-table
   ```
