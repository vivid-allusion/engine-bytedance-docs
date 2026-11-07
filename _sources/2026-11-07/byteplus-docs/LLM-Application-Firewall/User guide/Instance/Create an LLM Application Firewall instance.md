---
title: "Create an LLM Application Firewall instance"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/create_an_LLM_Application_Firewall_instance"
---

To protect your LLM applications with the LLM Application Firewall, you must first create an instance. This guide provides step\-by\-step instructions for purchasing and creating your first instance, and explains important precautions to be aware of. Following these steps will enable you to integrate your domains and configure protection rules.

<span id="8c7f0c06"></span>
## Prerequisites

You have completed enterprise identity verification.

<span id="a6d8276d"></span>
## Precautions


* Each account can create only one instance in a given region. After the instance expires and is reclaimed, a new instance can be purchased.

* Instances are reclaimed 15 days after they expire. Please update your DNS settings in advance to avoid disruption to your normal business operations.

* Expired instances only retain forwarding capability and no longer provide protection. The CNAME resolution will not be changed for domains onboarded via traffic\-based methods.


<span id="215c4b0d"></span>
## Create your first instance


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. On the welcome page, click **Activate now**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If this is not your first time creating an instance, go to <strong>Settings \> Instance management</strong> and click <strong>Purchase Instance</strong>.   </div>
   

3. The configuration\-related purchase parameters are explained below.

   
   |Parameter |Description |
   |---|---|
   |Instance name |Optional parameter. If left blank, an instance name will be generated automatically.<br><br> |
   |Billing mode |* **Annual or monthly subscription**: Billing is based on the specifications of the selected plan and the duration of use. Prices vary by plan. For details, see [Subscription](https://docs.byteplus.com/docs/LLM-Application-Firewall/billing_model_and_pricing_details#9ee9e8b7).<br><br>* **Pay\-as\-you\-go**: Fees are comprehensively calculated based on billing items such as detection and response generation, and fees are paid based on actual hourly usage. For more information, see [Pay-as-you-go](https://docs.byteplus.com/docs/LLM-Application-Firewall/billing_model_and_pricing_details#8e90bbb0). |
   |Region |Region of the instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">We recommend selecting a region close to your protected resources to minimize network latency.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can purchase one instance per region. A new instance can be purchased after the previous one expires and is reclaimed.</div><br> |
   |Package specifications |With annual or monthly billing, you can choose different specifications. |
   

4. After confirming the selected configuration, read and agree to the relevant service agreements by checking the corresponding boxes.

5. Click **Buy Now** to enter the order management page. Confirm the order information.

6. After confirming that the order information is correct, complete the payment.

   The instance takes effect immediately after purchase. After purchase, connect your domains to the instance and configure a protection policy to enable protection.


<span id="3639b549"></span>
## View instance information

You can view information about purchased instances on the instance management page and learn about the specifications and the effective time of the instances.


1. Log in to the [LLM Application Firewall console](https://console.byteplus.com/omni-shield/llm-shield/).

2. In the top bar, select the region to which the instance belongs.

3. In the left navigation, select **Settings \> Instance management**.

4. View instance region, specifications, expiration time, and other information.


<span id="adb3087c"></span>
## Related operations


* Modify an instance name: Change the name of your instance.

* Unsubscribe: Deletes the instance. When an instance is deleted, its associated protection policies and configurations are also permanently removed.

* Modify configuration: Modify instance configurations. The LLM Application Firewall supports the following four methods for modifying configurations:

   * Switch from annual or monthly subscription to pay\-as\-you\-go billing

   * Switch from pay\-as\-you\-go to annual or monthly subscription billing

   * Downgrade the specifications of annual and monthly subscription plans

   * Upgrade annual and monthly subscription plans
