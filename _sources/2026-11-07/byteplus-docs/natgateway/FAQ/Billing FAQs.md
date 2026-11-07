---
title: "Billing FAQs"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Billing-FAQ"
---

* [How is an Internet NAT Gateway billed?](https://docs.byteplus.com/en/docs/51/10037#.5YWs572RTkFU572R5YWz5aaC5L2V6K6h6LS577yf)

* [After an Internet NAT Gateway is disassociated from an EIP, is the gateway still billed?](https://docs.byteplus.com/en/docs/51/10037#.5YWs572RTkFU572R5YWz6Kej57uR5YWs572RSVDlkI7vvIzov5jnu6fnu63mlLbotLnlkJfvvJ8=)

* [Can I change the specification of an Internet NAT Gateway, and how is the Internet NAT Gateway billed?](https://docs.byteplus.com/en/docs/51/10037#.5YWs572RTkFU572R5YWz5pSv5oyB5Y-Y5pu06KeE5qC85ZCX77yM5oCO5LmI6K6h566X6LS555So5ZGi77yf)

* [Does the Internet NAT Gateway support billing conversion?](https://docs.byteplus.com/en/docs/51/10037#e1t2Lae8)

* [Do subscription Internet NAT Gateways support auto renewals?](https://docs.byteplus.com/en/docs/51/10037#.5YyF5bm05YyF5pyI5YWs572RTkFU572R5YWz5pSv5oyB6Ieq5Yqo57ut6LS55ZCX77yf)

* [If the BytePlus account that owns the NAT Gateway is in arrears, will charges still be incurred?](https://docs.byteplus.com/en/docs/51/10037#92eesFw6)


<span id=".5YWs572RTkFU572R5YWz5aaC5L2V6K6h6LS577yf"></span>
## How is an Internet NAT Gateway billed?

Internet NAT Gateways support the Pay\-as\-you\-go and Subscription billing. For more information, see [Internet NAT Gateway Billing overview](https://docs.byteplus.com/en/docs/natgateway/Billing-overview).

If you need the internet NAT Gateway to associate with an Elastic IP Address (EIP), enabling internet communication, you will also need to apply for an EIP and pay the fee for it. For EIP billing details, see [EIP Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

<span id=".5YWs572RTkFU572R5YWz6Kej57uR5YWs572RSVDlkI7vvIzov5jnu6fnu63mlLbotLnlkJfvvJ8="></span>
## After an Internet NAT Gateway is disassociated from an EIP, is the gateway still billed?

The fees for the Internet NAT Gateway and the EIP are charged separately, and separate bills are issued. Before the Internet NAT Gateway is released, the specification configuration fee is charged on the gateway side regardless of whether the EIP is attached.

If you disassociate an Internet NAT Gateway from an EIP but do not release the EIP, the Internet NAT Gateway is still charged a specification fee and the EIP is also charged a fee. For more information, see Billing of EIPs.

<span id=".5YWs572RTkFU572R5YWz5pSv5oyB5Y-Y5pu06KeE5qC85ZCX77yM5oCO5LmI6K6h566X6LS555So5ZGi77yf"></span>
## Can I change the specification of an Internet NAT Gateway, and how is the Internet NAT Gateway billed?

You can change the specification of an Internet NAT Gateway. For more information, see Specification changes and Changing the specification of an Internet NAT Gateway.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Subscription Internet NAT Gateways do not support specification downgrades.</div>


<span id="e1t2Lae8"></span>
## Does the Internet NAT Gateway support billing conversion?

Internet NAT Gateway supports the following types of billing conversion:


* Convert between Pay\-by\-CU and Pay\-by\-specification

* Convert between Pay\-by\-specification and Subscription

* Convert Subscription to Pay\-by\-CU.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Converting from Pay\-by\-CU to Subscription is not supported for internet NAT Gateways. For more details, see <a href="https://docs.byteplus.com/en/docs/natgateway/Billing-method-change">Billing conversion</a>.</div>


* <div data-tips="true" data-tips-type="default">Subscription Internet NAT Gateways support only specification upgrades. Before you switch from Pay\-as\-you\-go to subscription, we recommend that you determine whether you need to change the specification.</div>



<span id=".5YyF5bm05YyF5pyI5YWs572RTkFU572R5YWz5pSv5oyB6Ieq5Yqo57ut6LS55ZCX77yf"></span>
## Do Subscription Internet NAT Gateways support auto renewals?

Yes. Internet NAT Gateways support both manual and automatic renewal methods. For details, see [Renewal](https://docs.byteplus.com/en/docs/natgateway/Renewals).

<span id="92eesFw6"></span>
## If the BytePlus account that owns the NAT Gateway is in arrears, will charges still be incurred?

Yes. If the account is in arrears but the NAT Gateway is still providing services normally, charges will continue to accrue. Billing stops only after the NAT Gateway enters the Suspended status.

If you still need to use this NAT Gateway, [top up](https://docs.byteplus.com/en/docs/6269/100434) your account promptly. If you no longer need it, we recommand [deleting the Internet NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Deleting-a-NAT-gateway)/[deleting the VPC NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Deleting-a-VPC-NAT-Gateway) as soon as possible.
