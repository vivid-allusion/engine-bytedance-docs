---
title: "Enabling workspace access over the Internet using NLB and PrivateLink"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Enabling-workspace-access-over-the-Internet-using-NLB-and-PrivateLink"
---

VMP workspaces support enabling public access using Network Load Balancer (NLB) and PrivateLink. This topic describes how to configure PrivateLink to read and write data in a VMP workspace.

## Background

A VMP workspace offers a standard remote write URL and a standard query URL that can be accessed over internal networks. This allows you to collect service metrics and business metrics in the internal networks of the public cloud and deploy Grafana in a VKE cluster to create and view metric dashboards. For more details, see [Deploying Grafana and connecting to a workspace in the VKE cluster](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster).

In some scenarios, you may need to access the data of a VMP workspace over the Internet. For example, in multi\-cloud scenarios, you need to aggregate data from multiple public clouds to Grafana for centralized viewing. In such cases, public access to VMP workspaces can be achieved by configuring a public NLB and PrivateLink.

## Prerequisites

A VMP workspace has been created, and basic authentication has been enabled. For details, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

## Procedure

### Step 1: Create a PrivateLink endpoint for the VMP workspace

> **tip**

* > We recommend using a  root user for this operation. When you create an endpoint as an IAM user, insufficient permissions may prevent selection of available endpoint services. If this issue occurs, see [Why can't I select available endpoint services when creating an endpoint?](https://docs.byteplus.com/en/docs/privatelink/FAQs) for troubleshooting.

* > In a read/write separation scenario, you need to create separate endpoints for read and write operations.

1. Log in to the [VPC console](https://console.byteplus.com/vpc).

2. In the left navigation pane, select **PrivateLink \> Endpoint**. On the **Interface Endpoint** tab, click **Create Endpoint** and complete the parameter configuration.

   |Parameter |Parameters |Description |
   |---|---|---|
   |Basic information |Region |The region of the endpoint. Select the same region as the VMP workspace's region. |
   ||Name |Specify a custom name for the endpoint. |
   ||Type |The endpoint type. Select **Interface**.<br><br>> **tip**<br><br><br>> An interface endpoint is an elastic network interface with a private IP address from the subnet and can forward access traffic to the associated endpoint service. This type is applicable to scenarios where service resources in VPCs for the same account or across accounts need to be shared.<br> |
   ||Project |Select the owning project of the endpoint.<br><br>> **tip**<br><br><br><br>* > If no project is specified, this endpoint belongs to the "default" project.<br><br><br>* > Endpoints cannot be shared across projects. After a project is selected, the created endpoint can only be used by authorized users within that project.<br><br><br>* > For more information about endpoint projects, see [Project management](https://docs.byteplus.com/en/docs/privatelink/Managing-projects).<br> |
   |Endpoint Service |Enable cross\-region |Whether to enable cross\-region support. After this feature is enabled, the endpoint can connect to endpoint services in different regions. |
   ||Service region |Select the region where the endpoint service to be connected by the endpoint is located.<br><br>> Description<br><br><br>> If cross\-border connections are involved, the account must qualify for cross\-border transmission. For details, see [Cross\-border business overview](https://docs.byteplus.com/en/docs/6405/1184976).<br> |
   ||Add method |Select the method to add the endpoint service to be associated. Select a method as needed to specify the endpoint service. Select **BytePlus Service**. |
   ||Endpoint Service |Select the service purpose for the endpoint. Select **VMP Readonly** or **VMP Writeonly**.<br><br><br>* **VMP Readonly**: Queries workspace data (for example, Grafana Query access).<br><br>* **VMP Writeonly**: Writes data to workspaces (for example, the collector's Remote Write). |
   |Network Configuration |IP address type |Select the IP address type of the endpoint. Select IPv4.<br><br>> **tip**<br><br><br>> To select both IPv4 and IPv6, ensure the following conditions are met:<br><br><br><br>* > The selected endpoint service supports IPv6.<br><br><br>* > The selected VPC has an IPv6 CIDR block enabled, and there is a subnet with an IPv6 CIDR block enabled.<br> |
   ||VPC |Select the VPC to which the endpoint belongs. |
   ||Availability Zone and Subnet  |Select the availability zone and subnet of the endpoint.<br><br><br>* Only availability zones supported by the **endpoint service** can be selected.<br><br>* After the subnet is selected, the system automatically creates an endpoint network interface within the subnet.<br><br>   * **IP address allocation method:** <br><br>      * Automatic allocation: The system automatically allocates an unused IP address from the selected subnet.<br><br>      * Manual allocation: Manually enter an unused IP address in the selected subnet.<br><br>   * **IP address allocation:** <br><br>      * If the IP type is IPv4, allocate an IPv4 address.<br><br>      * If the IP type is IPv4 and IPv6, allocate an IPv4 address and an IPv6 address.<br><br>      * If the IP type is IPv6, allocate an IPv6 address. |
   ||Security group |Select the security groups to associate with the endpoint network interface.<br><br>> **tip**<br><br><br><br>* > If the selected **VPC** is a shared VPC, the security groups must be created by the current account. Shared security groups cannot be selected.<br><br><br>* > Confirm that port 8080 is allowed by the security groups. Otherwise, the port may be inaccessible.<br> |
   |Advanced options<br><br> <br><br> <br><br> |Private DNS name |Enable the private DNS name. This allows you to specify a custom domain name for the endpoint.<br><br>> **tip**<br><br><br><br>* > An endpoint can enable a DNS name only when the endpoint service associated with the endpoint has a DNS name enabled and the public domain name has passed verification. If this option is enabled, the private DNS name defaults to the private DNS name configured for the endpoint service, and you can use this private DNS name to access the endpoint service.<br><br><br>* > For details on how to enable and verify a private DNS name for an endpoint service, see [Modifying and verifying a private DNS name](https://docs.byteplus.com/en/docs/privatelink/Modifying-Verifying-private-DNS-names).<br> |
   ||Tags |A tag is a key\-value pair and is used for resource classification and search. For more information about tags, see [Tag management](https://docs.byteplus.com/en/docs/privatelink/Managing-tags).<br><br>Click **Add tag** and enter a tag key and tag value to add a tag to the endpoint. |

3. After reviewing and confirming the relevant service agreements, click **Buy now** to complete the creation.

4. Return to the endpoint list and wait for the **connection status** of the endpoint to change to **connected**.

5. Run `curl http://<endpoint domain>:8080` on an ECS or Pod in the same VPC. If `Not Found` is returned, it indicates that the endpoint, domain, and network are connected.

6. Return to the endpoint list, click the name of the created endpoint, switch to the **Availability Zone and network interface** tab, and record the **IP address**.

### Step 2: Create a public NLB instance

1. Log in to the [NLB console](https://console.byteplus.com/nlb/region:nlb+cn-beijing/LoadBalancer).

2. In the top navigation pane, select the **project** and **region** that match the VMP workspace.

3. Select **Instances** in the left navigation pane and click **Create NLB**.

4. Configure the key parameters as described in the table below and other parameters as needed. For more information about configuring parameters, see [Creating an NLB instance](https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance).

   |**Parameters** |**Description** |
   |---|---|
   |**Region** |The region in which the NLB instance resides.<br><br>> **tip**<br><br><br>> The created NLB instance is available only to resources in that region and cannot be migrated. Ensure that the instance's region matches that of the VMP workspace.<br> |
   |**VPC** |The VPC to which the NLB instance belongs.<br><br>> **warning**<br><br><br>> It must be within the same VPC where the PrivateLink endpoint created in **Step 1** is located. Otherwise, the NLB cannot access this endpoint.<br> |
   |**IP version** |Private IP address type of the NLB instance.<br><br><br>* **IPv4**: Supports only IPv4 addresses.<br><br>* **Dual stack**: Supports both IPv4 and IPv6 addresses. |
   |**Network Type (IPv4)**  |The network type of the NLB instance's IPv4 address. Select **Internet**.<br><br><br>* **Internet**: This NLB instance can be accessed over both private and public IPv4 networks.<br><br>* **Private network**: This NLB instance can be accessed only over the private IPv4 network.<br><br><br>> **warning**<br><br><br>> The domain name of a public NLB instance resolves to the public IP address of the NLB instance, and the domain name of a private NLB instance resolves to the private IP address of the NLB instance.<br> |

5. After reviewing and confirming the relevant service agreements, click **Submit order** and wait for the instance status to change to **normal**.

6. Record the EIP of the NLB instance in the instance list.

### Step 3: Create an IP\-type server group and add backend servers

1. Log in to the [NLB console](https://console.byteplus.com/nlb).

2. In the top navigation pane, select the **project** and **region** that match the VMP workspace.

3. In the left navigation pane, select **Server Group**. Then, click **Create server group**.

4. Configure the key parameters as described in the table below and other parameters as needed. For more information about configuring parameters, see [Creating server groups](https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group).

   |Parameters |Description |**Recommended value for this scenario** |
   |---|---|---|
   |Name |Specify a custom name for the server group. |For example, vmp\-private\-link\-rsp |
   |Server group type |The type of the server group.<br><br><br>* **Server type**: Only ECS instances or auxiliary network interfaces within the same VPC as the server group can be added as backend servers.<br><br>* **IP\-type**: Only IP addresses can be added as backend servers. As long as the network is reachable, IP addresses within other VPCs or IDCs can be added as backend servers. |IP\-type |
   |IP version |The protocol type of the backend server's IP address in the VPC. Currently, only IPv4 type backend servers can be added. |IPv4 |
   |VPC |Select the VPC to which the server group belongs.<br><br>> **warning**<br><br><br>> The selected VPC must be the VPC where the PrivateLink endpoint created in **Step 1** and the NLB instance created in **Step 2** are located.<br> |\- |
   |Protocol |The communication protocol used by the NLB instance to forward traffic to backend servers.<br><br><br>* **TCP**: Only TCP and TLS listeners can be associated.<br><br>* **UDP**: Only UDP listeners can be associated. |TCP |
   |Scheduling algorithm |Select the rule for forwarding requests to the server group. For more details, see [Learn more](https://docs.byteplus.com/en/docs/clb/Server-Group-Overview).<br><br><br>* **Weighted Round Robin (WRR)** : Backend servers with higher weight values are polled more frequently (with higher probability).<br><br>* **Weighted Least Connections (WLC)** : Calculates the current connection count divided by the weight for each backend server, then forwards the request to the server with the lowest value.<br><br>* **Source Address Hash (SH)** : Uses consistent hashing based on the source IP address. Requests from the same source address are always routed to the same backend server. |Weighted Round Robin (WRR) |
   |All\-port forwarding |All\-port forwarding can be enabled when the service port of every backend server in the server group is the same as the listener port.<br><br>If this feature is enabled, the server group can only be associated with listeners that have all\-port listening enabled. You do not need to specify a port for backend servers in the group. NLB forwards traffic to the backend servers on the frontend request port (that is, the listening port) by default. |Disabled |
   |Health checks |Select whether to enable health checking. If this feature is enabled, NLB can determine whether backend servers are healthy, preventing requests from being forwarded to unhealthy backend servers and ensuring service availability. **Enable** this feature.<br><br>> **tip**<br><br><br><br>* > Disabling health checks may cause requests to be forwarded to unhealthy backend servers. To ensure continuous service availability, we recommend against disabling health checks.<br><br><br>* > Health checks consume a certain amount of network resources. We recommend that you reduce the impact on your service based on your business requirements, for example, by lowering the health check frequency or increasing the health check interval.<br> |Enable |
   |Health check protocol |The protocol for health check requests.<br><br><br>* **TCP**: Sends a SYN handshake packet to check whether the port of the backend server is functioning normally.<br><br>* **HTTP**: Sends a HEAD or GET request to simulate browser access behavior and check whether the application on the backend server is functioning normally. Parameters specific to the HTTP protocol are as follows:<br><br>   * **Health check method**: Selects the request method used to perform health checks on backend servers.<br><br>      * **GET**: A GET request returns both the response headers and the response body. This requires the server to support the GET method.<br><br>      * **HEAD**: A HEAD request returns only the response headers, reducing backend overhead. This requires the server to support the HEAD method.<br><br>   * **Health check domain name**: Enter the domain name for health check requests. This must be set to the address that the backend server actually uses to provide external\-facing services. If this parameter is not specified, the private IP address of the backend server is used by default.<br><br>   * **Health check path**: Enter the URL path for health check requests. This must be set to the address that the backend server actually uses to provide external\-facing services. If this parameter is not specified, the default is `/`.<br><br>   * **Health status code**: Configure the response code. If a response code of the selected type is received, the server is considered healthy and available.<br><br>* **UDP**: Sends ICMP or UDP probe packets to check whether the backend server is functioning normally. Parameters specific to the UDP protocol are as follows:<br><br><br>     Custom request/response: Specify whether to enable custom health check strings.<br><br><br>   * When this option is enabled, configure the following parameters:<br><br>      * **Custom request**: Enter the string for health check requests.<br><br>      * **Custom response**: Enter the string for health check responses.<br><br>   * When this option is disabled, no strings need to be specified.<br><br><br>[Learn more](https://docs.byteplus.com/en/docs/clb/NLB-Health-check-overview)<br><br>> **tip**<br><br><br>> When the backend protocol of a server group is TCP, the UDP protocol is not supported for health checks.<br> |TCP |
   |Health check port |Configure the port used for health checks.<br><br><br>* **Use the backend server port**: By default, the backend server port is used for health checks, and you do not need to additionally specify a port.<br><br>* **Specify a specific port**: If all\-port forwarding is enabled, you can select only this option. The port range is 1–65535. |Use the backend server port |
   |Response timeout |Configure the time to wait for a health check response.<br><br><br>* If no valid response is received from the backend server within the response timeout period, the health check is considered abnormal.<br><br>* The value range is 1–60 seconds. The default timeout is 3 seconds. |3 seconds |
   |Detect interval |Specify the time interval for performing health checks.<br><br><br>* The health check interval must be greater than or equal to the response timeout.<br><br>* The value range is 3–300 seconds. The default interval is 10 seconds, meaning a health check is performed on the backend server every 10 seconds. |10 seconds |
   |Healthy threshold |After you enable health checking, enter the number of health checks required to determine that the backend server is functioning normally.<br><br><br>* When the specified number of consecutive health checks are performed on the same backend server and all results are **normal**, the health check status changes from **abnormal** to **normal**.<br><br>* The value range is 2 to 10. The default value is 3. |3 times |
   |Unhealthy threshold |After you enable health checking, enter the number of health check attempts required to determine that a backend server is unhealthy.<br><br><br>* If the specified number of health checks are performed consecutively on the same backend server and all results are **abnormal**, the health check status changes from **normal** to **abnormal**.<br><br>* The value range is 2 to 10. The default value is 3. |3 times |

5. Click **Confirm** to complete creation.

6. Click the name of the created server group, switch to the **Server** tab, click **Add server**, and configure parameters.

   |Parameters |Description |
   |---|---|
   |IP address |Enter the IP address of the backend server. Enter the private IP address of the endpoint network interface recorded in **Step 1**.<br><br>> **tip**<br><br><br>> If two endpoints (read and write) are created in a read/write separation scenario, add them separately.<br> |
   |Availability zone |Select the availability zones from which this backend server can receive requests. |
   |Port |The port on the backend server. Enter **8088**. |
   |Weight |The probability that the backend server receives a request (the probability is the weight of this IP address divided by the total weight of all IP addresses in the group). Keep the default value of **100**.<br><br><br>* The larger the weight, the more requests are forwarded to the backend server. The default is 100.<br><br>* If the weight is set to 0, this server will no longer accept new requests.<br><br>* When the listener scheduling algorithm is Source Address Hash (SH), the weight is only 0 or non\-zero. |

7. Click **Confirm**. Confirm that the status of the server group in the server list is **normal**.

### Step 4: Add a TCP listener and associate the server group

1. Log in to the [NLB console](https://console.byteplus.com/nlb/region:nlb+cn-beijing/LoadBalancer).

2. In the top navigation pane, select the **project** and **region** that match the VMP workspace.

3. In the left navigation pane, select **Instances**. Find the NLB instance created in **Step 2** and click **Edit listener** on the right side.

4. Click **Add listener**. Configure the key parameters as described in the table below and other parameters as needed. For more information about configuring parameters, see [Adding a listener](https://docs.byteplus.com/en/docs/clb/NLB-Adding-a-listener).

   |Parameters |Description |**Recommended value for this scenario** |
   |---|---|---|
   |Listener name |Enter the name of the listener. |The default naming format is "protocol\-port" (for example, TCP\-8080). |
   |Listening Protocol |Select the protocol type for the listener of the NLB instance. |**TCP**. |
   |Listening port |Enter the listening port. The range is 1–65535.<br><br><br>* Listen on a single port: Enter a single port. When the listener detects a TCP request on this port, it replaces the destination IP address and port in the request with the backend server's IP address and port, and forwards the request to the backend server.<br><br>* Listen on all ports: Enter the port range. When the listener detects a TCP request within this port range, it replaces the destination IP address in the request with the backend server's IP address and forwards the request to the backend server. |**8080** (consistent with the endpoint port). |
   |Timeout period |Set the timeout. If no data is transmitted within the timeout period, the connection is automatically closed.<br><br>The timeout for the TCP listener is 10 to 900 seconds, with a default of 900 seconds. |900 seconds. |
   |New connection rate limit / Max connections |Whether to enable new connection rate limiting.<br><br>When this option is enabled, enter a rate limit value:<br><br><br>* Valid values are 0 to 1000000. A value of 0 indicates no limit.<br><br>* When the number of new connections captured by this listener exceeds the configured limit, the excess connections are dropped and are not forwarded to backend servers. |Disabled<br><br> |

5. Click **Next**. In the **Select server group** step, select the IP\-type server group created in **Step 3**.

6. Click **Next**. Verify the configuration and click **Confirm** to create the listener.

7. After creation, go to the listener details page to confirm that the associated server group's health check status is **normal**.

### Step 5: Configure DNS domain resolution

1. Log in to the DNS service provider console you use (such as BytePlus Cloud DNS or other third\-party DNS).

2. Add an **A record** for the workspace's public domain and set the record's value to the **NLB's EIP address** recorded in **Step 2**.

3. Wait for the DNS setting to take effect globally (this takes approximately 1–10 minutes).

## Verify connectivity

1. **NLB instance status:**  Confirm that the instance status is **Running** and the listener status is **Normal**.

2. **Health check result:**  On the details page of the backend server group corresponding to the listener, confirm that the backend IP address (the private IP address of the endpoint) is **normal**.

3. **DNS resolution:**  Run `nslookup on the workspace's public domain name` on your local machine and confirm that the resolution result is the EIP of the NLB instance.

4. **End\-to\-end access:**  Remote users access the NLB via `http://<public IP or domain name>:8080`, and the NLB transparently passes the requests through to the workspace. Use the path formats provided in the table below to verify both the query (read) and Remote Write (write) paths separately:

   |**Purpose** |**Complete URL** |**Verification method** |Description |
   |---|---|---|---|
   |Query (read) |http://<public IP or domain name\>:8080/workspaces/b73\*\*\*/api/v1/query |Access via a browser or curl with BasicAuth should return the PromQL query result as JSON. |* Replace "public IP or domain name" with the NLB's EIP recorded in **Step 2**.<br><br>* Replace "b73\*\*\*" with the ID of the VMP workspace.<br><br>* The protocol is **HTTP** and the port is **8080**.<br><br>* In a read/write separation scenario, queries and writes must point to the backend IP associated with the corresponding Readonly/Writeonly endpoint, respectively.<br><br><br> |
   |Remote Write (write) |http://<Public IP or domain name\>:8080/workspaces/b73\*\*\*/api/v1/write |The Remote Write address in the collector (Prometheus / Agent) configuration should point to this URL, and samples can be written successfully. ||
