---
title: "Add secondary network interface as backend server"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Associating-a-secondary-network-interface-with-an-instance"
---

[The secondary network interface](https://docs.byteplus.com/docs/ecs/Network-interface-overview) is an elastic network interface. The secondary network interface can be attached to an ECS instance within a VPC and can migrate between different ECS instances.

ALB allows you to add the primary and secondary private IP addresses of the secondary network interface to the server group.

To use a secondary network interface as a backend server, complete the following steps:


1. Add a secondary network interface: add the IP address of the secondary network interface to the server group.

2. Configure network interface routing: manually configure the network interface routing to ensure the backend server can properly respond to requests from clients or ALB instances.


<span id="15f50111"></span>
## Add secondary network interface

<span id="b7ef8af2"></span>
### Before you begin

The secondary network interface is attached to the ECS instance. For detailed operations, see [attach secondary network interface](https://docs.byteplus.com/docs/ecs/Attaching-and-detaching-secondary-network-interfaces).

<span id="b45a133c"></span>
### Procedure


1. Log in to the [Application Load Balancer console](https://console.byteplus.com/alb).

2. In the left navigation pane, click **server group** to go to the **server group** page.

3. On the **server group** page, find the server group where you want to add backend servers, then click **add server** in the **actions** column.

4. On the **select backend server** page, enable **advanced mode**.

5. Check the secondary network interface attached to the ECS instance, select the IP address, then click **next: configure port and weight**. You can select one or multiple IP addresses of the secondary network interface.

6. On the **configuration port and weight** page, set the port and weight for the backend server, then click **confirmed**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select multiple IP addresses of one secondary network interface as backend servers, you need to configure the port and weight separately for each IP address.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to batch configure the same port or weight for backend servers, select these backend servers and click <strong>Set the same weight</strong> or <strong>Set same port</strong> below the list, then enter a value.   </div>
   

   
   |**Configuration Item** |**Description** |
   |---|---|
   |Port |Configure the backend server's port. The backend server uses this port to provide services and receive requests. The value ranges from 1 to 65535. |
   |Weight |Configure the weight of the backend server. The default value is 100. Value range: 0 to 100.<br><br><br>* The weight determines the traffic distribution ratio. The proportion of requests received by a single backend server = the backend server’s weight / the sum of all backend servers' weights in the server group.<br><br>* Backend servers with higher weights receive more requests. If the backend server's weight is 0, ALB will not forward requests to that backend server.<br><br>* When the routing algorithm applied to the server group is source address hashing, ALB no longer forwards requests based on the weight value. |
   |Copy |Optional. Click **Copy** to clone an added backend server entry. After copying, enter a different port number in the new entry. This allows the Application Load Balancer to forward requests to different ports on the same backend server. |
   |Remove |Optional. Click **Remove** to remove the added backend server. |
   


<span id="0096abaf"></span>
## Configure network interface routing

ALB forwards client requests and sends health check requests to backend servers using the VPC CIDR block 100.64.0.0/10. When using a secondary network interface as a backend server, you need to configure a route for this secondary network interface targeting the private network CIDR block. This allows the backend server to properly respond to client requests and health check requests.

The routing information to be configured is as follows:


|**Destination** |**Destination address mask** |**Gateway address** |**Network interface** |**Hop count** |
|---|---|---|---|---|
|100.64.0.0 |255.192.0.0 |Gateway address of the subnet where the network interface resides |Secondary network interface name, such as eth2 |100 |


For detailed steps to configure network interface routing, refer to [Configure network interface routing](https://docs.byteplus.com/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After configuring routing via the command line, manually added routes will be cleared when you restart the ECS instance. In this case, you need to reconfigure the routes.</div>
