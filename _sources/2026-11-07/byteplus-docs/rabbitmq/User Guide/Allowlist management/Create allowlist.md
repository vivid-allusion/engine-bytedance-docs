---
title: "Create allowlist"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Create_allowlist"
---

After you create an allowlist and associate it with the RabbitMQ instance, only the IP addresses or ranges configured in the allowlist can access the instance. This topic describes the steps to create an allowlist.

<span id="AVjDvIXX"></span>
## Note


* Each BytePlus account can create up to 100 allowlists for each region.

* Each allowlist can contain up to 300 IP addresses and CIDR\-formatted IP address ranges.


<span id="F0U6miIk"></span>
## Background information 

After you associate an allowlist with the RabbitMQ instance, only the IP addresses and ranges configured in the allowlist can access the Message Queue for RabbitMQ instance. For security, create an allowlist and add your client IP address or range to the RabbitMQ instance allowlist. We recommend regularly maintaining and managing your allowlist to improve access security for your RabbitMQ instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a RabbitMQ instance has never been associated with any allowlist since its creation, all IP addresses are allowed to access the instance. Once an allowlist is associated with the instance, only the IP addresses in the allowlist can access it; after disassociating all allowlists, no IP address can access the instance.</div>


<span id="iKORnJQJ"></span>
## Operation steps


1. Log in to [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq/).

2. Select the region of the instance from the top menu bar.

3. In the left navigation bar, click **Allowlist**.

4. In the upper left corner of the **Allowlist** page, click **Create allowlist**.

5. Fill in the allowlist configuration.

   
   |**Parameters** |**Description** |
   |---|---|
   |Allowlist name |Allowlist name. Must meet the following requirements:<br><br><br>* Can not start with a number or hyphen (\-).<br><br>* Length must be between 1 and 128 characters.<br><br>* Can only include Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The allowlist name must not be the same as any existing name in the current region. |
   |Description |A brief description of the allowlist. The total length can not exceed 200 characters. |
   |IP address |Specify the IP addresses or IP ranges to be added to the allowlist. Only IP addresses or ranges configured in the allowlist can access Message Queue for RabbitMQ instances.<br><br><br>* You can configure up to 300 IP addresses or CIDR\-format IP ranges in each allowlist. Separate multiple addresses with a comma, space, or line break (English or Chinese).<br><br>* Duplicate IP addresses are not allowed in the allowlist. |
   

6. Click **Create**.


<span id="3KZKaNmk"></span>
## Next steps

After successfully creating the allowlist, you can associate instances with the allowlist. See [Associate instances with the allowlist](https://docs.byteplus.com/en/docs/rabbitmq/Associate_instances_with_the_allowlist).
