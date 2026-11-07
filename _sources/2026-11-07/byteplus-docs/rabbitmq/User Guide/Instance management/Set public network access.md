---
title: "Set public network access"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access"
---

Before accessing the RabbitMQ instance via the public network, you must enable public network access function of the instance. This section describes the steps to enable and disable public network access.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The RabbitMQ instance has been successfully created, and its status is **Running**.

* Before enabling public network access, create an EIP in the same region as the RabbitMQ instance. It is recommended that the EIP bandwidth limit exceeds the estimated peak public network traffic. For detailed operations, see [Apply for EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Message Queue for RabbitMQ supports enabling public network access. Once enabled, you can access the RabbitMQ instance via the public network. If public network access was not enabled when creating the instance, please refer to this section to configure it.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When building the connection between client and instance, SSL authentication is required. Enabling public network access automatically enables SSL. After enabling SSL, data is transmitted encrypted and higher security is provided.</div>


* <div data-tips="true" data-tips-type="tip">SSL\-encrypted transmission is only supported in public network environments. Disabling public network access automatically disables SSL authentication.</div>



<span id=".5byA5ZCv5YWs572R6K6_6Zeu"></span>
## Enable public network access


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq/).

2. On the **Instances** page, click the target instance name.

3. On the **Instance information** page, in the **Service access** section, click **Enable public network access**.

4. On the **Enable public network access** page, select an EIP and click **OK**.

   If no EIP is available, apply for a public IP address as prompted, then bind it again.

   After enabling public network access, each access point will provide a public network access address. For example, the \*\*Web UI Access Point (public network)\*\* is the RabbitMQ instance's Web UI public access address. You can choose the appropriate method to connect based on your business needs.


<span id=".5YWz6Zet5YWs572R6K6_6Zeu"></span>
## Disable public network access

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After disabling public network access, RabbitMQ will close all public network access points and automatically unbind the Elastic IP (EIP).</div>


* <div data-tips="true" data-tips-type="tip">EIPs unbound from the RabbitMQ instance will be retained and continue to incur charges. Release the related resources if no longer needed.</div>


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq/).

2. On the **Instances** page, click the target instance name.

3. On the **Instance information** page, in the **Service access** section, click **Disable public network access**.

4. Confirm the EIP and related public access addresses to unbind in the pop\-up dialog, then click **Close**.


<span id=".5YW25LuW5pON5L2c"></span>
## Other operations

After enabling or disabling public network access, you can check the execution status of related tasks, including status, start time, and end time, on the **Task management** tab.<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bfd0aa4565b303a8357f606f383d1fc5.png) </span>
