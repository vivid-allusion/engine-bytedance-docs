---
title: "Configure a GitLab webhook"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Configure_a_GitLab_webhook"
---

For GitLab code repositories, after you turn on the code source trigger, you need to go to the corresponding code repository to configure the pipeline's Webhook address.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

The mapping between Gitlab trigger events and Code Pipeline console trigger events is as follows.


* Push events \> Code commit

* Create tag

* Merge request events (merged) \> Merge request


It is recommended to select the option to push all events in Gitlab. Whether the pipeline is triggered is determined by the trigger event you select and the trigger condition you configure in the Code Pipeline console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The event trigger settings for the target pipeline have been enabled, and the corresponding pipeline Webhook URL has been copied. For detailed instructions, see [code source trigger](https://docs.byteplus.com/en/docs/cp/Trigger_from_code_source).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to GitLab and go to the main page of the target repository. Select **Settings \> Webhooks**.

2. Configure the Webhook settings as required. Configuration items not mentioned in the table can be configured as needed.

   
   |Configuration Item |Descriptions |
   |---|---|
   |URL |Enter the pipeline Webhook URL prepared in the prerequisites. |
   |Trigger |Select the push events you need. It is recommended to select the option to push all events. Whether the pipeline is triggered depends on the trigger event you select and the trigger conditions you configure in the Code Pipeline console. |
   

3. Click **Add webhook** to complete the configuration.
