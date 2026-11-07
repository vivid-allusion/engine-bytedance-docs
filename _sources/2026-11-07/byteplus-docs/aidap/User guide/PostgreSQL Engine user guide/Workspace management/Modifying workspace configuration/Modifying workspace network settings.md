---
title: "Modifying workspace network settings"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Modifying_workspace_network_settings"
---

Network protocol types, virtual private cloud, and subnet support configurations in the AI Native Database Platform Workspace. This topic introduces the operation steps for modifying the above configurations.

<span id="dUkgCv2W"></span>
## Prerequisites

A workspace is created and its status is **Running**.

<span id="5B6EbdLj"></span>
## Precautions


* A newly created workspace using the PostgreSQL engine will use the shared public network provided by AI Native Database Platform by default. The virtual private cloud and subnet on the **Workspace settings page** are empty.

* After modifying the virtual private cloud and subnet, private network access for the workspace cannot be disabled.

* Confirm the following risks before executing the operation: Modifying the VPC and subnet does not change the private domain name, but the private IP address will change.

* Clear the client cache promptly to avoid potential read/write abnormalities.

* Changing the virtual private cloud and subnet will alter the IP address used by the workspace. The previously used IP, once released, may be occupied by other systems and cannot be selected again.


<span id="SgTcAQk0"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. In the middle navigation bar, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span> **Workspaces** to access the workspace list.

4. In the workspace list, click  **...**  \> **Configure** in the target workspace row to enter the **Workspace settings page**.

5. On the **Workspace settings** page, locate the **Network configuration** area, set the network protocol type, virtual private cloud, and subnet used by the workspace, then click **Save**.

   * **Network protocol type** includes **IPv4** and **IPv4 + IPv6**.

   * **Virtual Private Cloud** can be selected from the drop\-down list for the workspace. You can also click **Create VPC ** on the right to create a new VPC. For more information on this operation, refer to [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

   * **Subnet** can be selected from the subnets of the specified virtual private cloud from the drop\-down list. You can also click **Create subnet** on the right to create a new subnet within the specified virtual private cloud. Refer to [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).


<span id="W1CWMPfw"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ModifyVpcSettings](https://docs.byteplus.com/en/docs/330/ModifyVpcSettings) |Call the ModifyVpcSettings API to modify the workplace's virtual private cloud and subnet. |
