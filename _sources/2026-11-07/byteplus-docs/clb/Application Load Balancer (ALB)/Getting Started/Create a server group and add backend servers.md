---
title: "Create a server group and add backend servers"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-Creating-a-server-group"
---

A server group is a collection of backend servers. After creating a server group, you can attach it to any listener of an ALB instance within the same VPC.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ALB allows you to configure and manage server groups. For more details, refer to <a href="https://docs.byteplus.com/docs/clb/Managing-server-groups">Creating and Managing Server Groups</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Application Load Balancer console](https://console.byteplus.com/alb).

2. Click **Server Group** in the left navigation pane to open the **Server Group** page.

3. On the **Server Group** page, click **Create backend server group**.

4. On the **Create backend server group** tab, configure as shown below. See [Create server group](https://docs.byteplus.com/docs/clb/ALB-Creating-a-server-group#.5Yib5bu65ZCO56uv5pyN5Yqh5Zmo57uE) for details.

5. After completing the configuration on the **Create server group** tab, click **Confirmed** to successfully create the server group.

6. On the **server group** page, select the newly created server group and click **Add backend server** in the action bar.

7. On the **Add backend server** tab, select the backend servers to add, then click **Next to configure port and weight**.

8. On the **Configure port and weight** tab, enter the server ports and assign weights according to the actual situation, then click **Confirmed** to finish adding backend servers to the server group.


<span id=".5a2X5q616K-05piO"></span>
## Field description

<span id=".5Yib5bu65ZCO56uv5pyN5Yqh5Zmo57uE"></span>
### Create server group

For the [Getting started](https://docs.byteplus.com/docs/clb/ALB-quick-start-Overview) scenario, you can configure the server group and backend servers with reference to the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details on creating and deleting server groups, see <a href="https://docs.byteplus.com/docs/clb/Managing-server-groups">Manage server groups</a>.</div>



|**Configuration fields** |**Required** |**Explanation** |
|---|---|---|
|Server Group Type |Yes |* You need to select the type of server group to create.<br><br>* In this example, the server group type is `server group type`. |
|Name |Yes |* You need to name the created server group for easier management.<br><br>* In this example, the name is `alb1group1`. |
|VPC |Yes |* You need to select a VPC for the server group, which is also the VPC of the ALB instance to be associated.<br><br>* In this example, the Virtual Private Cloud is `ALB-**-VPC2`. |
|Scheduling algorithm |Yes |* You need to specify the algorithm that controls traffic distribution among different backend servers within the server group.<br><br>* In this example, the routing algorithm is `Weighted Round Robin (WRR)`. The higher the weight you assign to a backend server, the more frequently (probability) it is polled. |
|Backend communication protocol |Yes |* You need to specify the communication protocol between the ALB and the backend server group.<br><br>* In this example, the backend communication protocol is `HTTP`. |
|Health check |No |* If you enable Health Check, after the server group is attached to the ALB instance, ALB will send health check requests to the backend servers in the server group based on your specified rules to monitor their Health status. You can choose an existing health check template or set a custom health check to configure a Health Check policy for the server group.<br><br>* In this example, you enable Health Check configuration and choose a custom health check. Details are as follows:<br><br>   * Protocol: In this example, the protocol is `HTTP`. You can select `HTTP` (default) or `TCP`.<br><br>   * Health Check port: In this example, the port is `Use the backend server port`. You can select `Use the backend server port` (default) or `Specify a specific port`.<br><br>   * Protocol version: In this example, the protocol version is `HTTP1.0`. Protocol version can only be selected when the protocol is `HTTP`. You can choose `HTTP1.1` (default) or `HTTP1.0`.<br><br>   * health check method: in this example, the method is `HEAD`. you can select the health check method only when the protocol is `HTTP`. you can choose `GET` or `HEAD` (default).<br><br>   * health check domain name: in this example, no domain name is entered; the ALB uses the backend server's private IP as the health check target address. you can enter a domain name as the health check target address only when the protocol is `HTTP`.<br><br>      * when the protocol version is `HTTP1.0`, leave blank by default; the ALB uses the backend server's private IP as the health check target address.<br><br>      * when the protocol version is `HTTP1.1`, you must enter a health check domain name.<br><br>   * health check path: in this example, the path is`/`。 you can set the health check path only when the protocol is `HTTP`. ALB uses by default`/`as the health check path.<br><br>   * Normal status code: in this example, the `2XX` status code is considered normal. Only when the protocol is `HTTP` can you set the normal status code.<br><br>      * ALB considers the health check successful only if the backend server returns a normal status code.<br><br>      * ALB allows you to set `2XX` (default), `3XX` (default), `4XX`, and `5XX` as normal status codes.<br><br>   * Response timeout: in this example, the timeout period is`2`s。 If the backend server does not respond correctly within 2s, ALB considers the health check failed.<br><br>   * Detect interval: in this example, the detection interval is`2`s。 Every 2 seconds, the ALB sends a health check request to the backend server.<br><br>   * Healthy threshold: In this example, the healthy threshold is`3`times. The ALB considers the backend server healthy only after 3 consecutive successful health checks.<br><br>   * Unhealthy threshold: In this example, the unhealthy threshold is`3`times. The ALB considers the backend server unhealthy only after 3 consecutive failed health checks. |
|Session Persistence |No |* This feature is not enabled in this example.<br><br>* After you enable cookie\-based session persistence, the ALB can forward requests from the same client to the same backend server. |
|Description |No |* You can add a description to the created server group.<br><br>* No description is added in this example. |
|Project |No |* A project is a unit used by BytePlus to manage cloud resources. Through projects, you can centrally manage cloud resources. For more information, see [Use projects to manage ALB resources](https://docs.byteplus.com/docs/clb/Using-projects-to-manage-ALB-resources).<br><br>* This example is `default`, indicating that this server group belongs to the default project. |
|Tag |No |* A tag consists of a key\-value pair used to mark resources for easier search and aggregation. You can select tags for the server group here or enter the tag key and tag value directly. For more project information, see [Use tags to manage ALB resources](https://docs.byteplus.com/docs/clb/Using-tags-to-manage-ALB-resources).<br><br>* This example does not add tags to the server group. |


<span id=".5re75Yqg5ZCO56uv5pyN5Yqh5Zmo"></span>
### Add backend server


|**Field** |**Explanation** |
|---|---|
|Port |* In this example, the ports of the two backend servers you added are both 8080.<br><br>* Port range is 1 to 65535. |
|Weight |* The weight value for both backend servers in this example is 100.<br><br>* A higher weight value means more requests are forwarded to this backend server.<br><br>* The default weight value is 100, and it must be an integer between 0 and 100. If the weight value is 0, the backend server will no longer receive new requests.<br><br>* After you configure the weight for a backend server, the weight proportion for that backend server = its weight value divided by the total weight values of all backend servers in the server group. The weight proportion for both backend servers in this example is: 100 / (100 + 100) = 50%.<br><br>* If you set the routing algorithm of the server group to `Source Address Hash`, the weight value you set will be ignored. ALB does not forward traffic based on the weight values you set for backend servers. |
|Copy |* This example does not use this feature.<br><br>* You can copy to a specific backend server. After copying, select a different port for that server. This allows the server to receive traffic using different ports you configured. |
|Remove |* This example does not use this feature.<br><br>* You can directly remove backend servers added in the server group. |
