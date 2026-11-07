---
title: "Resource explorer"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Resource-explorer"
---

Resource Explorer lets you view, deploy, and manage Kubernetes resources in a specific cluster, and provides visual management for Custom Resource Definition (CRD) resources. This topic primarily describes how to create custom resources and how to manage and view all API groups and CRD resources in a cluster.

<span id=".5Yib5bu66Ieq5a6a5LmJ6LWE5rqQ"></span>
## Creating custom resources


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the cluster that you want to configure.

4. On the cluster management page, click **Workload** \> **Resource Explorer** in the left navigation bar.

5. Click **Create with Yaml**.

   
   |Parameter |Description |
   |---|---|
   |Type |Select a resource type from the drop\-down list. |
   |Yaml |Enter the content of the YAML file. You can upload a `YAML` file. The newly uploaded YAML file will overwrite the existing YAML content. The file can be up to 1.0 MiB in size. |
   

6. Click **Confirm** to create **custom resources**.


<span id=".5p-l55yL6LWE5rqQ5a-56LGh"></span>
## Viewing resource objects


1. On the **Resource Explorer** page, select **CRD** or **API Group** from the Category list to view the resources of the selected category.

2. Click the name of the CRD resource or API group that you want to view.

3. Go to the details page of the CRD resource or API group to view details of these objects: custom CRD, system CRD, custom API group, and native API group objects.


<span id=".566h55CG6Ieq5a6a5LmJ6LWE5rqQ"></span>
## Managing custom resources

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You can manage only custom API groups and cannot manage native API groups.</div>


* <div data-tips="true" data-tips-type="warning">Proceed with caution when you edit system\-generated CRD resource objects.</div>


1. On the **Resource Explorer** page, select **CRD** or **API Group** from the Category list to view the resources of the selected category.

2. Click the name of the custom resource you want to manage, locate its target object, then click `···` in the **Actions** column to manage it.

   
   |Parameter |Description |
   |---|---|
   |Edit Yaml |Modify CRD resource objects or API group resource objects by editing YAML content. |
   |Delete |Delete the selected CRD resource object or API group resource object. |
   


<span id="jE5m6ZDE"></span>
## Appendix

For more information about CRD, CR, and API Group in native Kubernetes, see the following topics:


* [Kubernetes CRD](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/)

* [Kubernetes API Group](https://kubernetes.io/docs/reference/using-api/#api-groups)

* [Kubernetes CR](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
