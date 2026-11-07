---
title: "Creating an Internet Tunnel Bandwidth"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Creating-the-internet-bandwidth"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After completing the creation of the Internet Tunnel (IT) Gateway, you also need to create an IT Bandwidth for the gateway. To enable Internet access, add an IT Public IP to the bandwidth.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have completed BytePlus [account registration](https://docs.byteplus.com/en/docs/6261/64925) and real\-name authentication before you can purchase Direct Connect resources.

* You have created an IT Gateway. For procedure, see [Creating an Internet Tunnel Gateway](https://docs.byteplus.com/en/docs/directconnect/Creating-an-Internet-Tunnel-gateway).

* Your account has an [available balance](https://docs.byteplus.com/en/docs/6269/100429)​ of no less than USD 0. If your balance is insufficient, recharge before creating the IT Bandwidth. For procedure, see [Recharge](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Internet Tunnel Gateway console](https://console.byteplus.com/dc/InternetTunnelGateway).

2. In the top menu bar, select your target region.

3. In the IT Gateway list, click the name of the target IT Gateway to enter its details page.

4. Click the **IT Bandwidth** tab, then click **Create IT Bandwidth**. On the Create IT Bandwidth page, configure the parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Billing method |The billing method of the IT Bandwidth. Currently, only **Pay\-as\-you\-go** is supported. |Pay\-as\-you\-go |
   |Region |The region where the IT Bandwidth is located. It defaults to the region of its IT Gateway. No modification is required. |China (Beijing) |
   |IT Gateway |The IT Gateway to which the IT Bandwidth belongs. It defaults to the current IT Gateway ID. No modification is required. |itg\-12ajc0ris7egw17q7y2p9\*\*\*\* |
   |Name |Set the name for the IT Bandwidth. |Bandwidth \- internet |
   |**Public network information** |||
   |ISP |Select the ISP for the IT Bandwidth.<br><br><br>* The ISP cannot be modified after the IT Bandwidth is created.<br><br>* You can only add IT Public IPs with the same ISP to the IT Bandwidth.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Actual available ISPs are subject to the display in your console. To request more ISPs, please contact your account manager.</div><br> |BGP (multi\-line) |
   |Metering method |Select the billing method for the IT Bandwidth. Currently, only **Pay\-by\-95th\-peak** is supported, with a minimum guaranteed ratio of 20%.<br><br>To learn more, see [Billing](https://docs.byteplus.com/en/docs/directconnect/Billing-overview-1#.5YWs572R5bim5a696LS5). |Pay\-by\-95th\-peak |
   |Maximum bandwidth |Set the maximum bandwidth for the IT Bandwidth. |300 |
   |Agreement |Follow the console guidance to review and accept the legal terms. |Check |
   |**Advanced option** |||
   |Project |The selected project. For more information, see [Project management](https://docs.byteplus.com/en/docs/directconnect/Project_Management).<br><br><br>* If you select "All Resources" for the account in the top menu bar before entering the creation page, you can choose an existing project from the dropdown.<br><br>* If you select a specific target project in the top menu bar, only target project can be selected.<br><br><br>If you need to move an IT Bandwidth to a different project after its creation, see [Move resources into a project](https://docs.byteplus.com/en/docs/6649/94337). |default |
   |Tag |Add one or more custom tags to the IT Bandwidth as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/directconnect/Tag_Management).<br><br>Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e69956428611ee87141a75073bce3c8a.png) </span> icon, type the tag key and tag value, and add the tag to the IT Bandwidth. |* Tag key: ITBandwidth\-key<br><br>* Tag value: ITBandwidth\-v1 |
   

5. Click **Submit** to complete the creation of the IT Bandwidth.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After the IT Bandwidth is created, you can add an IT Public IP to it for internet access. For procedure, see [Applying for an IT Public IP](https://docs.byteplus.com/en/docs/directconnect/Applying-for-an-Internet-Tunnel-address) and [Add an IT Public IP](https://docs.byteplus.com/en/docs/directconnect/Managing-the-internet-bandwidths#.5re75Yqg5LqS6IGU572R6YCa6YGT5YWs572RSVA=).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateInternetTunnelBandwidth](https://docs.byteplus.com/en/docs/directconnect/CreateInternetTunnelBandwidth): Create an IT Bandwidth.
