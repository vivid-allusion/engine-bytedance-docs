---
title: "Creating Upstreams of VCI Agent Sandbox type"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_Upstreams_of_VCI_Agent_Sandbox_type"
---

APIG supports integration with VCI Agent Sandbox. It abstracts Agent Sandbox Pods under VCI instances in a container cluster into an Upstream and uses it as a routing backend for the gateway. This is suitable for scenarios where a business is deployed using Agent Sandbox and needs to dynamically route traffic by Sandbox ID through the gateway. This topic describes how to create an Upstream of the VCI Agent Sandbox type.

<span id="tVBmbokS"></span>
## Prerequisites


* An APIG instance has been created. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The cluster to integrate with has been added as an Upstream source. For specific operations, see [Importing VKE clusters](https://docs.byteplus.com/en/docs/apig/Import_container_cluster).

* A label has been configured for the Agent Sandbox Pod. For more information, see [Injecting node labels or annotations into pods](https://docs.byteplus.com/en/docs/vke/Injecting-node-labels-and-annotations-into-pods?lang=en).


<span id="MUtcbFv6"></span>
## Usage limits

The APIG instance and VKE cluster must be in the same VPC.

<span id="cFyY5zAr"></span>
## Procedure


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the **Instance management** drop\-down list. Then, click **Upstreams**. 

4. On the Upstream list page, click **Create Upstream**.

   5. On the "Create Upstream" page, enter the parameter information as required.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |Upstream name |Specify a name for the Upstream. The Upstream name must be unique within the same instance. |
      

   * **Back\-end configuration**

      
      |Parameter |Description |
      |---|---|
      |Backend service |Select the backend service type that the Upstream integrates with. In this scenario, **VCI Agent Sandbox** is selected. |
      |Listening range |Configure the listening scope.<br><br><br>* **All Sandboxes**: Covers all Sandboxes in the selected cluster.<br><br>* **Label selected**: Enter the Key and Value of the Sandbox Label. **Using form editing** and **Using JSON format editing are supported**. |
      

6. Click **Confirm**.


<span id="jv0A5d2R"></span>
## Validate results

After the Upstream is created, you can view the Upstream of the VCI Agent Sandbox type in the Upstream list.

<span id="mnc7n8sI"></span>
## Security group configuration


* When APIG integrate with a VPC\-CNI cluster, access is allowed by default and no extra access configuration is required.

* When APIG integrates with a Flannel cluster, you need to allow inbound access from the APIG security group (named `apig-sg-<accountID>`) for all nodes in the Flannel cluster. This ensures that the gateway can properly access resources within the cluster. All nodes in VKE are associated with a default security group named `<ClusterID>-common`. You only need to add an inbound rule to this default security group to allow access from the APIG security group. To do so, follow the steps below:

   1. Log in to the [VKE console](https://console.byteplus.com/vke). In the left navigation pane, select **Cluster**. On the cluster list page, click the target Flannel cluster to enter the cluster management page.

   2. In the left navigation pane, select **Node**. On the node list page, click any node name to enter the node details page.

   3. In the "Basic information" section, locate the default VKE security group named `<ClusterID>-common` and click to view its details.

   4. Switch to the **Access rules** tab, and click **Add rule** in the **Inbound rule** section.

   5. In the **Add inbound rule** dialog box, configure the APIG security group information as required. Retain the default settings for parameters not mentioned in the following table.

      
      |Parameter |Description |
      |---|---|
      |Protocol |Select "ALL" to allow access over all communication protocols. |
      |Source address |Select **Security Group**, and select the APIG security group named `apig-sg-<accountID>`. |
      

   6. Click **Confirm**.
