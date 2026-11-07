---
title: "Configure DNS reset"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-k86j4knvfd"
---

SealSuite DNS reset helps employees adjust DNS configurations to resolve network issues related to domain name resolution. This document describes how administrators configure DNS reset and how it appears in the client.

## Overview

DNS reset helps employees adjust the DNS servers used by their devices. It applies to scenarios such as website access failures or abnormal domain name resolution caused by unsuitable DNS configurations. The SealSuite client provides automatic reset and manual reset. Employees can restore automatic DNS retrieval through DHCP or manually enter DNS server addresses.

administrators can further enable **DNS selection** to centrally configure DNS servers and auxiliary speed test websites for employees to select. After the configuration takes effect, the client tests the speed of candidate DNS servers and displays the server addresses and latency results. Employees can select a server based on the test results. They can also run the detection again to compare server response times on the current network.

For example, an enterprise may want employees to use specified DNS servers, while allowing them to select faster servers based on their network. In this case, administrators can configure multiple candidate addresses. Employees can view the speed test results in the client and make a selection, without searching for or entering addresses manually.

## Configuration steps

1. Log in to the Admin Console. In the left navigation pane, choose **Settings** \> **IT Tools**.

2. In the **Network Utilities** area, click the **DNS Reset** card.

3. View **DNS reset mode**.

   **Automatic DNS reset** and **Manual DNS reset** are basic features provided by the client. They are selected by default and cannot be modified.

   |Mode |How it works |
   |---|---|
   |Automatic reset |Automatically obtains the DNS configuration based on Dynamic Host Configuration Protocol (DHCP). |
   |Manual reset |Employees enter DNS server addresses in the client. |
   |DNS selection |Completes speed tests based on DNS server addresses configured by the administrator, so employees can select a server. |

4. Enable **DNS selection** as needed and configure the following items.

   |Configuration item |Description |
   |---|---|
   |DNS server address |Configure candidate DNS servers for employees to select. After DNS selection is enabled, the client tests the speed of these servers. Employees select a server based on the results. You can configure up to 5 servers. Adding, editing, and deleting servers are supported. |
   |Common websites |Configure website addresses used to assist DNS server speed tests. Employees can use these websites in their client to test the speed of candidate DNS servers and compare the results. You can configure up to 5 websites. Adding, editing, and deleting websites are supported. |

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/dns-admin-live.png)

5. Click **Confirm**.

## Client experience

Employees go to **Lab** \> **DNS Reset** in the SealSuite client, then select a reset method as needed:

* **Restore automatic DNS retrieval**: Select **Automatic DNS reset**. The system obtains the DNS configuration based on the current network.

* **Use a specified DNS server**: Select **Manual DNS reset** and enter the DNS server address provided by the IT administrator.

* **Select a DNS server after speed testing**: After the administrator enables and configures DNS selection, employees can view the system\-recommended addresses and latency on the manual reset page, then select an appropriate server. Click **Re\-run** to test the latency of candidate servers again.

> **说明**

> Using an enterprise internal DNS address outside the enterprise intranet may cause network access issues. Before using an internal DNS server, confirm that the current network can access the server.

> For details about client operations, see [Labs: DNS reset](https://help.feilian.cn/help-center/laboratorylaboratory?lang=en#39c6111c).
