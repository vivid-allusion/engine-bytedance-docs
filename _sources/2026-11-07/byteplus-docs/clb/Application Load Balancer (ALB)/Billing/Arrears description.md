---
title: "Arrears description"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Overdue-payments"
---

When your account balance falls below zero, the account enters an overdue state. You can refer to the [Account overview](https://docs.byteplus.com/en/docs/6269/100429) to view overdue details. Once an account becomes overdue, it may lead to the shutdown and eventual reclamation of Application Load Balancer (ALB) instances, affecting their operation and configuration management.

<span id=".5qyg6LS55b2x5ZON"></span>
## Overdue Impact

After an account becomes overdue, the impacts and operational restrictions on ALB resources over different periods are outlined in the table below.


|**Overdue payment duration** |**Duration ≤ 15 days** |**15 days < Duration ≤ 30 days** |**Duration \> 30 days** |
|---|---|---|---|
|Instance status |* Instances run as expected.<br><br>* If you top up your account and complete the overdue payment now, your workloads are not affected. |* Instances stop, but instance resources are retained.<br><br>* ALB stops serving you. If you top up your account and complete the overdue payment now, your instances restore and the system continues to bill the resources of the instances. |* The system reclaims the instance resources and the elastic IP addresses (EIPs) associated with the instances.<br><br>* The system deletes the data and configurations of your instances. The data and configurations cannot be restored. |
|Billing status |Normal billing |Billing stopped |Billing stopped |
|Operational restrictions |You cannot create instances or modify the public network settings of existing instances. |The following operations are not supported:<br><br><br>* Operations on instances: Creating instances, associating elastic IP addresses with instances, and modifying public network settings.<br><br>* Operations on listeners: Adding listeners and modifying the information about existing listeners.<br><br>* Operations on the server groups associated with instances: Deleting and editing server groups.<br><br>   * Operations of editing a server group include adding back\-end servers to and deleting back\-end servers from a server group, modifying the weight of back\-end servers, and modifying health check settings and other information.<br><br>* Monitoring operations: The existing monitoring and alerting services stop, and only the data stored before the instances stop is retained.<br><br>* Logging operations: related to access logging and health check logging. The configured access logging service and health check logging services stop, and only the data stored before the instances stop is retained.<br><br>* Operations on the custom configurations associated with instances: Deleting and modifying custom configurations.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can view health check logs and remove log topics within 24 hours after a payment becomes overdue. If you do not settle your overdue payment within 24 hours, you can no longer view the health check logs.</div><br> |Only the following operations are supported:<br><br><br>* Operations on server groups that are not associated with instances: Creating, deleting, and editing server groups.<br><br>   * Operations of editing a server group include adding back\-end servers to and deleting back\-end servers from a server group, modifying the weight of back\-end servers, and modifying health check settings and other information.<br><br>* Operations on certificates: Uploading, querying, and deleting certificates.<br><br>* Operations on access control lists: Creating, querying, modifying, and deleting access control lists, and adding IP entries to and deleting IP entries from access control lists.<br><br>* Operations on health check templates: Creating, querying, deleting, and modifying existing templates. |
