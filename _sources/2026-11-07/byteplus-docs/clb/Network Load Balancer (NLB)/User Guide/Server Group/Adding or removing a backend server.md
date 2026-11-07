---
title: "Adding or removing a backend server"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Adding-removing-backend-server"
---

<span id="fJKnccof"></span>
## Add server

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* The servers have been created and the applications deployed, so they can properly handle forwarded requests.

* The security groups or network ACLs associated with the servers have been configured to allow inbound traffic from the NLB. If not allowed, see [Configuring a backend server security group and Network ACL](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).

* Make sure that the servers to be added are consistent with the server group type and IP version.

   * Server type server group: Only ECS instances or secondary ENIs (Network Interfaces) within the same VPC can be added as backend servers.

   * IP type server group: Only IP addresses can be added as backend servers. As long as network connectivity is reachable, IPs from other VPCs or IDCs are also supported.


<span id="fl713AAl"></span>
### Action notes


* When client address keep\-alive is enabled for the NLB instance, binding an EIP address to a server\-type backend server will cause traffic destined for that IP address to be unreachable.

* The number of backend servers added in a single operation cannot exceed 100.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation pane, select **Server Group**.

3. In the top menu bar, select the target project and region.

   * **Server** ** type server group**

      1. Click  **··· \> Add server** to the right of the target server group.

      2. Click **Add server** and select a backend server.

         * By default, Advanced Mode is disabled, and you can only select the primary ENI of the ECS instance as the backend server.

         * After Advanced Mode is enabled, you can select the secondary ENI of the ECS instance as the backend server. Depending on your actual scenario, you can select one or more IP addresses for the secondary ENI.

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Notes         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">When selecting a secondary ENI as the backend server, you also need to <a href="https://docs.byteplus.com/en/docs/clb/NLB-Configuring-the-secondary-network-interface-routing">Configure the routing for secondary ENI</a> so that it can respond to requests from clients or the NLB.         </div>
         

      3. Click **Next** to configure ports and weight for the added backend servers.

         * When the same server provides different services over different ports, click **Add port** on the right side of the target server and add the required ports one by one.

         * When different servers provide services over the same port, select the target servers, click **Modify port** above the list, and set the port for them in bulk.

         
         |Parameters |Notes |Sample |
         |---|---|---|
         |Port |The port on which the backend server provides services.<br><br><br>* When the server group has all\-port forwarding enabled, the listener port is used by default to receive and handle traffic, and ports cannot be added or specified manually.<br><br>* Ensure that the security group associated with the backend server has allowed this port. For detailed configuration, see [Configuring backend server security group](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL). |80 |
         |Weight |This value indicates the probability that the backend server will receive requests (the probability equals the server's weight divided by the total weight of all servers in the group).<br><br><br>* The larger the weight, the more requests are forwarded, and the default is 100.<br><br>* A weight of 0 indicates that the server will no longer accept new requests.<br><br>* When the scheduling algorithm is Source Hashing (SH), only zero and non\-zero weights are distinguished. |100 |
         

      4. Click **Confirm** to complete the action.

   * **IP** ** type server group**

      1. Click  **··· \> Add IP address** to the right of the target server group.

      2. Click **Add server**, then configure the backend server information according to the table below.

         * When the same server provides different services over different ports, click **Copy** on the right side of the target server and add the required ports one by one.

         * When different servers provide services over the same port, select the target servers, click **Modify port** above the list, and set the port for them in bulk.

         
         |Parameters |Notes |Sample |
         |---|---|---|
         |IP address |Enter the IP address of the backend server. Supported IP address ranges: `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.<br><br>When adding a secondary private IP address of an ECS instance within the same VPC as a backend server, you must also [Configure the routing for the secondary ENI](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-the-secondary-network-interface-routing) so that it can respond to requests from clients or the CLB. |192.168.2.10 |
         |Zone |Select the Availability Zones from which this backend server can receive access requests.<br><br>When cross\-az forwarding is disabled for the NLB instance, this backend server will only receive traffic from the same Availability Zone. If you want this backend server to receive traffic from other Availability Zones, select **All** here. |All |
         |Port |The port on which the backend server provides services.<br><br><br>* If the instance corresponding to the specified IP address is associated with a security group, ensure that the security group has opened the port specified here. For detailed configuration, see [Configuring a security group for backend servers](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL).<br><br>* If the server corresponding to the specified IP address has other access control policies configured, those policies must also allow traffic on the port specified here. For details, see [Configuring backend server access control](https://docs.byteplus.com/en/docs/clb/NLB-Configuring-backend-server-security-group-and-Network-ACL). |80 |
         |Weight |This value indicates the probability that the backend server will receive requests (the probability equals the weight of this IP address divided by the total weight of all IP addresses in the group).<br><br><br>* The larger the weight, the more requests are forwarded, and the default is 100.<br><br>* A weight of 0 indicates that the server will no longer accept new requests.<br><br>* When the listener scheduling algorithm is Source Hashing (SH), only zero and non\-zero weights are distinguished. |100 |
         

      3. Click **Confirm** to complete the action.


<span id="oEdUkW7u"></span>
## Remove server

<span id="1dWu3VyT"></span>
### Action notes


* Removing a backend server only disassociates it from the NLB; it does not delete the server itself.

* When you delete a backend server from a server\-type server group, the system automatically removes it from the group.


<span id="qpJntNNX"></span>
### Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation pane, select **Server Group**.

3. In the top menu bar, select the target project and region.

4. Click the name of the target server group.

5. In the **Server** tab, click **Remove** to the right of the target server.

6. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AddNLBBackendServers](https://docs.byteplus.com/en/docs/clb/AddNLBBackendServers)

* [RemoveNLBBackendServers](https://docs.byteplus.com/en/docs/clb/RemoveNLBBackendServers)


&nbsp;
