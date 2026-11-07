---
title: "Configure GitHub webhook push"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Configure_GitHub_webhook_push"
---

For GitHub code repositories, after you enable the code source trigger, you need to configure the pipeline Webhook address in the corresponding repository.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

Correspondence between GitHub trigger events and Code Pipeline console trigger events is as follows.


* Pushes \> Code commit

* Branch or tag creation \> Create a tag

* Pull requests (merged) \> Pull requests


It is recommended to select the option "Push all events" on GitHub. Whether the pipeline is triggered depends on the trigger event you select and the trigger condition you configure in the Code Pipeline console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The event trigger settings for the target pipeline have been selected, and the corresponding pipeline Webhook URL has been copied. For specific actions, please refer to [Code Source Trigger](https://docs.byteplus.com/en/docs/cp/Trigger_from_code_source).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to GitHub, go to the target repository homepage. Select **Settings \> Webhooks \> Add webhook**.

2. Configure the Webhook information as required. Configuration items not mentioned in the table can be configured as needed.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Payload URL |Enter the pipeline Webhook URL provided in the prerequisites. |
   |Content type |Select **application/json**. |
   |Trigger events |We recommend selecting **Send me everything**. Whether the pipeline is triggered is determined by the trigger event you select and the trigger conditions you configure in the Code Pipeline console. |
   |Active |Select **Active**. Otherwise, the Webhook trigger will not function. |
   

3. Click **Add webhook**, then complete the configuration.
