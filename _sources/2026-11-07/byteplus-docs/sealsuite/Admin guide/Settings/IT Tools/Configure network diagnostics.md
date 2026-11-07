---
title: "Configure network diagnostics"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-network-diagnosis"
---

The SealSuite network diagnostics feature helps employees check network connectivity and website access, and troubleshoot network issues. This article describes how an administrator configures network diagnostics and how the feature works in the client.

## Overview

When employees cannot connect to the internet, cannot open an internal enterprise website, or experience slow access, they often cannot determine whether the issue is with the local network, the VPN connection, or website access. SealSuite network diagnostics centrally checks the local network status and access to specified websites. This helps employees identify issues and provides IT administrators with information for further troubleshooting.

administrators can enable diagnostics based on the enterprise office network and configure business URLs to check. The client displays and runs only enabled checks. The following checks are supported:

* **Diagnose local network status**: Checks the connection status of wired, wireless, and cellular networks, whether a system network proxy is enabled, and the VPN connection status. This helps employees identify network connection or configuration issues.

* **Check internet and intranet access**: Checks the accessibility, DNS resolution, access latency, and jitter of internet and internal enterprise websites. This helps troubleshoot issues such as inaccessible websites, DNS resolution errors, and slow access. For example, if internet access works but an internal website cannot be opened, employees can use the VPN connection check and internal URL check results to narrow down the issue.

* **Submit issues and diagnostic results**: Employees can submit diagnostic results to IT administrators. If diagnostics pass but a website still cannot be accessed, employees can also provide the inaccessible URL. administrators can continue troubleshooting based on the issue description, diagnostic results, and client logs.

Network diagnostics applies to the following enterprise scenarios:

* The enterprise uses both internet applications and internal business websites, and needs to check internet and intranet access separately.

* Remote work relies on VPN to access internal resources, and the enterprise needs to distinguish issues with the local network, VPN connection, and business website access.

* The IT team frequently receives reports about network connectivity or website access issues, and needs detailed check results to reduce repeated troubleshooting information collection.

## Configuration steps

1. Log in to the Admin Console. In the left navigation pane, choose **Settings** \> **IT Tools**.

2. In the **Network Utilities** section, click **Network Diagnostics**.

> **说明**

> The diagnostic items on the configuration page are enabled by default and displayed in the client. After an administrator disables a diagnostic item, the client no longer displays or runs that check.

1. In **Network Diagnostic Configuration**, enable or disable the following diagnostic items as needed.

   |Configuration item |Description |
   |---|---|
   |Network connection diagnostics |Checks the connection status of wired, wireless, and cellular networks. |
   |Network proxy diagnostics |Checks whether a system network proxy is enabled on the client. |
   |VPN connection diagnostics |Checks the client VPN connection status. |

2. In **Network address detection**, configure the following settings.

   When you configure URLs to check, we recommend adding office websites and internal business addresses that employees actually use to **Internet websites** and **Internal websites** respectively. This ensures that the check scope covers common office needs. You can disable diagnostic items for network capabilities that the enterprise does not use. This prevents checks unrelated to the office environment from appearing.

   |Configuration item |Description |
   |---|---|
   |**Internet websites** |Configures internet websites to check from employee devices, such as commonly used office websites. The client checks the accessibility, DNS resolution, access latency, and jitter of these websites. |
   |**Internal websites** |Configures internal enterprise business websites to help employees check access to internal resources. |
   |Check item name |Sets the check item name displayed in the client. The default names are **Internet websites** and **Internal websites**. Click the edit icon on the right side of the name to customize it. Multilingual configuration is supported. |
   |URL list |Configures the website names and addresses to check. Each group supports up to 8 URLs. When the corresponding module is enabled, you can add URLs, or edit and delete the 3 system default URLs and custom URLs. Use the switch in the upper\-left corner of the module to enable or disable the check group. After the group is disabled, the client does not display or run the check group. |

3. Click **Confirm**.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/it-tools-en-20261023/diagnosis-admin-live.png)

## Client behavior and usage

1. Employees go to **Lab \> Network diagnostics**. The client automatically starts diagnostics. After diagnostics complete, employees can view the results.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bec69793b494d0abecf04a17aaae601~tplv-goo7wpa0wc-image.image)

2. Troubleshoot issues based on the check prompts, and run diagnostics again as needed.

3. After diagnostics complete and the check results contain issues, click **Feedback** to report the diagnostic results to the Admin Console.

   If diagnostics pass but a website still cannot be accessed, click **Still having issues**, enter the inaccessible URL, and then click **Feedback**.

administrators can view feedback and diagnostic results in **Enterprise Settings** \> **Admin Center** \> **User Feedback**. For more information, see [Handle user feedback](https://docs.byteplus.com/docs/sealsuite/docs-user-feedback).

After employees submit feedback, they can proactively contact IT administrators to view backend data and follow up. For client diagnostic prompts and other operations, see [Labs: Network diagnostics](https://help.feilian.cn/help-center/laboratorylaboratory?lang=en#2bca717a). When administrators need device and network information, employees can go to **Lab \> Local information** to copy the relevant information. For more information, see [Local information](https://help.feilian.cn/help-center/laboratorylaboratory?lang=en#2611542f).
