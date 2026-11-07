---
title: "Obtaining the client Source IP address"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Obtaining-the-client-Source-IP-address"
---

<span id="RAc9IyJz"></span>
## Background


* When Network Load Balancer (NLB) forwards access requests to the backend server, in the following scenarios, the source address of the access request (that is, the client address) is not replaced. You can log in to the backend server and run the `cat /var/log/nginx/access.log` command to view the access log and obtain the client's source IP address.

   
   |Access request |Backend server |Server Group Type |Enable client IP address preservation |Is the source IP address replaced |Is Proxy Protocol required |
   |---|---|---|---|---|---|
   |IPv4 |IPv4 |Server type |Yes |No |No |
   |IPv6 |IPv6 |Server type |Yes |No |No |
   

* In the process of NLB forwarding access requests to the backend server, in the following scenarios, the source address of the access request (that is, the client address) will be replaced. If the backend server needs to obtain the client's real IP address, it must use the Proxy Protocol.

   
   |Access request |Backend server |Server Group Type |Enable client IP address preservation |Is the source IP address replaced |Is Proxy Protocol required |
   |---|---|---|---|---|---|
   |IPv4 |IPv4 |Server type |No |Yes |Yes |
   |IPv6 |IPv6 |Server type |No |Yes |Yes |
   |IPv4 |IPv6 |Server type |Yes |Yes |Yes |
   |IPv6 |IPv4 |server type |Yes |Yes |Yes |
   |IPv4 |IPv6 |Server type |No |Yes |Yes |
   |IPv6 |IPv4 |Server type |No |Yes |Yes |
   |IPv4 |IPv4 |IP type |Not supported for this feature |Yes |Yes |
   |IPv6 |IPv4 |IP type |Not supported for this feature |Yes |Yes |
   


<span id="tDbArNM9"></span>
## How it works

The process of using Proxy Protocol between NLB and the backend server is as follows:


1. The client sends an access request to the NLB.

2. The NLB establishes a connection with the backend server.

3. **The NLB sends a Proxy Protocol packet to the backend server, carrying the client's IP address and port number.** 

4. **The backend server receives and parses the Proxy Protocol message to obtain the client's IP address and port number.** 

5. NLB sends client access requests to the backend server.

6. The backend server handles the client's request.


<span id=".5bqU55So5Zy65pmv"></span>
## Preparations


* Ensure that you have completed the basic configuration of NLB. For detailed operations, see CLB Quick Start.

* Before enabling the Proxy Protocol feature, ensure that the service deployed on the backend server supports Proxy Protocol v2.

   > Nginx version 1.13.11 and above support Proxy Protocol v2. This topic uses Nginx 1.20.1 as an example.   
   

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".5q2l6aqk5LiA77ya5ZCv55SoUHJveHkgUHJvdG9jb2zljY_orq4="></span>
### Step 1: Enable Proxy Protocol


1. Log in to the Server Group console.

2. In the top menu bar, select the target project and region.

3. Click Edit basic information on the right side of the target server group.

4. Select Enable Proxy\-Protocol protocol, click Know and Enable to complete the action.


<span id=".5q2l6aqk5LqM77ya5ZCv55So5ZCO56uv5pyN5Yqh55qEUHJveHkgUHJvdG9jb2w="></span>
### Step 2: Enable Proxy Protocol for backend services


1. Log in to the backend server. For details, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Run the following command to open the Nginx configuration file, nginx.conf.

   `vi /etc/nginx/nginx.conf`

3. Press `i` to enter edit mode and modify the Proxy Protocol configuration as follows.

   ```Nginx
   http {
         # $proxy_protocol_addr is used to record the client's real IP
         # $remote_addr is used to record the NLB instance's local IP
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


<span id="OFlR6GtF"></span>
### Step 3: Verify traffic


1. Open the browser on your local computer.

2. Input https://your custom domain name and display the application page deployed by the backend server, indicating that the Proxy Protocol configuration is complete.


<span id=".5q2l6aqk5LiJ77ya6I635Y-W5a6i5oi356uv5rqQSVDlnLDlnYA="></span>
### Step 4: Obtain client Source IP address


1. Log in to the backend server. For details, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

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
