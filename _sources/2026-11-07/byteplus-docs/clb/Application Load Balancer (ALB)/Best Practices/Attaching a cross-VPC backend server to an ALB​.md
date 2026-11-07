---
title: "Attaching a cross-VPC backend server to an ALB​"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Mounting-back-end-servers-to-an-ALB-instance-across-VPCs"
---

Application Load Balancer (ALB) supports attaching cross\-VPC backend servers. This topic guides you to configure forwarding route information in the ALB console and Transit Router (TR) console, enabling ALB to forward client requests to backend servers in other Virtual Private Clouds (VPCs).

<span id=".56S65L6L5Zy65pmv"></span>
## Example scenarios

This diagram shows an ALB configured with cross\-VPC backend servers Company A created a public ALB instance (named alb\-01) in China (Beijing) on BytePlus. This ALB instance (alb\-01) resides in VPC1. At the same time, Company A created an Elastic Compute Service (ECS) instance (named ecs\-02) in China (Beijing). This ECS instance (ecs\-02) resides in VPC2. Company A requires that alb\-01 in VPC1 can forward client requests to ecs\-02 in VPC2. Company A can interconnect alb\-01 in VPC1 with ecs\-02 in VPC2 through a TR.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_291657a5b7d2c94186062a032ca52235.png) </span>


|Region |Instance |VPC |Subnet CIDR block |
|---|---|---|---|
|China (Beijing) |ALB instance (alb\-01) |VPC1 |172.16.0.0/12 |
||ECS instance (ecs\-02) |VPC2 |192.168.0.0/24 |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created an ECS instance (ecs\-01) in VPC1 to send requests.

* You have created an ALB instance (alb\-01) in VPC1 to forward requests from ecs\-01.

* You have created an ECS instance (ecs\-02) in VPC2 with deployed services to process requests.

* You have [created a TR instance](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01) (tr\-1) in China (Beijing).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This scenario serves as an example. Adapt the information according to your actual plan during configuration.</div>


* <div data-tips="true" data-tips-type="tip">The subnet CIDR block of alb\-01 in VPC1 must not overlap with that of ecs\-02 in VPC2.</div>


* <div data-tips="true" data-tips-type="tip">To use the TR service, please contact your account manager.</div>



<span id=".6YWN572u5q2l6aqk"></span>
## Configuration procedure

The procedure for the above example scenario is as follows:


|Step |Action |Specific content |
|---|---|---|
|1 |Create an IP\-type server group |You need to create an IP\-type server group. |
|2 |Add an IP\-type backend server |You need to enable remote IP and add the IP address of the cross\-VPC backend server. |
|3 |Configure a listener |You need to configure a listener for the created ALB instance and set the IP\-type server group as the default server group. |
|4 |Configure a TR |* You need to create two network instance attachments for tr\-1 via the TR console. Respectively attach tr\-1 to the ALB instance of VPC1 and esc\-02 of VPC2.<br><br>* You need to configure back\-to\-source routing for tr\-1 via the TR console. When the destination CIDR block of the TR is the ALB's back\-to\-source address, the next hop of the route is VPC1. |
|5 |Configure routing for VPC |You need to configure routing for the target route tables of VPC1 and VPC2 in the VPC console. |
|6 |Test network connectivity |You can verify network connectivity between ecs\-01 and ALB via `curl`, and verify service availability by accessing ALB through a local internet client. |


<span id=".5q2l6aqkMe-8muWIm-W7ui1pcC3nsbvlnovmnI3liqHlmajnu4Q="></span>
### Step 1: Create an IP\-type server group


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Server group**.

4. Click **Create backend server group**.

5. In the **Create server group** tab, set the server group type to IP type. Select your created VPC1 in the VPC field. In this example, the server group is named TEST with Weighted Round Robin (WRR) selected and other features disabled. For more information, see the configuration description in [Creating a server group](https://docs.byteplus.com/en/docs/clb/Managing-server-groups).

6. After completing the relevant configuration in the **Create server group** tab, click **Save** to successfully create the IP\-type server group (TEST).


<span id=".5q2l6aqkMu-8mua3u-WKoC1pcC3nsbvlnovlkI7nq6_mnI3liqHlmag="></span>
### Step 2: Add an IP\-type backend server


1. On the **Server group** page, locate the new IP\-type server group (TEST).

2. In the **Actions** column, click **Add backend server**.

3. On the **Add IP address** page, the VPC ID and CIDR block of the server group (TEST) are displayed. Enter the IP address of ecs\-02 in VPC2, and turn on the switch in the Remote IP column. Set the port to 8002 and the weight to 100.

4. Click **OK** to complete adding the IP\-type backend server (ecs\-02) to the server group (TEST).


<span id=".5q2l6aqkM--8mumFjee9ruebkeWQrOWZqA=="></span>
### Step 3: Configure a listener


1. On the **Instance management** page, locate the new ALB instance (alb\-01).

2. In the **Actions** column, click **Listener**.

3. In the **Listener information** tab, click **Add listener**.

4. On the **Add listener** page, set the name to TEST\-01, the listening protocol to HTTP, and the listening port to 8002. Then click **Next: default backend server group**.

5. In the **Default server group** tab, select the server group (TEST) from the dropdown, then click **Next: confirm the configuration**.

6. After confirming the listener's configuration is correct, click **Save** to complete adding the listener.


<span id=".5q2l6aqkNO-8mumFjee9ruS4rei9rOi3r-eUseWZqA=="></span>
### Step 4: Configure a TR

Configure a TR instance (tr\-1) based on the [Creating a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc) section of the Transit Router official documentation. Create two network instance attachments for tr\-1 to connect VPC1 and VPC2 separately.


1.  Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name (tr\-1) of the TR instance to enter its details page.

3. In the **Intra\-region attachment** tab below **Basic information**, click **Create attachment** to redirect to the **Create attachment** page, and respectively configure two attachments based on the table below.

   
   |Parameter ||Value (Network instance attachment 1) |Value (Network instance attachment 2) |
   |---|---|---|---|
   |**Basic Information** |TR |tr\-1 |tr\-1 |
   ||Region |China (Beijing) |China (Beijing) |
   ||Name |netlink\-01 |netlink\-02 |
   |**Network instance** |Attachment type |VPC |VPC |
   ||VPC |VPC1 |VPC2 |
   |**Attachment point configuration** |Availability Zone and Subnet |Availability Zone A, subnet\-01 |Availability Zone A, subnet\-02 |
   |**Route configuration** |Association forwarding |Enabled, tr\-systemrtb |Enabled, tr\-systemrtb |
   ||Route learning |Enabled, tr\-systemrtb |Enabled, tr\-systemrtb |
   

4. Click **Buy now**.

5. Click the **Route Table** tab, then click the target route table (tr\-systemrtb).

6. On the right section of the tab, click **Create static route** and configure routing based on the table below.



|Field |Description |
|---|---|
|Route name |trentry\-01 |
|Destination CIDR |100.127.238.0/23 is the back\-to\-source address of this ALB instance in China (Beijing). Adapt the back\-to\-source address according to your actual configuration. You can view the back\-to\-source address of this ALB instance on the **Detail** page of the ALB console.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the back\-to\-source address is not displayed, please contact your account manager to enable the IP\-type server group feature.</div><br> |
|Blackhole routing |No |
|Next Hop type |Intra\-region attachment |
|Next Hop |VPC1 |


<span id=".5q2l6aqkNe-8mumFjee9rnZwY-i3r-eUseS_oeaBrw=="></span>
### Step 5: Configure routing for VPC

Configure routing for the target route tables of VPC1 and VPC2 based on the [Route Table Overview](https://docs.byteplus.com/en/docs/vpc/Route-table-overview) section of the Virtual Private Cloud official documentation.


* Add a custom route entry to the target route table of VPC1, with the destination CIDR block set to the CIDR block of the backend server (ecs\-02) and the next hop set to the TR. When the destination CIDR block is VPC2, the request routes to the TR.

* Configure the ALB's back\-to\-source address in the system route table of VPC2. When the destination CIDR block is the ALB's back\-to\-source address, the response routes back to the TR.

1. Log in to [the Route Table console](https://console.byteplus.com/vpc/routeTable).

2. In the top menu bar, select the region for the target VPC: China (Beijing).

3. In the route table list, click the name of the target route table.

4. In the **Route entry** tab of the details page, select **Custom route**.

5. Click **Add route** and configure the custom route according to the prompts.



|Field |VPC1 |VPC2 |
|---|---|---|
|Destination CIDR |192.168.0.0/24 |100.127.222.0/23 |
|Next Hop type |TR |TR |
|Next Hop |tr\-1 |tr\-1 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">192.168.0.0/24 is the CIDR block where the backend server (ecs\-02) resides. Adapt the destination CIDR block according to your actual requirements.</div>


* <div data-tips="true" data-tips-type="tip">100.127.222.0/23 is the back\-to\-source address of this ALB instance in China (Beijing). Adapt the back\-to\-source address according to your actual configuration. You can view the back\-to\-source address of this ALB instance on the <strong>Detail</strong> page of the ALB console. If the back\-to\-source address is not displayed, please contact your account manager to enable the IP\-type server group feature.</div>



<span id=".5q2l6aqkNu-8mua1i-ivlee9kee7nOi_numAmuaApw=="></span>
### Step 6: Test network connectivity


1. Log in to ecs\-01. For procedure, see [Logging on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Logging on to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Run the `curl` command to connect to the private IP address of alb\-01 to test network connectivity.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_250d351f58a61d65ff55ad93cb563d58.png) </span>

3. On a local client with internet access, browse to http:// alb\-01's elastic IP address. The backend service interface configured on ecs\-02 is displayed. This confirms that the request was successfully forwarded by the ALB instance to the backend server (ecs\-02), which processed the request correctly and returned the page.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


1. When attaching a cross\-VPC backend server, the subnet CIDR block of this ALB instance must not overlap with that of the backend server.

2. Within the same region, you can only attach backend servers from other VPCs to an ALB instance residing in a single, specified VPC. The VPC can host one or more ALB instances with cross\-VPC backends.

3. An ALB instance must not serve as the backend for another ALB instance in the same region.


&nbsp;
