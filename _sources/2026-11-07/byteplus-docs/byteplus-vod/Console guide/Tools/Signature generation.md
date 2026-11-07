---
title: "Signature generation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-signature-generation"
---

To calculate the signature for Type A URL signing of your BytePlus VOD acceleration domain name, you can use the signature tool available in the VOD console. This guide walks you through the prerequisites and the step\-by\-step procedure for generating a valid signature.

<span id="7c302d8e"></span>
## Prerequisites


* [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management)

* Enable and configure Type A URL signing. For details, see [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview).


<span id="22363077"></span>
## Procedure


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Tools** \> **Signature generation** on the left navigation bar.

3. Follow the on\-screen instructions to complete the parameter configuration. The detailed description of each parameter is provided in the table below.

   
   |Parameter |Description |
   |---|---|
   |URL signing type |Type A |
   |Signature key |Set the signature key in the following ways:<br><br><br>* Manually enter the signature key, which must be 6\-40 characters long and can contain letters and numbers.<br><br>* Click the **Auto get** button next to the input box and select the BytePlus VOD domain name from the pop\-up box. The system will automatically retrieve the key that you have configured from the domain name. |
   |URI |Enter the URI. The following rules must be followed:<br><br><br>* The file path must start with a forward slash (`/`) and does not include the domain name.<br><br>* The file path can contain printable ASCII characters except for consecutive slashes (`//`), percent signs (`%`), dollar signs (`$`), spaces, question marks (?), and Delete (ASCII code 127) characters. |
   |Random string |Enter a random string. It can only contain letters and numbers and cannot exceed 100 characters. |
   |Timestamp |The simulated signing time point can be set to the current time, a future time, or a past time. You can configure the timestamp in the following ways:<br><br><br>* Manually enter the timestamp, which should not exceed 2147483647.<br><br>* Click the **Auto get** button next to the input box. |
   |Validity duration |Specify the validity duration based on your business requirements. This parameter, used in conjunction with the timestamp parameter, determines the expiration time of the signature. The unit of measurement is in seconds, with a valid range of 0 to 315,360,000 seconds.<br><br>The formula to calculate the expiration time of the signature is:<br><br>Expiration time = timestamp + validity duration.<br><br>If BytePlus VOD receives a request with a signature expiration time earlier than the current time, the CDN identifies the signature as expired. In such instances, a 403 response status code is issued, indicating authentication failure. |
   

4. Click the **Generate** button. You can view and copy the signature result on the right side of the page.


<span id="1d2f7200"></span>
## References

To learn about the logic behind Type A URL signing, see [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview) and [Type A signing](https://docs.byteplus.com/docs/byteplus-vod/docs-type-a).
