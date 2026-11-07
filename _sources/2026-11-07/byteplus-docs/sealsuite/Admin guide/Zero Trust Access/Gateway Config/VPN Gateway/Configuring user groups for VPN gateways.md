---
title: "Configuring user groups for VPN gateways"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-user-groups-for-vpn-gateways"
---

You can specify the users who have the permission to use the VPN function for each VPN gateway.

<span id="c3252aa1"></span>
# Instructions for use

If you have added a rule group relating to **Adjust** **VPN** **gateways** **that** **are** **available** **for** **users** through Dynamic Control in the Admin Portal, it will take precedence over rules for setting **Scope** within VPN gateways.

<span id="425dec16"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **Zero Trust Access** \> **Gateway Config** \> **VPN Gateway**.

3. On the **VPN** **Gateway** page, click your target VPN gateway card, and then click the **Access Group** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb19a77abd74721b8acab3d6802488e~tplv-goo7wpa0wc-image.image) </span>

4. In the **Add Gateway Access Rule** dialog box, complete the following configuration and click **Confirm**.

   
   |**Field** |**Description** |
   |---|---|
   |**User Scope** |Specify the group of users who are entitled to use the VPN gateway based on **Department**, **Role** or **member**. Only designated employees can view and use the VPN gateway. |
   |**Gateway** |By default, this field is automatically set to the VPN gateway that you want to configure. However, you can configure other VPN gateways for your target user group as needed. |
