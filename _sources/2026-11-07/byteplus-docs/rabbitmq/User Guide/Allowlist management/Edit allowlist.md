---
title: "Edit allowlist"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Edit_allowlist"
---

You can modify allowlist names, IP addresses, and other configurations based on business needs. This topic describes the steps to edit the allowlist in the console.

<span id="gmM9hLbJ"></span>
## Note

Each allowlist can contain up to 300 IP addresses or CIDR\-format IP address ranges.

<span id="rvi8uTeY"></span>
## Operation steps


1. Log in to [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region of the instance from the top menu bar.

3. In the left navigation bar, click **Allowlist**.

4. Locate the specified allowlist on the **Allowlist** page, and click the allowlist name.

5. Click **Edit** in the **allowlist information** section.

6. Reset the basic information of the allowlist.

   
   |**Parameters** |**Description** |
   |---|---|
   |Allowlist name |Allowlist name. Must meet the following requirements:<br><br><br>* Cannot start with a number or hyphen (\-).<br><br>* Length must be between 1 and 32 characters.<br><br>* Can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-). |
   |Description |A brief description of the allowlist. The total length can not exceed 200 characters. |
   |IP address |IP address or IP range to be added to the allowlist. Only IP addresses and address ranges configured in the allowlist can access the Message Queue for RabbitMQ instance.<br><br><br>* You can set up to 300 IP addresses or CIDR\-format IP address ranges in each allowlist. Separate multiple addresses with either English or Chinese commas, spaces, or line breaks.<br><br>* Duplicate IP addresses are not allowed in the allowlist. |
   

7. Click **Create**.


<span id="T8XZS8fQ"></span>
## Related actions

Besides modifying the allowlist name, description, and IP address, you can also associate or disassociate instances with the allowlist. For details, see:


* [Associate instances with the allowlist](https://docs.byteplus.com/en/docs/rabbitmq/Associate_instances_with_the_allowlist)

* [disassociate instances from the allowlist](https://docs.byteplus.com/en/docs/rabbitmq/Disassociate_instances_from_the_allowlist)
