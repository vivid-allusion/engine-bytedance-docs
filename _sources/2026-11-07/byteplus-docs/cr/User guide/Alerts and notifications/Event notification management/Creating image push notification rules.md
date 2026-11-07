---
title: "Creating image push notification rules"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Create_notification_rules"
---

CR supports sending message notifications, helping you obtain information about the success of image pushes in a timely manner. This topic describes how to create a notification rule for image push events.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This operation applies only to Standard Edition standard instances.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

CR supports sending notifications for image push events in specified instances, namespaces, or OCI artifact repositories. For example, if the effective scope of a rule is all Nginx image tags within namespace A, notifications will be sent when a new or updated image or Chart version is pushed to that Nginx OCI repository via CR.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Standard Edition instances have been created; for instructions, see [Create Standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance) **.** 

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* A maximum of 20 notification rules can be enabled. Any new rules created beyond this limit will be in a disabled state. To enable a new rule, first disable or delete an existing one.

* A notification rule takes effect only after it is created and enabled. The following methods are supported for enabling notification rules.

   * During creation: Select **Notification rules \> Rule state** \> **Enable**.

   * After creation: On the notification rules list page, click **Enable** in the **Actions** column of the target rule to enable the rule.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Event notification**.

4. On the **Event notification** page, click **Create notification rule**.

5. Configure the notification rule parameters.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |Trigger action |Select the event that triggers the notification. In this scenario, select **Push image**. |
      |Name |The custom name of the notification rule. |
      

   * **Effective scope**

      
      |Parameter |Description |
      |---|---|
      |Effective level |The level at which the rule is applied. Options: Instance, Namespace, and OCI artifact repository.<br><br><br>* Instance: The notification rule applies to all namespaces and OCI artifact repositories under the selected instance.<br><br>* Namespace: The notification rule applies to all OCI artifact repositories within the selected namespace.<br><br>* OCI artifact repository: The notification rule applies to the selected OCI repository(ies). |
      |Instance |Select the instance to which the notification rule applies. |
      |Namespace |Select the namespace to which the notification rule applies. |
      |OCI artifact repository |Select the OCI artifact repository to which the notification rule applies. Multiple OCI artifact repositories can be selected. |
      |Artifact repository type |Select the type of artifact to which the rule applies. Current options: ** Image**, **Chart**, and All. |
      |Tier |Select the image or Chart version to which the notification rule applies. Options: All and Regular expression matching. For common version filtering regular expressions, see [regex matching examples](https://docs.byteplus.com/en/docs/cr/Regular_expression_matching_examples?lang=en). |
      

   * **Notification rules**

      
      |Parameter |Description |
      |---|---|
      |Rule state |Specifies whether the notification rule is enabled or disabled. A maximum of 20 notification rules can be enabled. Any new rules created beyond this limit will be in a disabled state. To enable a new rule, first disable or delete an existing one. |
      |Notification method |Currently, only **HTTP(s)**  is supported. |
      |Target URL |The URL that is invoked when the event is triggered. The notification payload is sent to this URL. For example, a webhook URL. |
      |Custom Header |Supports defining custom Header for the request sent to the target URL based on your service. |
      

6. After the configuration is complete, click **Confirm**.


<span id=".5raI5oGv56S65L6L"></span>
## Message example

After a successful push, you will receive a Hook message notification. An example message and parameter descriptions are provided below.

```json
{
  "id": "283154ee-797d-4842-9ce4-****",
  "source": "cr",
  "type": "cr:Tag:Push",
  "specversion": "1.0",
  "time": "2024-02-03T20:02:11Z",
  "volcaccountid": "210013****",
  "volcregion": "ap-southeast-1",
  "data": {
    "image": "enterprise-****.cr.volces.com/event-****/event-****:event-****",
    "registry": "enterprise-****",
    "namespace": "event-****",
    "repository": "event-****",
    "tag": "event-****",
    "digest": "sha256:4e973642bc4933eb9bea99e5b64ddc1bc16a152a4e7038a442bcf2338994****",
    "operator": "paas****@****",
    "type": "Image"
  }
}

```



|Parameter ||Description |
|---|---|---|
|id ||The ID of the push notification message. |
|source ||The source of the pushed message. Fixed value is cr, which indicates CR product. |
|type ||The event that triggers the notification. `cr:Image:Pushed` indicates an image push event. |
|specversion ||The message notification version. This is a fixed parameter and requires no special attention. |
|time ||The time when the notification is sent. |
|volcaccountid ||The ID of the BytePlus root user who creates the message notification. |
|volcregion ||The BytePlus region from which the notification is sent. |
|data |image |The address of the image. |
||registry |The name of the instance where the image resides. |
||namespace |The namespace where the image resides. |
||repository |Name of the OCI artifact. |
||tag |The image tag. |
||digest |The identifier of the image content. |
||operator |The BytePlus root user who creates the message notification. |
||type |The type of pushed OCI artifact.<br><br><br>* `image`: Image.<br><br>* `chart` : Helm Chart. |


<span id=".5q2j5YiZ5Yy56YWN56S65L6L"></span>
##
