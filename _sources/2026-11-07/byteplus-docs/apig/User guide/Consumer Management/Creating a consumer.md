---
title: "Creating a consumer"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_a_consumer"
---

The consumer is an abstraction of the object that accesses the API gateway. By using consumers, the gateway can merge one or more objects into a single user identity, which facilitates permission control and user management of the access source. Consumers can be a variety of client applications, mobile applications, web applications, third\-party Services or other systems. This article describes how to create consumers.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An APIG instance has been created. For details refer to [Creating an instance ](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* A gateway can create up to 20 consumers.

* The consumer name cannot be repeated in the same instance.


<span id=".5Yib5bu65raI6LS56ICF"></span>
## Create a consumer


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **consumer management \> consumer list ** .

4. On the consumer page, click **create consumer ** .

5. On the **create consumer ** page, create consumer.

   
   |Parameter |Description |
   |---|---|
   |Instance |Select the instance to which the consumer belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Consumers can only select APIG instances created after 00:00 on January 19, 2024.</div><br> |
   |Consumer name |Custom consumer name to identify the consumer.<br><br><br>* Consumers are instance\-level resources. The consumer name cannot be repeated in the same instance.<br><br>* Please enter 2~ 63 characters.<br><br>* Characters can only contain uppercase and lowercase letters, numbers, and dashes`-`.<br><br>* Cannot be underlined`-`Beginning. |
   |Notes/comments |Configuration of consumer's Notes/comments content, e.g. consumer's purpose, easy to identify later. |
   

6. Click **Confirm** to complete the configuration.
