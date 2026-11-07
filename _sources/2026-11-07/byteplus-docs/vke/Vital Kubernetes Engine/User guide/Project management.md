---
title: "Project management"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Project-management"
---

Project management is a resource management method provided by BytePlus. Vital Kubernetes Engine (VKE) allows you to manage resources such as clusters, node pools, and nodes by project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about projects, see <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management">Project management</a>.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* You can manage the following VKE resources by project: clusters, node pools, and VKE\-associated basic cloud resources except for the resources of Torch Log Service (TLS), Vital Managed Service for Prometheus (VMP), and Application Load Balancer (ALB).

* A resource can belong to only one project.

* If you modify the permission scope of the KubernetesNodeRoleForECS role that VKE depends on, you need to ensure that the scope is set to **global**.

* After resources are bound to a project, the resources can only be used by users who are granted permission on the project.

* The association between resources remains unchanged after the resources are added to a project.

* If you need to associate resources from multiple projects, you need permission on all these projects. For example, suppose you want to associate a cluster in Project A with an Elastic IP Address (EIP) in Project B. In this case, you need permission on both Project A and Project B. 

* When you use an Identity and Access Management (IAM) user to create and manage resources, the IAM user needs to be granted the appropriate permissions by the BytePlus root user. For specific operations, see [Configuring IAM user permissions](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions).


<span id=".6aG555uu566h55CG5L2_55So5rWB56iL"></span>
## Usage process for project management

This topic provides an example on how to manage clusters by project. The general process for using the project management feature is as follows:


1. [Create a project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project): Create a project to manage instances by project.

2. [Configure IAM user permissions](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions): Grant project permissions to an IAM user.

3. [Create a cluster](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances): Use the IAM user to create a cluster and bind the cluster to the project.

4.  (Optional)[ Move the cluster into or out of the project](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management): When the project associated with the cluster changes, you can move the cluster into or out of a project.


<span id=".5p-l55yL6aG555uu6LWE5rqQ5L-h5oGv"></span>
## Viewing project resources

<span id=".5p-l55yL6LWE5rqQ5omA5Zyo6aG555uu"></span>
### Viewing the project where a resource belongs


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the name of the target cluster.

4. In the **Basic information** section, view the **project** where the cluster is located.


<span id=".6YCa6L-H6aG555uu5pCc57Si6LWE5rqQ"></span>
### Searching for resources by project


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the top navigation bar, select a region, and then select a project based on the following instructions.

   * Select **Account All Resources** to view all resources within the current account.

   * Select a specific project to view all resources that are bound to the project.

   * Click Manage project to go to the project list page, where you can manage projects.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the system displays all resources within the current account.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you log in to the console as an IAM user but the IAM user has not been granted global permissions, all resources within the root user will not be displayed when you select <strong>Account All Resources</strong>. In this case, switch the project or contact the BytePlus root user for authorization.   </div>
