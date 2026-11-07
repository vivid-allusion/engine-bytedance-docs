---
title: "Managing namespaces"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-namespaces"
---

After you create a namespace, you can view, update, or delete the created namespace on the namespace management page based on your business requirements. This topic describes how to manage namespaces.

<span id=".5p-l55yL5ZG95ZCN56m66Ze06K-m5oOF"></span>
## Viewing namespace details


1. Log in to the [VKE console](https://console.byteplus.com/vke).. In the left navigation bar, click **Cluster**.

2. On the Cluster page, click the name of the target cluster.

3. In the left navigation bar of the cluster management page, click **Namespace**.

4. On the **Namespace** page, view the system default namespaces and user\-defined namespaces of the cluster. You can view the following basic information about the namespaces.

   
   |Parameter |Description |
   |---|---|
   |Name |The namespace name. You can perform fuzzy searches on namespaces by name. |
   |Label |The labels of the namespace to help other resources identify the namespace. |
   |Annotation |The annotation of the namespace to help other resources identify the namespace. You can search for namespaces by annotation in the following search logic:<br><br><br>* When you search for namespaces by annotation, you can add up to 10 key\-value pairs for precise searching.<br><br>* When multiple key\-value pairs are used in a search, pairs with the same key are in the logical OR relationship and pairs with different keys are in the logical AND relationship. |
   |Status |The running status of the namespace. Valid values:<br><br><br>* **Active**: The namespace is running.<br><br>* **Terminating**: The namespace is being deleted. |
   |ResourceQuota |The ResourceQuota of the namespace. For a detailed description, see [Setting ResourceQuota](https://docs.byteplus.com/en/docs/vke/Setting-ResourceQuotas). |
   |LimitRange |The LimitRange of the namespace. For a detailed description, see [Setting LimitRange](https://docs.byteplus.com/en/docs/vke/Setting-LimitRanges). |
   |Creation time |The time when the namespace was created. |
   |Actions |You can modify the configurations of the namespace or delete the namespace. For related operation instructions, see the following sections of this topic.<br><br><br>* **Update**: Update the labels or description of the namespace in the console.<br><br>* **Edit Yaml**: Update the configurations of the namespace by editing the YAML file of the namespace. You cannot update the name of the namespace.<br><br>* **Set ResourceQuota**: Set limits on the total quantity of available resources, the quantity of resources of each type, and the quantity of resources available to pods in the namespace. For a detailed description, see [Setting ResourceQuota](https://docs.byteplus.com/en/docs/vke/Setting-ResourceQuotas).<br><br>* **Set LimitRange**: Set limits on resource usage for a single pod, container, and PVC in the namespace. For a detailed description, see [Setting LimitRange](https://docs.byteplus.com/en/docs/vke/Setting-LimitRanges).<br><br>* **Delete**: Delete the namespace. |
   


<span id=".5pu05paw5ZG95ZCN56m66Ze0"></span>
## Updating a namespace

You can update the configurations of a namespace by using the console or a YAML file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You cannot update the namespace name by using either method.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).. In the left navigation bar, click **Cluster**.

2. On the Cluster page, click the name of the target cluster.

3. In the left navigation bar of the cluster management page, click **Namespace**.

4. On the **Namespace** page, find the target namespace and click **Update** or **Edit Yaml** in the **Actions** column.

5. Update namespace information and then click **Confirm**.

   
   |Parameter |Description |
   |---|---|
   |Name |The namespace name. You cannot update the name. |
   |Label |The label corresponding to that in Kubernetes. A label is a key\-value pair used to identify a namespace. It helps Kubernetes quickly find target namespaces when used with a selector. For example, `service.istio.io/canonical-revision:latest`.<br><br>You can update the existing namespace labels. You can also click **Add new** and enter the **key** and **value** based on the on\-screen prompts. |
   |Annotation |The annotation that corresponds to the annotation in Kubernetes. It is primarily used to record additional information about application deployment, security policy, and scheduling policy. It is not used to identify or distinguish resources.<br><br>You can update the existing namespace annotations. You can also click **Add annotation** and enter the **key** and **value** based on the on\-screen prompts. |
   


<span id=".5Yig6Zmk5ZG95ZCN56m66Ze0"></span>
## Deleting a namespace

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">If you delete a namespace, all resources in the namespace are also deleted. This operation is irreversible. Proceed with caution.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).. In the left navigation bar, click **Cluster**.

2. On the Cluster page, click the name of the target cluster.

3. In the left navigation bar of the cluster management page, click **Namespace**.

4. On the **Namespace** page, find the target namespace and click **Delete** in the **Actions** column.

5. In the message that appears, click **Delete** to delete the namespace.
