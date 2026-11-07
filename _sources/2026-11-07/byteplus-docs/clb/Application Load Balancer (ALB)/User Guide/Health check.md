---
title: "Health check"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-Health-check"
---

This topic describes how to Create, Modify, and Delete health check templates in the BytePlus Application Load Balancer (ALB) console.

## ALB health check

* Health check is a crucial feature for ensuring application availability. ALB verifies whether backend servers can accept new requests by periodically performing health checks on them. When a backend server fails to respond correctly to ALB's health check requests, client traffic is not routed to that server. Instead, ALB forwards traffic to other servers in a normal state. This ensures service continuity and reliability.

* ALB health checks are performed at the server group level. After enabling health checks for a server group, ALB periodically checks the status of the backend servers within it.

### ALB health check process

You can choose whether to enable health checks for a server group when [Creating server groups and adding backend servers](https://docs.byteplus.com/docs/clb/ALB-Creating-a-server-group). After enabling health checks:

1. Based on the detection interval you set, ALB sends health check requests to each backend server in the server group.

2. If a backend server responds correctly to a health check request, that specific health check attempt for the server is considered successful.

   * When the number of consecutive successful health check requests meets the healthy threshold you set, the server is marked as normal. Client traffic can then be routed to this server.

3. If a backend server fails to respond within the response timeout period you set, or returns an incorrect status code, that specific health check attempt for the server is considered failed.

   * When the number of consecutive failed health check requests meets the unhealthy threshold you set, the server is marked as abnormal. ALB will not route client traffic to this server.

   * ALB will only forward new traffic to this server again after it is once more determined to be normal.

### TCP and HTTP health checks

ALB provides TCP and HTTP health checks.

* **TCP health check**: ALB checks the status of backend servers by sending SYN packets and verifying their SYN\-ACK responses, a process based on the TCP connection establishment mechanism.

* **HTTP health check**: ALB sends HTTP requests to backend servers and verifies their status based on response times and returned status codes.

## Create health check template

ALB provides the health check template feature, allowing you to create templates containing different health check configurations. When configuring health checks for a server group, you can directly select a health check template to complete the setup quickly and conveniently.

### Procedures

#### HTTP health check

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left\-side navigation pane, select **Health check**.

3. Click **Create health check template**.

4. Configure relevant parameters based on the table below.

   |Parameter |Required |Explanation |
   |---|---|---|
   |Name |Yes |Enter a health check template name. |
   |Health check protocol |Yes |HTTP health check protocol. |
   |Health check port |Yes |By default, the port of the backend server is used for health checks. Allowed ports for health checks:<br><br><br>* `Backend server port` (default).<br><br>* `Specify a specific port`. |
   |Protocol version |Yes |Specify the protocol version for health checks. Supports HTTP1.0 and HTTP1.1. Default: HTTP1.0. |
   |Health check method |No |Specifies the request method used for health checks. The following methods can be specified:<br><br><br>* GET: A GET request yields a response that includes both response headers and a response body.<br><br>* HEAD: A HEAD request yields a response that includes only response headers, not a response body. |
   |Health check domain |No |Enter the domain name of the health check request. Input rules are as follows:<br><br><br>* Only English letters, numbers, half\-width periods (.), and hyphens (\-) are allowed.<br><br>* Must contain at least one half\-width period (.), but cannot begin or end with a half\-width period (.). Each level of the domain name cannot start or end with a hyphen (\-).<br><br>* A maximum of 128 characters is allowed.<br><br>* Must be an exact domain name that complies with domain name specifications, e.g., www.test.com. Wildcard domain names are currently not supported.<br><br><br>> **warning**<br><br><br><br>* > When the protocol version is **HTTP/1.0**: If you do not specify a domain name, ALB uses the backend server's private IP address as the destination for health checks. However, the health check request will not include a Host header.<br><br><br>* > When the protocol version is **HTTP/1.1**: If you do not specify a domain name, ALB uses the backend server's private IP address as the destination for health checks and uses this IP address as the value for the Host header in the health check request.<br> |
   |Health check path |No |* Enter the path for health checks. The default value is the forward slash `/`, which indicates the root directory.<br><br>* The specific rules are as follows:<br><br>   * Must start with a forward slash (`/`).<br><br>   * Length must be 1 to 128 characters.<br><br>   * Only letters, numbers, `-`, `_`, `/`, `.`, `%`, `?`, `#`, `&`, and `=` are allowed. |
   |Health status code |Yes |* Specifies which response status codes are considered successful health check results. Multiple selections are supported.<br><br>* You must select at least one set of normal status codes. A health check request is only considered successful when the backend server returns a normal status code.<br><br><br>> **warning**<br><br><br><br>* > Please select the status codes according to your business needs. All status codes you select will be treated as normal. The ALB can only consider a health check successful if the backend server returns a normal status code.<br><br><br>* > The ALB allows you to set `2XX` (default), `3XX` (default), `4XX`, and `5XX` as normal status codes.<br><br><br>* > For example: If you have not selected 4xx status codes, ALB will consider the health check request as failed when the backend server returns a 4xx status code. If health check requests fail consecutively, that backend server will be isolated. Traffic will not be routed to this server until its status returns to normal.<br> |
   |Response timeout |No |The maximum time to wait for a health check response.<br><br><br>* If the backend server does not respond correctly within the specified time, the health check will be marked as abnormal.<br><br>* The default system response timeout is 2 seconds. The configurable timeout range is 1 to 60 seconds. |
   |Detect interval |No |The time interval between initiating health check requests.<br><br><br>* The default interval is 2 seconds, meaning a health check is performed on the backend server every 2 seconds.<br><br>* Please set this interval reasonably to avoid placing excessive burden on backend servers with health check requests. The configurable range is 1 to 300 seconds. |
   |Healthy threshold |No |The number of consecutive successful health check requests used by the system to determine if a backend server is normal.<br><br><br>* The default healthy threshold is 3 times, meaning a backend server is marked as normal only after 3 consecutive successful health check requests.<br><br>* The configurable range for the healthy threshold is 2 to 10 times. |
   |Unhealthy threshold |No |The number of consecutive failed health check requests used by the system to determine if a backend server is abnormal.<br><br><br>* The default unhealthy threshold is 3 times, meaning a backend server is marked as abnormal only after 3 consecutive health check request failures.<br><br>* The configurable range for the unhealthy threshold is 2 to 10 times. |
   |Description |No |Enter the description for a template. The specific rules are as follows:<br><br><br>* The length is limited to 255 characters<br><br>* Must start with a letter or Chinese character<br><br>* Can only contain Chinese characters, letters, numbers, half\-width comma `,`, period `.`, underline `_`, space, equal sign `=`, hyphen `-`, full\-width comma `，`, and full\-width period `。`. |
   |Project |No |Select a project for the health check template. A Project is a resource management method provided by BytePlus. Using projects, you can group and manage your cloud resources.<br><br>If you do not select a project, the health check template will be added to the **default** project by default. |
   |Tags |No |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the add icon, enter the tag key and tag value, and add a tag for the health check template. |

   ####

5. Click Create to complete the action.

#### TCP health check

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left\-side navigation pane, select **Health check**.

3. Click **Create health check template**.

4. Configure relevant parameters based on the table below.

   |Parameter |Required |Explanation |
   |---|---|---|
   |Name |Yes |Enter a health check template name. |
   |Health check protocol |Yes |TCP health check protocol. |
   |Health check port |Yes |By default, the port of the backend server is used for health checks. Allowed ports for health checks:<br><br><br>* `Backend server port` (default).<br><br>* `Specify a specific port`. |
   |Response timeout |No |The maximum time to wait for a health check response.<br><br><br>* If the backend server does not respond correctly within the specified time, the health check will be marked as abnormal.<br><br>* The default system response timeout is 2 seconds. The configurable timeout range is 1 to 60 seconds. |
   |Detect interval |No |The time interval between initiating health check requests.<br><br><br>* The default interval is 2 seconds, meaning a health check is performed on the backend server every 2 seconds.<br><br>* Please set this interval reasonably to avoid placing excessive burden on backend servers with health check requests. The configurable range is 1 to 300 seconds. |
   |Healthy threshold |No |The number of consecutive successful health check requests used by the system to determine if a backend server is normal.<br><br><br>* The default healthy threshold is 3 times, meaning a backend server is marked as normal only after 3 consecutive successful health check requests.<br><br>* The configurable range for the healthy threshold is 2 to 10 times. |
   |Unhealthy threshold |No |The number of consecutive failed health check requests used by the system to determine if a backend server is abnormal.<br><br><br>* The default unhealthy threshold is 3 times, meaning a backend server is marked as abnormal only after 3 consecutive health check request failures.<br><br>* The configurable range for the unhealthy threshold is 2 to 10 times. |
   |Description |No |Enter the description for a template. The specific rules are as follows:<br><br><br>* The length is limited to 255 characters.<br><br>* It must start with a letter or Chinese character.<br><br>* Can only contain Chinese characters, letters, numbers, half\-width comma `,`, period `.`, underline `_`, space, equal sign `=`, hyphen `-`, full\-width comma `，`, and full\-width period `。`. |
   |Project |No |Select a project for the health check template. A Project is a resource management method provided by BytePlus. Using projects, you can group and manage your cloud resources.<br><br>If you do not select a project, the health check template will be added to the **default** project by default. |
   |Tags |No |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the add icon, enter the tag key and tag value, and add a tag for the health check template. |

5. Click **Create** to complete the action.

## View server health check status

ALB health checks are performed at the server group level. Server groups are associated with listeners under an instance.

* On the **Instances** page, you can view the number of listeners with abnormal health checks under a specific ALB instance.

* On the **Listeners** tab of a specific instance, you can view the status of backend servers associated with different listeners. Health check status is as follows:

   * Not Enabled: The listener is associated with server groups, but health checks are not enabled for any of those groups.

   * No Targets: The listener is associated with server groups, but there are no backend servers within any of those groups.

   * Normal: The listener is associated with server groups, and the health checks for all backend servers within those groups are normal.

   * n abnormal: The listener is associated with server groups, and this indicates the total number of backend servers across all groups with abnormal health checks.

      > **tip**

      * > In the **Check Status** column, click on **exception** allows you to view detailed information about the abnormal backend servers.

      * > For backend servers with failed health checks, please first check whether the security group rules of the backend server have allowed access for the CIDR block `100.64.0.0/10`. If health checks remain abnormal even after the relevant ports are open, please check the internal routing configuration of the backend servers.

## Modify health check template

### Procedures

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left\-side navigation pane, select **Health check**.

3. Click **Edit** to the right of the target health check template.

4. Modify the health template parameters as needed.

5. Click **Confirm** to complete the action.

> **tip**

> After you modify a template, if you need to apply it to a backend server group, you can reselect this template in the server group's configuration.

## Delete health check template

If you no longer need a health check template, you can consider deleting it. Deleting a template does **not affect** the operational status of health checks for server groups. Server groups will continue to run health checks based on their current configuration until the health check settings on the server group are changed next time.

### Procedures

1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the left\-side navigation pane, select **Health check**.

3. Click **Delete** to the right of the target health check template.

4. Click **Delete** to complete the action.
