---
title: "Node group management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_Node_group_management"
---

This article introduces related operations for node management in Volcano Engine E\-MapReduce (EMR) clusters.

<span id="_1-进入节点管理"></span>
## Access node management


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. In the left navigation bar, click **Resource Management \> on ECS \> Cluster Name** to enter the specific cluster details page.

3. On the cluster details page, click the **Nodes**tab to access the node group list page.


<span id="_2-查看节点组列表信息"></span>
## View **node group list** information


|Name |Description |
|---|---|
|Node group name/ID |Click the node group name to open the drawer and obtain all node information for that node group |
|Role |After initialization is completed, the roles Master, Core, Task, and GateWay cannot be changed. |
|Quantity |The number of nodes contained in the node group |
|Instance specification |ECS corresponding model, vCPU, memory, and network bandwidth |
|Disk |Current disk information of the node group |
|Payment type |Current payment type of the node group |
|state |The current status of the node group (Normal, Warning). When the node group is in Warning status, hovering the mouse over the status will indicate how many nodes are abnormal. |
|Operation |Expand disk capacity and the number of nodes for all machines in the node group |


<span id="_3-节点列表"></span>
## **Node list**

After clicking the node group name, the right drawer expands to display the **node list** of the node group:


|Name |Description |
|---|---|
|Node name/Node ID |The host name is automatically created by the system during cluster initialization, following the naming convention: EMR\-{instance type}{number}\-{cluster ID}<br><br>Click the ECS ID to navigate to the ECS host details |
|IP address |The IP address of the ECS host |
|Deploy service |The number of services deployed on the host. Hover over to expand the list of all services, components, and their statuses installed on the host |
|Node status |ECS status (refer to [lifecycle](https://docs.byteplus.com/en/docs/ecs/Instance\-lifecycle Instance lifecycle) for details) |


<span id="_4-新增节点组"></span>
## **Add node group**

You can add node groups to meet the requirements of different instance nodes.


1. Click the "Current newly added node group" button in the upper right corner of the **Node group list** interface to open the drawer.

2. Select the type of node group to add. You can add Core, Task, and GateWay node groups.

   
   |Node group type |Description |
   |---|---|
   |Master<br><br>(Manual creation is not supported) |Mainly responsible for deploying control processes, such as ResourceManager and NameNode. High processing power is not required. |
   |Core |Mainly responsible for storing all data in the cluster. After the cluster is created, scaling is also supported as needed. Requires both processing power and storage capacity. |
   |Task |Does not save data; adjusts the computing power usage of the cluster. Disabled by default; can be added as needed. Only processing power is required. |
   |GateWay |The GateWay node group can add and manage other nodes, automate client component updates, and synchronize EMR cluster configurations. This meets the need to rapidly change and configure development machine parameters in scenarios such as modifying configurations or adding new development machines.<br><br><br>* Only supports Hadoop clusters.<br><br>* Supported for EMR 3.x versions greater than or equal to EMR\-3.5.0 and EMR 2.x versions greater than or equal to EMR\-2.4.0. |
   

3. Enter the node group name and select the source of service parameters for initialization. If there are no machine group service parameters available for copying, you can select the system default configuration parameters, that is, Default.

4. Select the instance type, system disk, and data disk configuration.

5. Set the number of nodes in the node group.

6. Check the "**EMR Service Terms**" and confirm to complete the creation and scaling of the node group.


<span id="_5-节点组扩容"></span>
## Expand node group


1. Click the **Expand** button in the **Actions** column of the node group list to configure scaling settings on the node scaling page.

2. Fill in the information in the node scaling drawer:

   
   |Configuration item |Description |
   |---|---|
   |current instance configuration |* Node group name<br><br>* Node group ID<br><br>* Node group specification<br><br>* Node configuration<br><br>* x vCPU<br><br>* Disk type |
   |Scale\-out configuration |Displays the current number of instances. Select the number of additional instances to add. |
   |Price after scaling |Displays the real\-time calculated price after scaling. |
   |Operation |After agreeing to the service terms, click the **Confirm** button to start the scaling operation for the cluster. |
   


<span id="_6-磁盘扩容"></span>
## Expand disk


1. Click **Disk expansion** or **volume expansion** in the **Actions** column of the node group list to open the expansion drawer.

2. Confirm the information in the disk expansion drawer:

   
   |Configuration item |Description |
   |---|---|
   |current instance configuration |* Node group name<br><br>* Node group ID<br><br>* Node group specification<br><br>* Node configuration<br><br>* x vCPU<br><br>* Disk type |
   |Scale\-out configuration |* <br><br>* <br><br>* When **Disk expansion** is selected: expand the single disk capacity of the **system disk** or **data disk**.<br><br>* When **volume expansion** is selected: supports increasing the number of **data disks** for Core and Task node groups, up to a maximum of 8 disks.<br><br>* After the disk **volume expansion**, the service components where the node group resides must be restarted. |
   |Price after scaling |Displays the real\-time calculated price after scaling. |
   |Operation |After agreeing to the service terms, click the **Confirm** button to start the scaling operation for the cluster. |
