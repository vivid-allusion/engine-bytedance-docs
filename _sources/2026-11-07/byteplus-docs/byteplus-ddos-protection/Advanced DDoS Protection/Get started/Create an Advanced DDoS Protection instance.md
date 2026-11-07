---
title: "Create an Advanced DDoS Protection instance"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-purchasing-an-instance-of-advanced-ddos-protection"
---

To start using BytePlus Advanced DDoS Protection, you first need to create an instance. This guide provides step\-by\-step instructions on how to purchase and configure your new DDoS instance through the console.

<span id="17ba8206"></span>
## Before you begin

Ensure your BytePlus account has no overdue payments.

<span id="7c28a0b6"></span>
## Precautions

You acknowledge and agree that if you have ordered the Advanced DDoS Protection prepaid products/services, the prepaid products/services do not support cancellation and refunds.

<span id="0cbba0cb"></span>
## Procedure


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Instance list**.

3. Click **Create instance**.

4. Set the specifications of your instance.

   
   |**Configuration** |**Description** |
   |---|---|
   |Region |The region for the instance. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">Service traffic is forwarded to our global scrubbing centers through an Anycast network. The traffic is then aggregated at the node in different regions, from which legitimate requests are returned to your origin servers.</div><br> |
   |Basic Specifications |* Provisioning mode: DNS\-based traffic redirection.<br><br>* Protective resources: An exclusive IP.<br><br>* Protection capability: Full protection for your service. |
   |Service bandwidth |The maximum legitimate traffic that the Advanced DDoS Protection instance can process after being filtered by our scrubbing centers. You are charged for the actual traffic forwarded to and from the instance, which means both the traffic back to the origin server and responding to the clients will be calculated. If the actual bandwidth usage of your business consistently surpasses the service bandwidth you have allocated, it may lead to service disruptions due to potential packet loss. We recommend choosing a bandwidth that aligns with your requirements. |
   |Protected ports |* It refers to the quantity of ports that the Advanced DDoS Protection instance can add for forwarding TCP or UDP rules.<br><br>* Each instance protects 50 ports for free, and more ports can be added if needed. Each additional block of 5 ports costs $100 USD per month. |
   |Protected domains |* It refers to the quantity of domains that the Advanced DDoS Protection instance can add for protection.<br><br>* Each instance protects 50 domains for free, and more domains can be added if needed. For every additional 5 domains, an extra USD $100 should be paid for each month. |
   |Quantity |The number of instances to purchase. Up to 10 instances can be set for each account. |
   |Duration |The subscription period for your instance. |
   |Service Agreement |Read and agree to the service level agreement, customer agreement, and service specific terms. |
   

5. Confirm your configuration, and click **Create instance**.

6. Confirm your order, and click **Next step**.

7. Proceed with the payment.

   The new instance appears in the Instance list. You can view the name, instance ID, IP address, and other details of your instance.


<span id="86ac7456"></span>
## What to do next

After creating an Advanced DDoS Protection instance, it is necessary to provision your services into the instance to protect them.


* For website services, see [Protecting a website](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-protecting-a-website).

* For port\-specific services, see [Protecting a port](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-protecting-a-port).
