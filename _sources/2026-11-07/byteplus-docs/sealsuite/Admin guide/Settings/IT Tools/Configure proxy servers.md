---
title: "Configure proxy servers"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/configuring-internet-proxies"
---

The SealSuite Internet proxy helps employees access the network through proxy servers provided by the enterprise. This article describes how administrators configure proxy servers, excluded domains, and the scope, and explains the client\-side behavior.

## Overview

Enterprises usually manage employee network access through specified proxy servers. If employees enter the server address, port, and proxy type themselves, errors can occur. When a server changes, administrators must also notify everyone again. The SealSuite Internet proxy centralizes these configurations in the Admin Console. Employees can select a proxy directly in **Network** \> **Proxy Server** on the client, without manual input. The Internet proxy provides the following capabilities:

* **Deliver proxy configurations centrally**: administrators configure proxy servers in the Admin Console (HTTP or HTTPS, up to 20 servers). Employees can select a server from the client drop\-down list. The address, port, and proxy type are maintained by administrators. When a server changes, administrators update it centrally in the Admin Console, without notifying employees one by one.

* **Route proxy access and local direct access separately**: Websites added to excluded domains are accessed directly through the local network and do not pass through the proxy server. Employees can select an HTTP or HTTPS web proxy configured by an administrator to access the network, Administrators add internal websites that require direct access to the exclusion list.

* **Control the scope by user group**: Specify employees who can use the proxy by department, role, or member. Clients for employees outside the scope do not show the Internet proxy entry and keep the original Internet access method.

## Prerequisites

Configure and enable network monitoring. For detailed instructions, see [Configure network monitoring](https://docs.byteplus.com/docs/sealsuite/docs-configuring-network-monitoring).

## Configuration steps

Proxy server configuration provides optional proxy connection information to clients. Follow these steps to add servers, set direct\-access websites, and specify users or devices in scope:

1. Log in to the Admin Console. In the left navigation pane, choose **Settings** \> **IT Tools**.

2. In the **Network Utilities** area, click **Proxy Server**.

3. In the **Proxy Server Configuration** area, click **Add Proxy Server** and configure the following items.

   |Configuration item |Description |
   |---|---|
   |Server icon, server name |Help employees identify and distinguish proxy servers on the client. Set the corresponding icon and name. |
   |Proxy type |Specify the web proxy type to use. Based on the actual proxy service configuration, select **Web Proxy (HTTP)**  or **Web Proxy (HTTPS)** . |
   |Server address |Specify the proxy server that clients connect to. Enter the domain name or IP address of the server. |
   |Port |Specify the port on which the proxy service receives connections. Enter the actual listening port of the server. The valid range is 1–65535. |

4. Click **Confirm** to add the server. Up to 20 proxy servers are supported.

5. (Optional) Configure **Exclude Domain List**.

   Excluded domains specify websites that do not pass through the proxy server and are accessed directly through the local network. In the **Exclude Domain List** area, add the website domains that require direct access.

6. Configure **Scope**.

   Effective objects specify which employees can use the Internet proxy. In this area, select the departments, roles, or members that need to use the proxy.

7. Click **Confirm** to save the configuration, and confirm that the **Proxy Server** switch is enabled on the IT Tools page. You can later enable or disable the feature using the switch on this card.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/proxy-admin-live.png)

## Client behavior

Employees within the scope go to **Network** \> **Proxy Server** on the client and select a proxy server configured by an administrator. The server name helps employees distinguish different access purposes. Excluded domains are accessed directly based on the administrator configuration.
