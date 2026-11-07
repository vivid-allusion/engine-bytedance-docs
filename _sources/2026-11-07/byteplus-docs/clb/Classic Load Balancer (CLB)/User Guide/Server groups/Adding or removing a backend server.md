---
title: "Adding or removing a backend server"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Adding-a-server"
---

## Add backend server

### Action description

* If the subnet where the backend server to be added resides is associated with Network ACL rules, you need to configure the Network ACL of the backend server subnet to ensure CLB functions properly.

* CLB supports adding backend servers of IPv4 or IPv6 type; you can choose as needed.

* A single CLB instance supports up to 200 backend servers. If the default quota does not meet your needs, please go to Quota Center to increase the corresponding quota.

* To add backend servers across VPCs, see [adding cross-VPC backend servers](https://docs.byteplus.com/en/docs/clb/Combining-with-the-TR-service-to-use-an-ECS-instance-in-a-VPC-as-the-cross-VPC-server).

### Procedures

The steps to add backend servers vary depending on the type of the backend server group.

* For the server\-type server group, please see Adding servers.

* For the IP\-address\-type backend server group, see Adding an IP address.

**Add server**

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name.

4. On the Server Group tab, click the name of the target server group.

5. Click Add Server to enter the ECS instances page.

   The list displays all Elastic Compute Service (ECS) instances located in the same VPC as the CLB instance. You can select ECS instances or secondary network interfaces mounted on ECS instances as backend servers.

   * Advanced mode is off by default, meaning the system uses normal mode by default, which only supports selecting the primary network interface of ECS instances as backend servers.

   * After enabling advanced mode, you can select the secondary network interfaces of ECS instances as backend servers. You can select one or more IP addresses of secondary network interfaces based on actual needs.

   > **tip**

   * > If there are many ECS instances and secondary network interfaces in the list, you can quickly find the target resource by ECS instance name or ID.

   * > When selecting secondary network interfaces as backend servers, you also need to [configure secondary network interface routes](https://docs.byteplus.com/en/docs/clb/Configuring-route-entries-for-a-secondary-network-interface) to allow the network interfaces to respond to requests from clients or the CLB instance.

6. Click **Next** to configure ports and weights for the added backend servers.

   If you select secondary network interfaces as backend servers and choose multiple IP addresses, the backend server information will display multiple rows based on the number of IP addresses. You need to configure ports and weights separately for each IP address of the same secondary network interface.

   |Parameter name |Parameter description |Example |
   |---|---|---|
   |Port |For the port used by backend servers to receive traffic, you must ensure that the security group associated with the server has allowed the corresponding port. For detailed configuration, refer to Configuring a backend server security group. |80 |
   |Weight<br><br> |The probability of the backend server receiving a request (probability = the server weight / the total weight of all servers in the group).<br><br><br>* The larger the weight, the more requests are forwarded; the default is 100.<br><br>* If the weight is set to 0, the server will not accept new requests.<br><br>* If the listener scheduling algorithm is Source IP Hash (SH), weights only distinguish between 0 and non\-zero values. |100<br><br> |

   * Batch settings: When multiple backend servers require identical port or weight settings, select them in the list and click Modify Port or Modify Weight to configure them in a batch.

   * Single settings: Click Add port on the right side of the target backend server to add multiple ports and configure corresponding weights for the backend server. This is suitable for scenarios where the server uses different ports to provide different services.

7. Click **Migrate** to complete the action.

**Add IP address**

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name.

4. On the Server Group tab, click the name of the target server group.

5. Click Add Server to enter add IP address page, and configure the backend server information as shown in the table below.

   |Parameter name |Parameter description |Example |
   |---|---|---|
   |IP Address<br><br> |Enter the IP address of the backend server. When adding secondary private IPs of ECS instances within the same VPC as backend servers, you also need to [configure the secondary network interface route](https://docs.byteplus.com/en/docs/clb/Configuring-route-entries-for-a-secondary-network-interface) to allow the network interface to respond to requests from clients or CLB instances. |192.168.2.10<br><br> |
   |Port |The port that the backend server provides services on. If the instance corresponding to the specified IP address is associated with a security group, confirm that the security group has allowed traffic on the designated port. For detailed configuration, refer toConfiguring a backend server security group. |80 |
   |Weight<br><br> |The probability of the backend server receiving a request (probability = the IP address weight / the total weight of all IP addresses in the group).<br><br><br>* The larger the weight, the more requests are forwarded; the default is 100.<br><br>* If the weight is set to 0, the server will not accept new requests.<br><br>* If the listener scheduling algorithm is Source IP Hash (SH), weights only distinguish between 0 and non\-zero values. |100<br><br> |

   * Batch modification: When multiple backend servers require identical port or weight settings, select them in the list and click Modify Port or Modify Weight to configure them in a batch.

   * Single modify: Directly modify the port in the target backend server's row.

   * Copy: To add different ports of the same IP address as backend servers, click Copy to the right of the target IP address to quickly duplicate a record, allowing you to fill in the required port number.

6. Click **Migrate** to complete the action.

## Remove server

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the target CLB instance name.

4. On the Server Group tab, click the name of the target server group.

5. Click Remove on the right side of the target server group.

6. Click **Migrate** to complete the action.

## Related documents

* [AddServerGroupBackendServers](https://docs.byteplus.com/en/docs/clb/AddServerGroupBackendServers)

* [RemoveServerGroupBackendServers](https://docs.byteplus.com/en/docs/clb/RemoveServerGroupBackendServers)
