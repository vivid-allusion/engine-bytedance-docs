---
title: "No charge during downtime"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/No_charge_during_downtime"
---

Byteplus E\-MapReduce provides a no\-charge when stopped feature for clusters, currently available only for clusters billed on a pay\-as\-you\-go basis. When you stop a pay\-as\-you\-go cluster and select the "no\-charge when stopped" option, some resources are reclaimed and billing for those resources stops once the cluster is stopped, helping to reduce related expenses and save on usage costs.

This feature is currently in invite\-only testing. If you would like to try it, please contact your account manager.

<span id="6961d403"></span>
## **Limitations**


* This feature is available to accounts on the whitelist. For accounts with whitelist access, the platform provides the capability to not charge for pay\-as\-you\-go EMR clusters when they are stopped.

* The no charge during shutdown feature can only be enabled when shutting down via Byteplus Console or API operations.

* After shutdown, ECS instances in the cluster will stop running, and billing for instance resources such as CPU and memory will cease. However, to prevent data loss, the attached cloud disks, public IP addresses, and bandwidth (in fixed bandwidth mode) will be retained and continue to incur charges.

* Clusters using the subscription payment model and clusters equipped with local disks do not currently support the stop billing exemption feature.

* The no\-charge shutdown logic applies only when the cluster is shut down through the console or by calling the API. Executing shutdown commands such as `shutdown` within an ECS instance does not trigger the no\-charge shutdown logic.


<span id="e4857839"></span>
## Note


* After you enable the stop without charge feature for a pay\-as\-you\-go cluster, the cluster will be in the **stopped** state.

* Because computing resources are reclaimed, a stopped cluster may fail to start if there is insufficient ECS inventory. If a failure occurs during the process of starting the cluster, please try again or wait for some time before trying again. If cluster startup fails, the cluster remains in a stopped and non\-billable state.

* The private IP address and the Elastic Public IP address bound before the instance is stopped remain unchanged after the instance is restarted.

* If your Byteplus account remains overdue for more than two hours, the public IP resources attached to instances with the Stop Charging When Shut Down feature enabled will become unavailable.

* If payment is overdue for more than 15 days, billing for cloud disks and public IPs attached to instances with the stop billing on shutdown feature enabled will stop, and the purchased instance, cloud disk, and public IP resources will be forcibly released.


<span id="b093e7ea"></span>
## Procedure


1. Log in to the EMR console, and go to the cluster list page.

2. Select the target cluster and click "No charge when stopped" in the operations column.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4ec290bbf6c45c4b780c1a091368621~tplv-goo7wpa0wc-image.image) </span>


3. I acknowledge the operational risks and confirm that I want to stop.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/500cb855163345c180ebf65c82d6b40f~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Caution: After the cluster is stopped, some ECS resources will be reclaimed and charges for them will cease. However, services under the cluster will become unavailable, and tasks that are currently running will fail. Please operate with caution.</div>
