---
title: "Create a Logstash instance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance"
---

Creating an instance is the first step to use Logstash. This topic describes how to create a Logstash instance.

<span id="BMGVT1bf"></span>
## Prerequisites


* Before using Cloud Search service, register a Volcengine account and complete  and enterprise verification.

* The first time you create an instance in the console, you must complete cross\-service authorization to allow Cloud Search service to access other cloud product resources. For authorization details, see [Cross-service authorization](https://docs.byteplus.com/en/docs/cloudsearch/cross-service-authorization).


<span id="KubOK9ez"></span>
## Procedure


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the project and region where you want to create an instance.

3. In the left navigation, select **Data processing** \> **Logstash**.

4. On the **Logstash** page, click **Create instance**.

5. On the **Create Logstash instance** page, configure the following parameters, then click **Confirm order**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Billing type |Supports **pay\-as\-you\-go** and **subscription** billing methods. Please choose the appropriate method based on your needs.<br><br><br>* Pay\-as\-you\-go: postpaid mode, can be started or stopped anytime, billed by actual usage duration.<br><br>* Subscription: prepaid mode, offers better discounts than pay\-as\-you\-go; recommended for long\-term users.<br><br><br>You can first create a pay\-as\-you\-go instance, then switch to subscription after confirming the instance meets your requirements. |
   |Availability zone |Select the availability zone based on your requirements. |
   |Name |Set the instance name. Naming rules are as follows:<br><br><br>   * Cannot start with a number or a hyphen (\-).<br><br>   * Length must be between 1 and 128 characters.<br><br>   * Contain letters, digits, underscores (_), and hyphens (\-). |
   |Version |Currently only **8.17.3** is supported. Logstash 8.17.3 is a newer open\-source version that supports TLS security protocol and offers more efficient pipeline processing. BytePlus has adapted Elasticsearch input/output plugins to ensure compatibility with all versions of Cloud Search, enabling seamless data migration. |
   |Node specification |Select the appropriate node specification according to your requirements. |
   |Storage type |Supports **ESSD\-FlexPL**, **ESSD\-PL0**, and **TSSD\-TL0**. |
   |Storage specifications |Please choose the appropriate storage capacity based on your needs. Value range: 10~15000 GiB. |
   |Number of nodes |Select the appropriate number of nodes according to your requirements. Valid values: 1~20. |
   |Private network |Select the target Virtual Private Cloud from the dropdown list. You can also click **Create Virtual Private Cloud** on the right to create a new Virtual Private Cloud. For detailed instructions, see [Create Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).<br><br><br>* If accessing the Logstash instance through ECS, select the same Virtual Private Cloud as ECS.<br><br>* Once the Logstash instance is created, the Virtual Private Cloud cannot be changed. |
   |Subnet |Select the subnet available within the private network. You can also click **Create subnet** on the right to create a new subnet. For detailed instructions, see [Create a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Affiliated project |The project affiliated with Logstash. To switch, modify it from the top navigation bar. |
   |Tag |(Optional) Add tags to the Logstash instance. |
   |Delete protection |Select whether to enable delete protection. It is disabled by default. Once enabled, the Logstash instance cannot be deleted directly. You must disable delete protection before deleting the instance. |
   

6. Complete the following steps according to the selected billing type.

   * If you select **Pay\-as\-you\-go**: on the order confirmation page, review the order details, read and check the **Database product and service terms**, then click **Buy now**.

   * If you select **Subscription**:

      1. On the order confirmation page, review the order details, read and check the **Database product and service terms**, then click **Buy now**.

      2. On the **Confirm order information** page, review the order details again, then click **Next**.

      3. On the **Submit payment information** page, confirm the payment details and select a payment method. Click **Pay**, then complete the payment following the prompts to finish creating the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When confirming the order, individual users must also check <strong>Explanation of uUnsubscription or change fees</strong>. To use an enterprise account, complete enterprise authentication.   </div>
