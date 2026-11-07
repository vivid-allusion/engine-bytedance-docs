---
title: "Arrears description"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Arrears"
---

After your account goes into arrears, Network Load Balancer (NLB) instance resources will be affected. 

<span id=".5qyg6LS55LuL57uN"></span>
## Overview

When your account is in arrears, BytePlus sends notifications by SMS, email, or internal messages based on your notification settings. Regardless of whether your instances are suspended or released, you shall settle the issued bills based on the actual.

The resource status of the instance at different stages after the account becomes overdue is as shown in the figure below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a3ff8905b1c2ba75e2e4456d0f015097.png) </span>

<span id="DEhroaY5"></span>
## NLB resource pack and coupon

When the account is in arrears but has NLB resource packs or coupons, the resource status is shown in the following table.


|Resource |NLB resource pack |NLB coupon |Elastic IP (EIP) coupon |IPv6 Internet bandwidth coupon |
|---|---|---|---|---|
|NLB Resource |The NLB instance is functioning properly. |The NLB instance is functioning properly. |NLB instance will be released due to overdue payments. |NLB instance will be released due to overdue payments. |
|EIP associated with the NLB instance |EIP will be released due to overdue payments. |EIP will be released due to overdue payments. |* EIP remains fully functional before overdue reclamation time.<br><br>* At the time of overdue reclamation:<br><br>   * The EIP created with the NLB instance is automatically deleted when the NLB instance is deleted.<br><br>   * EIP associated with the NLB instance will be automatically disassociated. |EIP will be released due to overdue payments. |
|The IPv6 Internet bandwidth of the NLB instance |IPv6 Internet bandwidth will be released due to overdue payments. |IPv6 Internet bandwidth will be released due to overdue payments. |IPv6 Internet bandwidth will be released due to overdue payments. |* IPv6 Internet bandwidth remains fully functional before overdue reclamation time.<br><br>* IPv6 Internet bandwidth will be deleted together with the NLB instance upon overdue reclamation. |


&nbsp;

&nbsp;

&nbsp;
