---
title: "Creating a backend server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-a-server-group"
---

This article introduces how to create a backend server group.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* The backend server group belongs to the same project as its CLB instance by default.

* After enabling the IP\-type backend server group feature, you can create an IP\-type backend server group for a newly created Classic Load Balancer (CLB) instance.

* The number of backend server groups that can be created by a single CLB instance is 20. If the default quota does not meet your needs, please go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=CLB) to increase the corresponding quota.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target project and target region.

3. Click the target instance name.

4. On the **Server Group** tab, click **Create Server Group**.

5. Refer to the table below for configuration related arguments.

   
   |Parameter  |Parameter Description |Sample Value |
   |---|---|---|
   |Term |Enter the name of the backend server group. |rsp01 |
   |Type |Select the Type of the Server Group.<br><br><br>* Server Type: Only supports adding ECS instances that are in the same VPC with the CLB instance / secondary network interfaces that are already associated with ECS instances as backend servers.<br><br>* IP Type: Only supports adding IP address as backend servers. As long as the network is reachable, you can add IP addresses of other VPCs or IDCs as backend servers.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">IP\-type server group feature is currently in the beta stage. If you need to use it, please contact the account manager.   </div><br>    |Server Type |
   |IP Address Version |The protocol type of the backend server's private IP address.<br><br><br>* IPv4: Only supports adding IPv4 backend servers.<br><br>* IPv6: Only supports adding IPv6 backend servers. IPv6 is only supported when the CLB instance is dual\-stack and the backend server group uses **Server\-type** targets. |IPv4 |
   |All\-port forwarding |All\-port forwarding needs to be enabled only when the Server Group needs to Attach a listener to listen by port range.<br><br><br>* After enabling, all servers in the group will use all\-port forwarding, and specific ports are not supported.<br><br>* Applicable to scenarios where a backend server application opens a continuous port range. For more details, please refer to [Creating a TCP protocol listener](https://docs.byteplus.com/en/docs/clb/Creating-a-TCP-listener) and [Creating a UDP protocol listener](https://docs.byteplus.com/en/docs/clb/Creating-a-UDP-listener).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The listener all\-port listening feature is in the beta stage. If you need to use it, please contact your account manager.</div><br> |Disable |
   |Tag |A tag consists of a key\-value pair. You can use tags to classify and search for resources. For more information about tags, refer to [Tag Management](https://docs.byteplus.com/en/docs/clb/Tag-management).<br><br>Click the add icon, input the Tag key and Tag value, to add a tag to the Server Group. |* Tag Key: rsp\-key<br><br>* Tag value: rsp\-test |
   

6. Click **OK**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After creating the backend server group, you also need to [Add backend servers](https://docs.byteplus.com/en/docs/clb/Adding-a-server).

<span id=".55u45YWz5paH5qGj"></span>
## Related document

[CreateServerGroup](https://docs.byteplus.com/en/docs/clb/CreateServerGroup)
