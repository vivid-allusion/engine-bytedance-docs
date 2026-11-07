---
title: "Best practices for RabbitMQ policy"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/RabbitMQ_Policy_best_practices"
---

This topic describes how to use RabbitMQ Policy and provides usage examples.

<span id="c15541db"></span>
## Solution overview

A Policy in RabbitMQ is a mechanism that makes it easy to automate the application of specific configurations or behaviors to queues, exchanges, and more. Policy typically uses regular expressions to select target objects and then applies configuration parameters to them. Thereby enabling automated large\-scale cluster configuration management.

<span id="e253d611"></span>
## Add Policy


1. Log in to the open\-source RabbitMQ console.

2. Click the **Admin** tab, click **Add / update a policy**, and add a RabbitMQ Policy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17f2740969df4ccdb78b3be71f8618ed~tplv-goo7wpa0wc-image.image) </span>

   Policy parameter description as follows:

   
   |Parameters |Description |
   |---|---|
   |Name |Policy name. |
   |Pattern |The matching pattern defined by a regular expression. |
   |Apply to |Policy scope: supports **Exchanges** or **Queues**. |
   |Priority |Strategy priority: the higher the number, the higher the priority. |
   |Definition |Strategy parameters.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In the RabbitMQ Web UI console, the bottom row of the Definition section is always a blank parameter row.</div><br> |
   


<span id="55c7b4a8"></span>
## Example 1: Delete all Queue using Policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If a queue has production and consumption activities, the queue will not be deleted even if a Policy is configured.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1b42ff666cf4f30b0a1e3a955506539~tplv-goo7wpa0wc-image.image) </span>

Example parameters are as follows:


|**Parameters** |**Description** |
|---|---|
|Virtual host |The effective scope of the vhost to which the policy is applied (this parameter is displayed when there are multiple vhosts). |
|Name |Policy name, custom settings. |
|Pattern | **.** \* (means matching all queues). |
|Apply to |Select **Queues**. |
|Priority |Strategy priority, custom settings. |
|Definition |The **expires** parameter of type **Number**, possible values are **1**, indicating that the queue expires after 1 ms. |


<span id="74b1bc34"></span>
## Example 2: Configure the default image queue via Policy

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is not recommended to enable mirroring in production environments, as this may introduce multiple stability risks. This function has been deprecated in the latest community version.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50ce932e5ffb4388814432a60b2ef6e2~tplv-goo7wpa0wc-image.image) </span>

The example parameters are as follows:


|**Parameters** |**Description** |
|---|---|
|Virtual host |Effective scope of the vhost to which the policy applies (this parameter is displayed when multiple vhosts exist). |
|Name |Policy name, custom settings. |
|Pattern | **.** \* (matches all queues). |
|Apply to |Select **Queues**. |
|Priority |The strategy priority, custom settings. |
|Definition |You can configure according to the following example:<br><br><br>* The **ha\-mode** parameter of type **String**, with a value of **all.** <br><br>* (Optional) If you only want to configure images on a fixed number of nodes, you can add the following parameters:<br><br>   * The **Number** type **ha\-params** parameter, the value is **2**。<br><br>   * The **String** type **ha\-sync\-mode** parameter, with a value of **automatic**. |
