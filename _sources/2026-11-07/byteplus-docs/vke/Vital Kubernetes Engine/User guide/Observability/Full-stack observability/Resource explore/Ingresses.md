---
title: "Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Ingress"
---

Ingress monitoring provides monitoring information for Ingress resources in clusters, including the resource list and resource details. This topic describes how to view the list of Ingresses and their details.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* Full\-stack observability has been enabled. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).


<span id=".6LWE5rqQ5YiX6KGo"></span>
## Resource list


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Resource explorer**.


<span id=".5p-l55yL6LWE5rqQ5YiX6KGo"></span>
### Viewing the resource list

In the **Resource type** panel, select **Ingress** to view the Ingress list. The list displays the basic information of each Ingress, including the Ingress name, namespace, type, VIP, listener protocol, and backend service.

In the Ingress list, you can click the Ingress name to go to the Ingress details page.

<span id=".6LWE5rqQ562b6YCJ"></span>
### Filtering resources

You can filter Ingresses by namespace and Ingress in the Ingress list.


1. Select the information to be retrieved from the **Namespace** and **Ingress** drop\-down lists.

2. Click **Add label/annotation** to configure the labels or annotations for Ingress.

   
   |Parameters |Description |
   |---|---|
   |Type |Select Label or Annotation to filter Ingresses. |
   |Name |Enter the name of the label or annotation in string format. |
   |Operator |Configure the operator. Valid values:<br><br><br>* **Include**: Indicates that the label and annotation contain the specified value.<br><br>* **Not equal to**: Indicates that the label and annotation do not contain the specified value. |
   |Value |Specify the value of the label or the annotation in string format. You can enter multiple values by pressing the spacebar. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add multiple labels or annotations for retrieval.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Multiple values are in the <strong>AND</strong> relationship, which means the Ingress must contain all values.   </div>
   

3. Click **Search** to retrieve the Ingress.


<span id=".6LWE5rqQ6IGa5ZCI"></span>
### Aggregating resources

You can aggregate Ingresses by **Namespace** in the Ingress list. After aggregation, Ingresses are displayed by aggregation dimension.


1. Select the target aggregation dimension from the **Aggregation dimension** drop\-down list.

2. Click **Search** to aggregate Ingresses.


&nbsp;
