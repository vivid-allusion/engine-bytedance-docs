---
title: "Connecting a VPC to an Alibaba Cloud ECS"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-an-Alibaba-Cloud-server"
---

This topic introduces how to use the VPN Connect product to establish a network link between BytePlus Virtual Private Cloud (VPC) and Alibaba Cloud VPC, enabling mutual access between Alibaba Cloud and BytePlus cloud resources.

<span id=".5pON5L2c5YmN5o-Q"></span>
## Prerequisites


* A VPC (192.168.0.0/16) has been created. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Alibaba Cloud self\-built cloud server (ECS 172.16.0.0/21) is available. For procedure, see Alibaba Cloud official product documentation.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u54Gr5bGx5byV5pOOVlBO6L-e5o6l"></span>
### **Step 1: Configure BytePlus VPN Connect**


1. Create a VPN gateway in the VPN Connect console. For procedure, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2).

2. Create a customer gateway in the VPN Connect console. For procedure, see [Creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1).

3. Create an IPsec\-VPN connection in the VPN Connect console. For procedure, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1).


<span id=".5q2l6aqk5LqM77ya6YWN572u6Ieq5bu65LqR5pyN5Yqh5ZmoVlBO"></span>
### **Step 2: Configure the self\-managed cloud server VPN**


1. Log in to the self\-managed cloud server instance and run the following command to install StrongSwan software.

   ```Plain Text
   [root@vpn ~]# yum -y install strongswan         
   ```
   

2. Run the following command to verify whether the software was installed successfully.

   ```Plain Text
   [root@vpn ~]# strongswan version 
   Linux strongSwan U5.7.2/K3.10.0-1127.el7.x86_64
   University of Applied Sciences Rapperswil, Switzerland
   See 'strongswan --copyright' for copyright information.
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This operation is based on StrongSwan version 5.7.2.   </div>
   

3. Configure the `ipsec.conf` file. Ensure the settings match the BytePlus IPsec connection.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the cloud and on\-premises StrongSwan servers use ikev1 mode and multiple cloud CIDR blocks need to be connected, you must configure policies for each cloud CIDR block in the <code>ipsec.conf</code> file to establish connections successfully.   </div>
   

   ```Plain Text
   [root@vpn strongswan]# cat /etc/strongswan/ipsec.conf
   # ipsec.conf - strongSwan IPsec configuration file
   # basic configuration
   
   config setup
       # strictcrlpolicy=yes
        uniqueids = never
   conn %default
       authby=psk     #Use pre-shared key authentication method
       type=tunnel
       
   conn volcvpn
       keyexchange=ikev2              # IKE version for IPsec-VPN connection. ikev2 is recommended for better security.
       left=172.16.0.135              # Local IP address
       leftsubnet=172.16.0.0/21       # Local Subnet
       leftid=111.XX.XX.125          # Public IP or EIP of the local gateway device
       right=180.XX.XX.131            # BytePlus VPN IP address
       rightsubnet=192.168.0.0/16      # BytePlus VPC network segment
       rightid=180.XX.XX.131        # BytePlus VPN address
       auto=route
       ike=aes-sha1-modp1024          # Encryption algorithm-authentication algorithm-DH algorithm of IKE protocol in IPsec-VPN connection
       ikelifetime=86400s             # SA lifetime of IKE protocol, in seconds
       esp=aes-sha1-modp1024          # Encryption algorithm-authentication algorithm-DH algorithm of IPsec protocol in IPsec-VPN connection
       lifetime=86400s                # SA lifetime for IPsec protocol
       type=tunnel
   ```
   

4. Configure the ipsec.secrets pre\-shared key.

   * strongSwan version 5.7.2

      ```Plain Text
      [root@vpn strongswan]# cat ipsec.secrets 
      111.XX.XX.125 180.XX.XX.131 : PSK 12345678
      ```
      

   * strongSwan 5.8.0 and later versions

      ```Plain Text
      [root@vpn strongswan]# cat ipsec.secrets 
      111.XX.XX.125 180.XX.XX.131 : PSK "12345678"
      ```
      

5. Enable system forwarding configuration.

   ```Plain Text
   echo 1 > /proc/sys/net/ipv4/ip_forward
   ```
   

6. Enable StrongSwan.

   ```Plain Text
   [root@vpn strongswan]# systemctl enable strongswan
   [root@vpn strongswan]# systemctl start strongswan
   ```
   


<span id=".5q2l6aqk5LiJ77ya6YWN572uVlBO572R5YWz6Lev55Sx"></span>
### **Step 3: Configure VPN gateway routes**


1. In the Virtual Private Cloud console, configure routing information in the route table of the VPC (192.168.0.0/16) as shown below.

2. In the VPN Connect console, configure VPN gateway routes as shown below.

3. Configure routing for the self\-built cloud service based on your actual situation; this will not be covered in detail here.


<span id=".5rWL6K-V6L-e6YCa5oCn"></span>
## Test connectivity

Log in to the ECS and execute the `ping` command to ping any private IP address of the BytePlus VPC, verifying private address communication between the ECS (172.16.0.0/21) and the BytePlus VPC (192.168.0.0/16).

If ping is successful as shown below, it indicates that the network connection between the ECS and the BytePlus VPC is established.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ce89e8b48f8f675e5ea24abcc5f46ab5.png) </span>
