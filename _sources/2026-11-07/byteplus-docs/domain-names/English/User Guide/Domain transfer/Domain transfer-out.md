---
title: "Domain transfer-out"
product: "BytePlus Domain Names"
product_code: "domain-names"
source: "https://docs.byteplus.com/en/docs/domain-names/domain-transfer-out"
---

This document describes how to transfer a domain from BytePlus Domains to another registrar.

<span id="r3y26G6O"></span>
## Overview

A domain transfer out refers to transferring a domain from BytePlus to another domain registrar. After the transfer is completed, the domain will no longer be managed by BytePlus Domains. Please proceed with caution. A domain transfer typically takes 5–7 days to complete. During the transfer process, you cannot renew the domain.


> * Before initiating the transfer, please carefully verify the domain information. The authorization code will be sent to the email address associated with your domain registration. Please check your inbox accordingly.

> * The authorization code is valid for 5 days. It will automatically expire after this period.

> * To ensure domain security, if you do not plan to transfer the domain, please enable the [transfer lock](https://docs.byteplus.com/en/docs/domain-names/domain-transfer-in_en#transfer-lock) promptly.


<span id="11Y1crZa"></span>
## Transfer rules

To transfer a domain out of BytePlus, the following rules must be met:


* The domain must have been registered for more than 60 days.

* If you performed an ownership change and chose not to disable the 60\-day transfer lock, you must wait 60 days before transferring the domain out.

* The domain must have been with BytePlus for more than 60 days since its last successful transfer from another registrar.

* The domain status must be Active, with no outstanding payments, pending arbitrations, legal proceedings, or disputes.

* The domain cannot be transferred if its status is `ServerTransferProhibited` (set by the registry) or `ClientTransferProhibited` (set by the registrar).


<span id="Lo7PxRik"></span>
## Precautions


* **Renewal Restriction:**  During the transfer process (5–7 days), you cannot manually renew the domain, and auto\-renew will not be triggered. If your domain is about to expire, please renew it before initiating the transfer to avoid service interruption.

* **The 45\-Day Rule:**  If your domain has expired and you have just renewed it, it is recommended to wait 45 days after the renewal before transferring it out. Otherwise, the previous renewal may become invalid, resulting in a loss of the renewal fee.


<span id="7vcOaBjb"></span>
## Steps


1. Log in to the BytePlus Domains console and go to the [Domain list](https://console.byteplus.com/domain-service/domain?) page.

2. Locate the domain you want to transfer out.

3. In the **Actions** column, click **Manage**.

4. On the domain management page, verify the email address listed under **General Information**.

   * The authorization code will be sent to this email address. 

   * If the email address is incorrect, you need to create a registrant profile with the correct email and perform an ownership change before transferring the domain out.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260324131229-1230858346128.webp) </span>

5. Click the  **... ** button in the upper right corner, then select **Transfer domain out**.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260324131045-270891775946.webp) </span>

6. On the **Domain transfer\-out** page, click **Submit transfer request**.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260324131253-360755886589.webp) </span>

7. Confirm the domain name, registrant, and email information. If correct, click **Submit**.

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260324131333-99548498491.webp) </span>

8. Enter the SMS verification code. The system will automatically send the authorization code to the registrant's email address.


Once you have the authorization code, you can submit a transfer\-in request at your new registrar. The code is valid for 5 days.

**To cancel a transfer:** 

If you want to cancel the transfer request, before it is approved, repeat Steps 1–3. Then, on the **Domain transfer\-out** page, locate the transfer record and click **Cancel ** in the **Actions** column. After entering the SMS verification code, the transfer will be canceled, and the authorization code will immediately become invalid.
