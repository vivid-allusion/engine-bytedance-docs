---
title: "Billing FAQs"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Billing-FAQs"
---

* [How is an EIP billed?](https://docs.byteplus.com/en/docs/48/10145#.5YWs572RSVDlpoLkvZXorqHotLnvvJ8=)

* [EIPs are billed based on actual traffic. Does the traffic include both inbound and outbound traffic?](https://docs.byteplus.com/en/docs/48/10145#.5YWs572RSVDmjInlrp7pmYXmtYHph4_orqHotLnvvIzmtYHph4_mmK_orqHnrpflh7rmlrnlkJHlkozlhaXmlrnlkJHnmoTmgLvmtYHph4_lkJfvvJ8=)

* [Do Subscription EIPs support auto-renewal? How do I renew it?](https://docs.byteplus.com/en/docs/48/10145#.5YyF5bm05YyF5pyI5YWs572RSVDmlK_mjIHoh6rliqjnu63otLnkuYjvvJ8=)

* [Do EIPs support billing conversion?](https://docs.byteplus.com/en/docs/48/10145#.5YWs572RSVDmlK_mjIHorqHotLnovazmjaLkuYjvvJ8=)

* [Will converting an EIP from Pay-by-bandwidth to Pay-by-data-transfer affect its usage?​](https://docs.byteplus.com/en/docs/48/10145#.5YWs572RSVDku47mjInluKblrr3kuIrpmZDorqHotLnovazkuLrmjInlrp7pmYXmtYHph4_orqHotLnvvIzkvJrlvbHlk43kvb_nlKjlkJfvvJ8=)

* [Can a Subscription EIP be converted to Pay-by-data-transfer?](https://docs.byteplus.com/en/docs/48/10145#.5YyF5bm05YyF5pyI5pSv5oyB6L2s5Li65oyJ6YeP6K6h6LS5LeaMieWunumZhea1gemHj-iuoei0ueWQl--8nw==)

* [How do I check the price of an EIP instance?](https://docs.byteplus.com/en/docs/48/10145#.5aaC5L2V5p-l55yL5YWs572RSVDlrp7kvovnmoTku7fmoLzvvJ8=)

* [How do I convert an EIP from Pay-by-data-transfer to Subscription?](https://docs.byteplus.com/en/docs/48/10145#bPRrIxC1)

* [If the account owning the EIP is in arrears, will additional charges still be incurred?​](https://docs.byteplus.com/en/docs/48/10145#Jh7des1r)

* [How do I troubleshoot abnormal EIP charges?​](https://docs.byteplus.com/en/docs/48/10145#oLVpEGyq)


<span id=".5YWs572RSVDlpoLkvZXorqHotLnvvJ8="></span>
## How is an EIP billed?

Elastic IP Addresses (EIPs) support both Pay\-as\-you\-go and Subscription billing. For more details, see [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

<span id=".5YWs572RSVDmjInlrp7pmYXmtYHph4_orqHotLnvvIzmtYHph4_mmK_orqHnrpflh7rmlrnlkJHlkozlhaXmlrnlkJHnmoTmgLvmtYHph4_lkJfvvJ8="></span>
## EIPs are billed based on actual traffic. Does the traffic include both inbound and outbound traffic?

No. Billing is based only on outbound traffic, accumulated over the billing period.

<span id=".5YyF5bm05YyF5pyI5YWs572RSVDmlK_mjIHoh6rliqjnu63otLnkuYjvvJ8="></span>
## Do Subscription EIPs support auto\-renewal? How do I renew it?

Yes. Log in to the [EIP console](https://console.byteplus.com/eip/eips) to manually renew or set up auto\-renewal for Subscription EIPs. For more information, see [Renewal](https://docs.byteplus.com/en/docs/eip/Renewal).

<span id=".5YWs572RSVDmlK_mjIHorqHotLnovazmjaLkuYjvvJ8="></span>
## Do EIPs support billing conversion?

Yes. EIPs support four types of billing conversions:


* Convert "Pay\-by\-bandwidth" to "Subscription".

* Convert "Subscription" to "Pay\-by\-bandwidth".

* Convert "Pay\-by\-bandwidth" to "Pay\-by\-data\-transfer".

* Convert "Pay\-by\-data\-transfer" to "Pay\-by\-bandwidth".


For procedure, see [Billing conversion](https://docs.byteplus.com/en/docs/eip/Billing-methods-change).

<span id=".5YWs572RSVDku47mjInluKblrr3kuIrpmZDorqHotLnovazkuLrmjInlrp7pmYXmtYHph4_orqHotLnvvIzkvJrlvbHlk43kvb_nlKjlkJfvvJ8="></span>
## Will converting an EIP from Pay\-by\-bandwidth to Pay\-by\-data\-transfer affect its usage?​

If the bandwidth cap remains the same before and after the conversion, it will not affect usage. If the bandwidth cap before the billing conversion is greater than 200 Mbps, the bandwidth after conversion will default to the maximum value of 200 Mbps. Reducing the bandwidth cap may affect service traffic and cause packet loss.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The bandwidth cap range for the Pay\-by\-bandwidth method is: 1 to 1000 Mbps.</div>


* <div data-tips="true" data-tips-type="tip">The bandwidth cap range for the Pay\-by\-data\-transfer method is: 1 to 200 Mbps.</div>



<span id=".5YyF5bm05YyF5pyI5pSv5oyB6L2s5Li65oyJ6YeP6K6h6LS5LeaMieWunumZhea1gemHj-iuoei0ueWQl--8nw=="></span>
## Can a Subscription EIP be converted to Pay\-by\-data\-transfer?

No. However, you can first change the metering method from Subscription to Pay\-by\-bandwidth, and then convert it from Pay\-by\-bandwidth to Pay\-by\-data\-transfer.

<span id=".5aaC5L2V5p-l55yL5YWs572RSVDlrp7kvovnmoTku7fmoLzvvJ8="></span>
## How do I check the price of an EIP instance?

You can view the price of EIP instances on the [Pricing calculator](https://www.byteplus.com/en/pricing?product=EIP&tab=2) page. The amount presented by Pricing calculator is for reference only. Specific charges are based on the order placed in [the EIP console](https://console.byteplus.com/eip/eips).

<span id="bPRrIxC1"></span>
## How do I convert an EIP from Pay\-by\-data\-transfer to Subscription?

For a Pay\-by\-data\-transfer EIP, you must first change its metering method to "Pay\-by\-bandwidth" via [Change configuration](https://docs.byteplus.com/en/docs/eip/Billing-methods-change#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS56L2s5Li65oyJ5bim5a695LiK6ZmQ6K6h6LS5), and then [convert it to Subscription](https://docs.byteplus.com/en/docs/eip/Billing-methods-change#.5oyJ5bim5a695LiK6ZmQ6K6h6LS56L2s5Li65YyF5bm05YyF5pyI).

<span id="Jh7des1r"></span>
## If the account owning the EIP is in arrears, will additional charges still be incurred?​

Yes. If the account is in arrears but the EIP is still providing services normally, charges will continue to accrue. Billing stops only after the EIP enters a suspended status.

If you still need the EIP, top up your account promptly. If you no longer need the EIP, we recommend [releasing it](https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP) as soon as possible.

<span id="oLVpEGyq"></span>
## How do I troubleshoot abnormal EIP charges?​

You can filter bills by EIP–related items in the [Bill details](https://console.byteplus.com/finance/account-overview) to review traffic charges. If anything appears abnormal, troubleshoot using the table below.


|Billing model |Anomaly |Solution |
|---|---|---|
|Pay\-as\-you\-go |EIPs are not associated with any cloud resource but still incur charges. |Verify whether such EIPs exist in any region by the following steps.<br><br><br>1. Log in to [the EIP console](https://console.byteplus.com/eip/eips).<br><br>2. Switch regions and review all EIPs across regions.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b6d43e6110da571414e964b0c15efc2c.png) </span><br><br>3. If the EIP is no longer needed, [disassociate it from the resource](https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP) and [release it](https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP). |
||Abnormal increase in EIP charges​ |If a Pay\-as\-you\-go EIP shows abnormally high traffic, unusual charges may be incurred. First, [check for abnormal EIP traffic](https://docs.byteplus.com/en/docs/eip/EIP-FAQs#Q5BlByn6). |
|Subscription |Unexpected charges on a Subscription EIP |When you convert a **Pay\-as\-you\-go** (Pay\-by\-bandwidth) EIP to a **Subscription** plan, the Subscription billing cycle starts from the time that the modification order is created. Charges incurred before the conversion but not yet billed will appear as a separate postpaid bill. You can verify the details in the [Bill details](https://console.byteplus.com/finance/bill/detail). |
