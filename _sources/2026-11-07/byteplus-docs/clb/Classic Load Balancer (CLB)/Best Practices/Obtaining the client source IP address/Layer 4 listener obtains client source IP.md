---
title: "Layer 4 listener obtains client source IP"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-a-Layer-4-listener-to-obtain-the-client-source-IP-address"
---

This topic explains how a layer 4 listener obtains the client's source IP address accessing the load balancing service through the Proxy Protocol.

<span id="h72Tx9Z4"></span>
## Background


* When the Classic Load Balancer (CLB) forwards access requests to the backend server, in the following scenarios the source address of the access request (i.e., the client address) will not be replaced. You can log in to the backend server and execute cat /var/log/nginx/access.log command to view the access logs and obtain the client's Source IP address.

   
   |Access request |Backend server |Server Group Type |Is the source IP address replaced |Is Proxy Protocol required |
   |---|---|---|---|---|
   |IPv4 |IPv4 |Server type |No |No |
   |IPv6 |IPv6 |Server type |No |No |
   

* During the process of the CLB forwarding access requests to the backend server, in the following scenarios the source address of the access request (i.e., the client address) will be replaced. If the backend server needs to obtain the client's real IP address, it must use the Proxy Protocol.

   
   |Access request |Backend server |Server Group Type |Is the source IP address replaced |Is Proxy Protocol required |
   |---|---|---|---|---|
   |IPv4 |IPv6 |server type |Yes |Yes |
   |IPv6 |IPv4 |Server type |Yes |Yes |
   |IPv4 |IPv4 |IP type |Yes |Yes |
   |IPv6 |IPv4 |IP type |Yes |Yes |
   


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Only Layer\-4 (TCP, UDP) listeners support the Proxy Protocol.</div>


* <div data-tips="true" data-tips-type="default">If the Layer\-4 listener is connected to the Web Application Firewall (WAF), the WAF converts the client's IP address when the client request passes through it, causing the backend server to be unable to directly obtain the client's source IP address.</div>



<span id="FJ7syI2F"></span>
## How it works

The process of CLB using Proxy Protocol with the backend server is as follows:


1. The client forwards access requests to the CLB.

2. CLB establishes a connection with the backend server.

3. **CLB sends a Proxy Protocol packet containing the client's IP address and port number to the backend server.** 

4. **The backend server receives and parses the Proxy Protocol packet to obtain the client's IP address and port number.** 

5. CLB sends the client's access request to the backend server.

6. The backend server handles the client's request.


<span id="FN4bcksF"></span>
## Preparations


* Please ensure you have completed the basic configuration of CLB. For detailed operations, please see CLB Getting Started.

* Before enabling the Proxy Protocol feature, ensure that the service deployed on the backend server supports Proxy Protocol v2.

   > nginx version 1.13.11 and above support Proxy Protocol v2. This article uses Nginx 1.20.1 as an example.   
   

<span id="7JJpA4xq"></span>
## Procedures

<span id="Pls2HORo"></span>
### Step one: Enable Proxy Protocol


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. Click the name of the target CLB instance to enter the instance details page.

3. Select the Listener tab, click Edit Listener on the right of the target listener, and enable the Proxy Protocol switch.

4. Click Next step three consecutive times, and then click OK to complete the actions.


<span id="hsgVHey5"></span>
### Step two: enable Proxy Protocol on backend services


1. Log in to the backend server. For detailed instructions, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Run the following command to open the Nginx configuration file, nginx.conf.

   `vi /etc/nginx/nginx.conf`

3. Press `i` to enter editing mode, and configure Proxy Protocol v2 to obtain the client's source address as follows.

   ```Nginx
   http {
         # $proxy_protocol_addr is used to record the client's real IP
         # $remote_addr is used to record the Local IP of the CLB instance
        log_format  main  '$proxy_protocol_addr - $remote_addr- $remote_user [$time_local] "$request" '
                         '$status $body_bytes_sent "$http_referer" '
                         '"$http_user_agent" "$http_x_forwarded_for"';
         # Taking port 80 as an example, add the proxy_protocol field
         server {
               listen 80   proxy_protocol;
               #...
         }
   }
   ```
   

4. Press Esc key to exit the edit mode, then type :wq to save and exit.

5. Run the following command to apply the configuration.

   `sudo nginx -s reload`


<span id="97xjuQgA"></span>
### Step 3: Verification


1. Open the browser on your local computer.

2. Input `http://your custom domain name `and display the application page deployed by the backend server, indicating that the Proxy Protocol configuration is complete.


<span id="EMTSgRZI"></span>
### Step 4: Obtain client Source IP address


1. Log in to the backend server. For details, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance) or [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Execute cat /var/log/nginx/access.log command, view the access Log, and obtain the client's Source IP address.

   * The format of the proxy protocol v2 packet header carrying the Source IP address of an IPv4 client is as follows:

      ```Plain Text
      /*
       * Proxy Protocol Header:
       * NAT44 Header
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |                                                               |
       * |                           Signature                           |
       * |                                                               |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |  Ver  |  Cmd  |   Af  | Proto |           Length              |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |                       IPv4 Source Address                     |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |                     IPv4 Destination Address                  |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |         Source Port           |        Destination Port       |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       */
      ```
      

   * The format of the proxy protocol v2 packet header carrying the Source IP address of an IPv6 client is as follows:

      ```Plain Text
      /*
       * Proxy Protocol Header:
       * NAT66 Header
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |                                                               |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |                                                               |
       * |                           Signature                           |
       * |                                                               |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |  Ver  |  Cmd  |   Af  | Proto |           Length              |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |                                                               |
       * |                                                               |
       * |                      IPv6 Source Address                      |
       * |                                                               |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |                                                               |
       * |                                                               |
       * |                    IPv6 Destination Address                   |
       * |                                                               |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       * |         Source Port           |        Destination Port       |
       * +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
       */
      ```
