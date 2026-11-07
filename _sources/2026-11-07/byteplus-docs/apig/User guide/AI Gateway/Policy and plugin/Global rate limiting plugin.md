---
title: "Global rate limiting plugin"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Global_rate_limiting_plugin"
---

The global rate limiting plugin centrally controls all incoming traffic based on preset metrics such as bandwidth thresholds, request rate upper limits, and connection limits. This prevents a single path or user from consuming excessive resources, which may degrade overall performance or make services unavailable. This feature also helps ensure the overall system stability and fair resource allocation. This topic describes how to configure a global rate limiting plugin.

## Prerequisites

* You have created a Redis database for plugin installation and obtained the account and password.

* (Optional) To enable rate limiting based on token count, create an Upstream with the backend service of the **AI model proxy** type. For details on how to create it, see [AI model proxy](https://docs.byteplus.com/en/docs/apig/AI_Multi-Model_Proxy).

## Procedure

### Step 1: Install the plugin

1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the **Instance management** drop\-down list, and click **Plugin Center \> traffic control \> Global rate limiting plugin**.

4. Click **Install plugin**, and on the configuration page, enter the address, port, and login information of the created Redis database.

5. Click **Confirm** to complete the operation.

### Step 2: Create a plugin

1. On the ** Global rate limiting plugin** page, click ** Create plugin**.

2. Configure rate limiting rules.

   > **tip**

   > You can configure multiple rate limiting rules using logical **OR**.

   |Parameter |Description |
   |---|---|
   |Service |Select the service associated with the plugin. |
   |Route |Select the route associated with the plugin. |
   |Rate limiting settings |Configure rate limiting rules based on your business scenario.<br><br><br>* **Rate limiting dimension**: The plugin currently supports rate limiting based on headers only.<br><br>* **Rate limiting target**: The following rate limiting targets are supported.<br><br>   * **Token count**: Supports rate limiting based on token count. Only a backend service Upstream of the ** AI model proxy type ** supports this feature. For details on how to create an Upstream of the AI model proxy type, see [AI model proxy](https://docs.byteplus.com/en/docs/apig/AI_Multi-Model_Proxy).<br><br>   * **Inbound bandwidth rate limit**: Supports bandwidth rate limiting for Upstreams.<br><br>   * **Request count**: Supports request count rate limiting for upstreams. |
   |Header Value |The value of the request header for the rate limiting object. |
   |Rate limit threshold |Configure the maximum number of tokens, inbound bandwidth, or requests allowed for the current instance within one interval. Requests that exceed the threshold are rejected. |

4. Click **Confirm** to finish.

## View settings

After configuration, you can view the configured plugin in the plugin list. If the plugin status is **Enabled**, the plugin has taken effect.
