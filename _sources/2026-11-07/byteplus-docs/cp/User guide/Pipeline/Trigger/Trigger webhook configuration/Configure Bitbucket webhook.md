---
title: "Configure Bitbucket webhook"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Bitbucket_Cloud_webhook_configuration"
---

For BitbucketCloud code repositories, after you turn on the code source trigger, you need to go to the corresponding code repository to configure the pipeline Webhook address.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

Mapping between BitbucketCloud trigger events and Code Pipeline Console trigger events


* Code submission and TAG creation

* Pull request created, updated, merged \> Pull request


It is recommended to select the "Push all events" option in Bitbucket Cloud. Whether the pipeline is triggered depends on the trigger event you select and the trigger conditions you configure in the Code Pipeline console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The event trigger settings for the target pipeline have been selected, and the corresponding pipeline Webhook URL has been copied. For detailed instructions, see [code source](https://docs.byteplus.com/en/docs/cp/Trigger_from_code_source).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to BitbucketCloud, then go to the target repository homepage. Select **Repository Settings \> Webhooks**.

2. Click **Add webhook** and configure the webhook information as required. Configuration items not mentioned in the table can be configured as needed.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Title |Customize the name of the current Webhook. |
   |URL |Enter the pipeline Webhook URL prepared in the prerequisites. |
   |Status |Select **Active**; otherwise, the pipeline cannot receive Webhook events from the code source. |
   |Triggers |Select the push events as needed. It is recommended to push all events. Whether the pipeline is triggered depends on the trigger events you select and the trigger conditions you configure in the Code Pipeline console. |
   

3. Click **Save** to complete the configuration.
