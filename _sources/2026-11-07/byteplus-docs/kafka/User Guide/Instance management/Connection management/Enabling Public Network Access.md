---
title: "Enabling Public Network Access"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/enabling-internet-facing"
---

Before accessing Kafka instances over the internet, enable public network access for the instances. If public network access is not enabled when you create an instance, refer to this topic for configuration.

<span id="背景信息"></span>
## Background information

Upon enabling public network access, Message Queue for Kafka assigns public endpoints to instances, facilitating client access to the Kafka instances over the internet. For the public endpoints of Kafka instances, you can specify whether to enable SSL authentication for data links. Currently, the client supports one\-way authentication for server certificates, and data transmission is encrypted, offering higher security compared to standard public network access methods.

<span id="前提条件"></span>
## Before you begin


* Create a Kafka instance and ensure that the instance status is **Running**.

* Before enabling public network access, first create an EIP in the same Region, ensuring the allocated EIP bandwidth exceeds the estimated peak of internet traffic.


<span id="开启公网访问"></span>
## Enabling public network access


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the **Instances** page, click the name of the target instance.

3. In the **Service access** pane under the **Instance Details** tab, click **Enable Public Network Access**.

4. On the **Enable Public Network Access** page, choose the EIP to associate and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no EIPs are available, follow the prompts to apply for a public IP address before association.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once public network access is enabled, the instance status temporarily changes to <strong>In the application network</strong>. Upon successful application, the status reverts to <strong>Running</strong>. Every endpoint offers an address for access over the internet. For example, the <strong>SASL_SSL endpoint</strong> offers an address using the Simple Authentication and Security Layer (SASL) mechanism for access over the internet. You can select an appropriate access method as needed.   </div>
   

<span id="关闭公网访问"></span>
## Disabling public network access

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Upon disabling public networkaccess, the Kafka instance terminates all public endpoints and automatically disassociates elastic IP addresses (EIPs).</div>


* <div data-tips="true" data-tips-type="tip">EIPs disassociated from the Kafka instance remain and continue to incur charges. If they are no longer needed, release the related resources manually.</div>


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. On the **Instances** page, click the name of the target instance.

3. In the **Service access** pane on the **Instance Details** tab, click **Disable Public Network Access**.

4. In the pop\-up dialog box, confirm the EIP you want to disassociate and the related addresses for access over the internet, then click **OK.** 

   Once public network access is disabled, the instance status temporarily changes to **Release the network**. Upon successful disabling, the status reverts to **Running**.
