---
title: "View instance information"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_instance_information"
---

This topic describes how to view detailed information of a Milvus for VectorDB instance, and explains the information on the Instance details page.

## Prerequisites

An instance is created. For more information about how to create an instance, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. On the **Instances** page, select the **Dedicated**, **Serverless**, or **On\-Demand** tab as needed, then click the instance name of the target instance.

   On the **Instance details** tab, you can view the following information about the instance.

   |**Parameter** |**Description** |
   |---|---|
   |Basic information |Basic information includes instance name, instance ID, version, kernel version, instance region, project, deletion protection, availability zone, embedding, and labels.<br><br>> **tip**<br><br><br><br>* > Availability zone and kernel version apply only to Dedicated instances.<br><br><br>* > You can click the edit icon to the right of **Tags** to view details, modify, or delete tags.<br> |
   |Service node configuration |Service node configuration includes the specifications and quantity of each type of service nodes.<br><br>> **tip**<br><br><br>> Service node configuration applies only to Dedicated instances.<br> |
   |Index node configuration |Index node configuration information includes the node type, CU type, specifications, and quantity of index nodes.<br><br>> **tip**<br><br><br>> Index node configuration applies only to Dedicated instances.<br> |
   |Compute node configuration |Compute node configuration information includes the node type, CU type, specifications, and quantity of compute nodes.<br><br>> **tip**<br><br><br>> Compute node configuration applies only to Dedicated instances.<br> |
   |Storage information |Storage information refers to the instance's storage capacity usage.<br><br>> **tip**<br><br><br><br>* > Storage usage statistics have a certain delay and are for reference only, and are not used for billing.<br><br><br>* > Storage information applies only to Dedicated instances.<br> |
   |Billing information |Billing information includes instance creation time, billing type, automatic renewal status, and instance expiration time. |
   |Network information |Network information includes the transport protocol, virtual private cloud, subnet, private network address, public network access status, and the public access address used by the instance. You can toggle HTTPS on or off by clicking the switch next to **Transport protocol**.<br><br>> **warning**<br><br><br><br>* > On\-Demand edition instances do not support configuring the transport protocol.<br><br><br>* > After enabling HTTPS, the instance access address will change. Update the client configuration promptly to avoid service interruption.<br><br><br>* > The instance will be temporarily inaccessible during the HTTPS switch.<br><br><br>* > After switching to HTTPS for Dedicated edition instances, gRPC and RESTful APIs use different ports, as follows:<br><br><br>   * > gRPC (SDK): 19530<br><br><br>   * > HTTP (RESTful API): 8080<br><br><br>* > After switching to HTTPS for Serverless edition instances, gRPC and RESTful APIs continue to use the same port, but the port changes from 19530 to 19531.<br> |
   |Instance access information |Instance access information includes the user name, password, private network address, and public network access information used to access the instance. |
   |Architecture diagram |The architecture diagram displays the instance’s service nodes, compute nodes, and their statuses, supporting node filtering by status. After pointing to the node icon, you can view Node ID, Status, CPU specifications, CPU usage, Memory specifications, Memory usage, Creation time, and Update time in the node card.<br><br>> **tip**<br><br><br>> The architecture diagram applies only to the Dedicated instances.<br> |
