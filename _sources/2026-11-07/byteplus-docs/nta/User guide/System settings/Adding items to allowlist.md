---
title: "Adding items to allowlist"
product: "Network Detection and Response"
product_code: "nta"
source: "https://docs.byteplus.com/en/docs/nta/Adding-items-to-the-allowlist"
---

If you identify some alerts that are actually normal network services or behaviors during security alert analysis, you can add these alerts to an allowlist to reduce false alerts.

<span id="9769b2ee"></span>
## Adding items to the allowlist


* You can choose **Add allowlists** for a risky port while viewing alert events by asset. For more information, refer to [Viewing asset risk information](https://docs.byteplus.com/docs/nta/Viewing-asset-risk-information).

* You can choose **Add allowlists** for a threat type while viewing alert events by alert. For more information, refer to [Viewing alert events](https://docs.byteplus.com/docs/nta/Viewing-alert-events).


You can go to **System settings** \> **Allowlist configuration** to view the added items or edit the allowlist information.

<span id="7f4fc5bc"></span>
## Adding allowlists

The IP addresses and ports added to an allowlist won't trigger the specific type of security alerts.


1. Log in to the NDR console.

2. Select **System settings** \> **Allowlist configuration** on the left side of the page.

3. Click **Add allowlists** and enter the corresponding parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |External IP address |It must be a public IP address or network segment in the format IP address/subnet mask, where IP address 0.0.0.0 indicates all public IP addresses. |
   |External port |Port ranges are supported, for example, 80\-80 or 100\-200. The range 0\-65535 indicates all ports. |
   |Asset IP address |The public IP address of an asset in your account. IP address 0.0.0.0 indicates the public IP addresses of all purchased assets. |
   |Asset port |Port ranges are supported, for example, 80\-80 or 100\-200. The range 0\-65535 indicates all ports. |
   |Protocol |Either TCP or UDP can be selected. |
