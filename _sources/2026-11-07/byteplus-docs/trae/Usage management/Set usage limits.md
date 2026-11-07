---
title: "Set usage limits"
product: "TRAE"
product_code: "trae"
source: "https://docs.byteplus.com/en/docs/trae/set-usage-limits"
---

You can set usage limits for TRAE built\-in models and enterprise built\-in models. When actual usage reaches the set limits, the system restricts the enterprise or members from continuing to use AI features or models. Usage limit settings can be modified dynamically.

<span id="c7c5326d"></span>
## Usage limit types

TRAE Enterprise supports configuring the following three types of usagelimit:


* **Enterprise overall limit**: When the cumulative usage of all members in the enterprise reaches the usage limit, all members will be unable to continue using AI features. If a model\-level usage limit is set, once the limit is reached, all members will be unable to continue using the corresponding model.

* **Per capita limit**: When the cumulative usage of an individual member reaches the usage limit, that member will be unable to continue using AI features. If a model\-level usage limit is set, once the limit is reached, that member will be unable to continue using the corresponding model.

* **Member\-specific limit**: When the excess usage of the specified member reaches the limit, that member will be unable to continue using AI features.


<span id="4683f4bf"></span>
## Set usage limits for TRAE built\-in models

You can set a default excess usage limit for TRAE built\-in models. During the current billing cycle, any session usage that exceeds the basic quota—including usage from resource packages and pay\-as\-you\-go usage—is referred to as "excess usage." Usage for TRAE built\-in models is calculated in US dollars (USD).

<span id="ecc18dfb"></span>
### Before you begin

Ensure that pay\-as\-you\-go service has been enabled. For how to do this, refer to [Enable pay-as-you-go billing](https://docs.byteplus.com/docs/trae/enable-pay-as-you-go-billing).

<span id="618dd8de"></span>
### Procedure


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Management** \> **Usage Management** \> **Usage Dashboard**.

3. Select **TRAE Built\-in Model**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/94459ff242de496cab09b37d0ff1f3c3) </span>

4. In the lower\-right corner of the **Excess Usage** card, click **Adjust the limit**.

   The **Adjust global quota** popup appears.

5. Set a total\-usage limit for all models or model\-level usage limits as needed:

   * **Set a total\-usage limit for all models (default)** 

      1. Set an enterprise overall limit and a per capita limit.

      2. Click the **Save** button.

   * **Set model\-level usage limits**

      1. Click **Configure a single model quota** at the bottom of the usage limit list.

      2. In the model\-level usage limit setup list, set a separate enterprise overall limit and a per capita limit for each model.

      3. Click the **Save** button.


<span id="70f981ff"></span>
## Set usage limits for enterprise built\-in models

You can set a default model\-level usage limit individually for each enterprise built\-in model. Usage for enterprise built\-in models is calculated by tokens.

<span id="2c3c8ee9"></span>
### Prerequisites

To set token usage limits for enterprise built\-in models, ensure that the API return format of the model provider complies with the Chat Completions protocol, and that the response meets any of the following required formats:


<columns>
<columnsItem zoneid="LT5fT6Ulh3">

```JSON
{
....
"usage": {
    "completion_tokens": 0,
    "prompt_tokens": 0,
    "prompt_cache_hit_tokens": 0,
    "prompt_cache_miss_tokens": 0,
    "total_tokens": 0,
    "completion_tokens_details": {
      "reasoning_tokens": 0
    }
...
}
```


</columnsItem>
<columnsItem zoneid="hhgmB1NbES">

```JSON
{
....
    "usage": {
        "input_tokens": 0,
        "output_tokens": 0
    }
...    
}
```




</columnsItem>
</columns>


<span id="8d88ec21"></span>
### Procedure


1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Management** \> **Usage Management** \> **Usage Dashboard**.

3. Select **Enterprise Built\-in Models**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/37d671eddb29442c86a74f9d6a6b7ffc) </span>

4. Click **Adjust the limit** in the lower\-right corner.

5. In the **Enterprise built\-in model quota management** popup, set a separate enterprise overall limit and a per capita limit for each model.

6. Click the **Save** button.


<span id="4ae3ff1f"></span>
## Set usage limits individually for members

You can configure individual excess usage limits for specified members. Individual usage limits for members are calculated in US dollars (USD).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Limits individually set for members take precedence and override global limits.</div>



1. Log in to the [TRAE Enterprise Console](https://console.enterprise.trae.ai/).

2. Go to **Enterprise Management** \> **Usage Management** \> **Usage Dashboard**.

3. Select **TRAE Built\-in Model**.

4. In the **Member usage** list, find the member who needs an individual excess usage limit, then click **Modify quota** in the **Actions** column. 

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/33639d2e1b474066b0dc7981d55be9f3) </span>

5. In the **Designated member quota modification** popup, set an excess usage limit for the member, then click the **Save** button.
