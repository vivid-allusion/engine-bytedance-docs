---
title: "Creating namespaces"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-namespace"
---

A namespace is an abstract group of resources and objects in a cluster. You can create different namespaces in a cluster, and data in different namespaces is isolated from each other.

<span id="HZzbIjkn"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. Click **Cluster** in the left navigation bar.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Namespace**.

5. On the Namespace page, click **Create namespace** or **Create with Yaml**, and then specify the parameters of the namespace.

   * Available parameters when you click **Create namespace**:

      
      |Parameter |Description |
      |---|---|
      |Name |Enter the namespace name. The namespace name must be unique in the same cluster.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Avoid using <code>kube-</code> as a prefix for namespace names, for example, <code>kube-namespace</code>. This prefix is reserved for Kubernetes system namespaces.</div><br> |
      |Label |Enter the labels for the namespace, which correspond to labels in Kubernetes. A label is a key\-value pair used to identify a namespace. It helps Kubernetes quickly search for target namespaces when it is used with the selector. For example, `service.istio.io/canonical-revision:latest`.<br><br>Click **Add new**, and enter the **key** and **value** based on the on\-screen prompts. |
      |Annotation |Enter the annotation of the namespace, which corresponds to the annotation in Kubernetes. It is primarily used to record additional information about application deployment, security policy, and scheduling policy. It is not used to identify or distinguish resources.<br><br>Click **Add annotation**, and enter the **key** and **value** based on the on\-screen prompts. |
      

   * Available parameters when you click **Create with Yaml**:

      
      |Parameters |Description |
      |---|---|
      |Type |The YAML file type. Select **Namespace**, which indicates that the YAML resource type to be created is Namespace. |
      |Yaml |Enter the content of the YAML file based on your business requirements. The `name` field indicates the name of the namespace. |
      

5. After the configuration is complete, click **Confirm**.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation result

After you create the namespace, you can view the created namespace on the Namespace page.
