---
title: "Dynamic control FAQ"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-dynamic-control-faq"
---

While using the SealSuite dynamic control module, if you encounter any issues or have questions, refer to the following frequently asked questions and its provided solution for assistance.

<span id="cc6cf7ab"></span>
## How to understand the belong to and include triggering parameters in dynamic control ?


* Belong to: The specific conditions need to be perfectly matched.

* Include: Refers to fuzzy matching.


<span id="c7751815"></span>
## What is the reason why a member is unable to hit the dynamic rule triggered by "Obtain VPN gateways"?

If the triggering method in the dynamic decision rule group is set to "Obtain VPN gateways", members need to perform the following actions to pull the VPN gateway list again to trigger the rule.


1. Start the application.

2. Enter the network page.

3. Open the gateway list.

4. Network switch detected.


<span id="a5e5ed9f"></span>
## How to handle the failure of calling the built\-in application control template for dynamic control function?

Please confirm whether you have purchased the license for application control. Failure to purchase will result in an error call.

<span id="8b46fcfe"></span>
## How to handle the notification sent by the robot configured in the dynamic control function, which does not reference real information but instead uses fixed text?

You need to confirm whether the format of the configured notification content is correct, and the variable needs to be guided out with a pound sign (#) to display the relevant configuration options.
