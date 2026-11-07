---
title: "Add Service"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Add_Service"
---

Add a ClusterIP type Service for the application to enable other Kubernetes applications within this cluster to access the current application. This article explains how to add the Service.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A managed application has been created and deployed, and the application must be deployed in a Vital Kubernetes Engine (VKE) cluster. For specific operations, refer to [Create and deploy managed applications (JAR / WAR)](https://docs.byteplus.com/en/docs/cp/Create_and_deploy_managed_apps_JAR_WAR).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page.

   1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the name of the target workspace to enter that workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

2. On the application management page, select the target hosted application, click the application card, and go to the Basic Information tab for the current application.

3. Switch to the application orchestration tab, and in the access method settings section, select **Service \> Add Service**.

4. In the Add Service dialog box, set the Service parameters.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Service name |A custom service name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Service names must be unique within the namespace of the deployed cluster.</div><br> |
   |Service type |This scenario is **intra\-cluster access (ClusterIP)** , which means that the service can be accessed by other applications within the cluster. |
   |Port mapping |Configure port mapping rules. Support configuration of multiple port mappings.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple port mappings are commonly used in scenarios where an application defines multiple ports to distinguish between different features. For example: one port is used for business access, and another port is used for debugging.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding multiple port mappings, duplicate ports are not allowed.</div><br><br><br>* Select a communication protocol: **TCP** or **UDP** are supported.<br><br>* Port: Set the port that the process listens on, usually defined by the program. Here, the service port is the same as the container port. |
   

5. Click **Confirm**. The Service is being created.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Supports configuring multiple Services for an application as needed.</div>


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. View the Service port mapping in the table: `<ClusterIP>:<Port number>`.

2. Manage your cluster with Kubectl. For specific operations, refer to [Connect to cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

3. Log in to any instance of this cluster and verify whether the application can be successfully accessed via `<ClusterIP>:<Port number>`.


```shell
#   Log in to any instance
kubectl exec -ti <your-pod-name> -n <your-namespace> -- /bin/sh

# Take a web application as an example: use the curl command to verify whether the application is accessible; if everything works normally, it will return the content of the application's homepage.
curl 172.XX.XX.XX:8080
```


<span id=".55u45YWz5pON5L2c"></span>
## Related Operations

For an existing Service, you can modify port mapping information and delete the Service.


|Feature |Descriptions |
|---|---|
|Modify a service |Select the target Service. In the **Actions** column, click **edit** to modify the relevant information. |
|Delete service |Select the target Service. In the **Actions** column, click **Delete** to delete the current Service.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><div data-tips="true" data-tips-type="danger">After you delete the Service, other applications in the cluster will no longer be able to access your application through the current service port. Proceed with caution!</div><br> |
