---
title: "K8s YAML application orchestration"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/K8s_YAML_application_orchestration"
---

After you create or import a K8s YAML application, you need to edit the application's YAML configuration file to ensure that the application to be deployed meets expectations. This article introduces operations related to application orchestration.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information


* The system provides template YAML files for the Deployment, Service, and Configmap resources. Here, commonly used parameter values are represented by placeholders, with default values pre\-filled to facilitate rapid application orchestration.

* A K8s YAML application can contain up to 20 resources. Among them, different types of resources follow the deployment order as follows:

   Namespace \> NetworkPolicy \> ResourceQuota \> LimitRange \> PodSecurityPolicy \> PodDisruptionBudget \> ServiceAccount \> Secret \> SecretList \> ConfigMap \> StorageClass \> PersistentVolume \> PersistentVolumeClaim \> CustomResourceDefinition \> ClusterRole \> ClusterRoleList \> ClusterRoleBinding \> ClusterRoleBindingList \> Role \> RoleList \> RoleBinding \> RoleBindingList \> Service \> DaemonSet \> Pod \> ReplicationController \> ReplicaSet \> Deployment \> HorizontalPodAutoscaler \> StatefulSet \> Job \> CronJob \> Ingress \> APIService \> Other（CustomResource）


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The environment has been created. For specific operations, refer to [Create environment](https://docs.byteplus.com/en/docs/cp/Create_environments).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the current application.

   1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the target workspace name to enter the target workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

   5. Click the target application card to enter the current application.

2. Click **Application Orchestration**, and switch to the Application Orchestration tab.

3. Click **edit** to enter the application orchestration page.

   The left side of the page displays all resources included in the current application, the middle section shows the YAML content for the corresponding resource, and the right side displays information about the placeholders used in the YAML.



|Feature |Descriptions |
|---|---|
|Add resource |In the left panel of the page, click the button in the upper right corner. **+** Add required resources.<br><br><br>* **Configmap**: a configuration\-type resource.<br><br>* **Deployment**: A stateless load\-type resource.<br><br>* **Service**: A resource of the service type.<br><br>* **Custom**: No restriction on kind; users can specify the kind. If you need to create resources other than the above three types, please select Custom.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only one kind is supported in a resource YAML.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only one resource of the Deployment type can be added to an application.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">An application can add up to 20 resources.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Resource names within an application are unique.</div><br> |
|Edit YAML content |On the left side of the page, click the title of the resource you want to edit. The YAML content of the current resource will be displayed in the central area. Edit as needed. When editing, you can directly enter parameter value constants. |
|Modify resource name |On the left side of the page, hover the mouse over the resource title. Click the edit icon that appears, then you can modify the resource name. |
|Delete resource |On the left side of the page, hover the mouse over the resource title. Click the delete icon that appears to delete unnecessary resources. |
|Form validation |Click **Form validation** to validate the entered content and help identify application orchestration issues early. |



4. After completing the configuration, click **confirm**.

5. In the pop\-up information box, set the following information:

   * Effective environment: Set the effective environment for this orchestration record. You can select zero or more environment instances.

   * Description: Set remarks for this scheduling record to facilitate traceability.

6. After completing the settings, click **create**.

   When application orchestration is successful, the system will generate a unique orchestration ID to record the current version of the application orchestration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each time an application orchestration is completed, a new orchestration record is generated.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only the latest orchestration record can be modified.   </div>
   


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Deploy the application immediately. For specific operations, refer to [K8s YAML application deployment](https://docs.byteplus.com/en/docs/cp/K8s_YAML_application_deployment).
