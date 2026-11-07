---
title: "Implementing IPv4+IPv6 traffic load balancing via ALB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-achieves-load-balancing-of-IPv4-IPv6-traffic"
---

This topic describes how to configure a dual\-stack Application Load Balancer (ALB) instance to handle IPv4 and IPv6 traffic. By following the procedure in this topic, your dual\-stack ALB instance can forward IPv4 and IPv6 traffic to backend servers, enabling IPv6 network clients to access backend services.

<span id="197d82f9"></span>
## Scenarios

Your service needs to use ALB to forward requests from IPv6 clients, allowing them to access backend servers through ALB.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d2068c9f2831bbf16d9b7545caa1e804.png) </span>

<span id="e26c2096"></span>
## Prerequisites

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* Your VPC has IPv6 enabled, allowing IPv6 private traffic communication among different resources within the same VPC. For details, see [Building an IPv4&IPv6 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv6-VPC).

* You have enabled access to resources within the VPC over IPv6 Internet by configuring an IPv6 gateway. For details, see [Configure an IPv6 gateway for IPv6 Internet access](https://docs.byteplus.com/en/docs/IPv6/Configure_an_IPv6_gateway_to_access_the_IPv6_public_network).


<span id="b3cf4a6f"></span>
## Procedure

<span id="15c92161"></span>
### Step 1: Create an IPv6 ECS\-01 as the simulated client and an IPv4 ECS\-02 as the backend server.


1. Create an IPv6 Elastic Compute Service (named ECS\-01) to simulate IPv6 client access.

2. Create an IPv4 ECS (named ECS\-02). Use ECS\-02 as a backend server to receive traffic from the ALB. For details, see [Purchasing and using ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).

3. Configure a security group rule for ECS\-02 to allow Port 80, enabling inbound requests from the ALB. Allow the service network CIDR block `(100.64.0.0/10)` in the security group. For configuration, see [Configuring security groups of backend servers](https://docs.byteplus.com/docs/clb/Allowing-ALB-to-access-back-end-servers)​​. Deploy the Nginx service on ECS\-02.

   ```Bash
   yum install -y nginx && systemctl start nginx && systemctl status nginx && cd /usr/share/nginx/html/ && echo "Hello World! this is ipv4 rs." > index.html
   ```
   


<span id="8ddd57bb"></span>
### Step 2: Configure an IPv6 gateway for the VPC where the ALB resides to enable access to Internet.


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc) and enable IPv6 for the VPC where the ALB resides.

2. Log in to the [Subnet console](https://console.byteplus.com/vpc/subnet) see [Enabling/disabling IPv6 for subnet](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-IPv6-for-a-subunet), and enable IPv6 and assign IPv6 CIDR blocks to the availability zones corresponding to different subnets in the VPC of the ECS.

   Assign IPV6 CIDR blocks to different availability zones of the ALB:


<span id="ba511096"></span>
### Step 3: Create an IPv4&IPv6 dual\-stack instance to receive client's IPv4 and IPv6 traffic.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This ALB instance resides the same VPC as ECS\-02.</div>


* <div data-tips="true" data-tips-type="warning">IPv6 is enabled for the availability zone of this ALB instance.</div>


* <div data-tips="true" data-tips-type="warning">Private IPv4&IPv6 dual\-stack ALB instances cannot receive internet traffic. Public IPv4&IPv6 dual\-stack instances automatically activate IPv6 Internet bandwidth during creation, and can receive internet traffic from both IPv4 and IPv6.</div>



Log in to the [ALB console](https://console.byteplus.com/alb) and complete the following actions.


1. Create a public IPv4&IPv6 dual\-stack instance based on [Creating an ALB instance](https://docs.byteplus.com/docs/clb/Creating-an-instance).

2. Create a server group and add the backend server (ECS\-02) to it based on [Creating a server group and adding backend servers](https://docs.byteplus.com/docs/clb/ALB-Creating-a-server-group).

3. Configure listener for the dual\-stack instance based on [Creating an HTTP listener](https://docs.byteplus.com/docs/clb/ALB-Creating-an-HTTP-listener).

4. Obtain the domain name of the ALB instance based on [Adding a CNAME record pointing to an instance domain name](https://docs.byteplus.com/docs/clb/Configuring-domain-name-resolution). In the domain console, configure DNS resolution to point your service domain to the ALB instance via CNAME. This provides a more simplified way to access network resources through the instance domain.


<span id="4d89af5d"></span>
### Step 4: Test connectivity

<span id="7d474cfa"></span>
### Method 1: Use ping6 to check the connection status, and get detailed DNS resolution through dig.

Assuming your application service domain to be tested is `alb.example.com`. During actual testing, replace `alb.example.com` with your service domain name.


1. ping6 check:

   ```Bash
   ping6 alb.example.com 
   ```
   

   If you receive a response, it means `alb.example.com` has been properly resolved to an IPv6 address and the network path is accessible.

2. dig check:

   ```Bash
   dig alb.example.com
   ```
   

   You can retrieve and review detailed DNS resolution information for your service domain to determine if the resolution results are as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9baf2dfa7c6683b9502e5f6981600e2.png) </span>


<span id="578b8655"></span>
### Method 2: Confirm connectivity by simulating access and checking relevant fields


1. **Preparations:** 

   Ensure Nginx records the `X-Forwarded-For` header: Update the Nginx configuration files (e.g., `/etc/nginx/nginx.conf` or `/etc/nginx/conf.d/default.conf`) to include `X-Forwarded-For` in the log format.

   1. Open the configuration file `(/etc/nginx/nginx.conf)`.

      ```Bash
      sudo vim /etc/nginx/nginx.conf 
      ```
      

   2. Within the http block, add or modify the log format.

      ```Bash
      http {
       log_format custom '$remote_addr - $remote_user [$time_local] "$request" '
                         '$status $body_bytes_sent "$http_referer" '
                         '"$http_user_agent" "$http_x_forwarded_for"';
                         
       access_log /var/log/nginx/access.log custom;
       ...
      }
      ```
      

   3. Reload or restart Nginx: After updating the configuration file, reload the Nginx configuration to apply the changes.

      ```Bash
      sudo systemctl reload nginx 
      ```
      

2. **Use ECS\-01 to serve as an IPv6 client accessing the service domain with ** **`curl`** **.** 

   1. Type the `curl` command. During actual testing, replace `alb.example.com` with your service domain name.

      ```Bash
      curl -6 -g -I http://alb.example.com 
      ```
      

   2. You can obtain the basic response from the server as shown below, indicating your service is connected to the ALB.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f03a30b31eff4558b152cc93d2754115~tplv-goo7wpa0wc-image.image) </span>

3. Check the Nginx access logs on the server to confirm that the `x-forwarded-for` header contains the IPv6 client's actual IP address.​​ Use the following command:

   ```Bash
   grep 'X-Forwarded-For' /var/log/nginx/access.log 
   ```
   

   You can also use packet capture tools to get the `x-forwarded-for` information. The `x-forwarded-for` information indicates the IPv6 client has been properly connected to the ALB.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f2e50911b764f369893b282674391a0~tplv-goo7wpa0wc-image.image) </span>


<span id="175d2efd"></span>
## FAQs

<span id="25ac731c"></span>
### How does the ALB obtain the real client IP address?

Answer: The ALB inserts the client’s real IP address (IPv4 or IPv6) into the `X-Forwarded-For` field of the HTTP header. The first IP address in this field is the real client IP.

<span id="9e6241c7"></span>
### Encountering a 502 error after implementing a dual\-stack ALB instance.​

Answer: We recommend first checking whether the backend application service is running normally. For example:


* Check whether the security group of the backend ECS properly allows the service CIDR block: `100.64.0.0/10`.

* We recommend enabling backend service health checks on ALB to prevent ALB from forwarding traffic to abnormal backend servers.


<span id="ce2c7ff2"></span>
### How can I increase the default bandwidth for Pay\-by\-data\-transfer IPv6? Is the default maximum bandwidth increasable?

Answer: You can increase it by the following two methods.


1. Based on your business scenario, you can purchase a Bandwidth Package to increase the default maximum bandwidth (200M). Currently, Bandwidth Package supports two metering methods: Pay\-by\-bandwidth and Pay\-by\-95th\-peak, but does not support Pay\-by\-data\-transfer for IPv4.

2. To adjust the default maximum bandwidth for a Pay\-by\-data\-transfer IPv6 instance, you can contact your account manager to request a bandwidth increase based on your instance configuration.
