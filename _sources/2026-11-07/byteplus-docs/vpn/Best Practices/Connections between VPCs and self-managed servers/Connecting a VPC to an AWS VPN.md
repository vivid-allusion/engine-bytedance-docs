---
title: "Connecting a VPC to an AWS VPN"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-AWS"
---

This topic describes how to use the BytePlus VPN Connect product to create a private network access channel between BytePlus and the AWS self\-built VPN with static routing.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account with completed [real-name authentication](https://docs.byteplus.com/en/docs/6261/64923) and sufficient balance to purchase Elastic Compute Service (ECS), VPN Connect, and related resources.

* A Virtual Private Cloud named VPC\-01 (CIDR block: 192.168.0.0/16) and its subnet created in BytePlus, with an ECS instance (IP: 192.168.2.88) deployed in one subnet. For procedure, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Purchasing and using ECS instances](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).

* VPC\-02 (CIDR block: 172.31.0.0/16) and a public subnet created in AWS, with an EC2 instance deployed in the public subnet (if using CentOS, subscribe in Marketplace beforehand). The EC2 instance's private IP is 172.31.16.111. See AWS product documentation on the AWS official website for detailed steps.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">EC2 instances are virtual servers in AWS cloud. For more details, see <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html">What is Amazon EC2</a>.   </div>
   

<span id=".5pON5L2c6K-05piO"></span>
## Instructions

Deploy the Strongswan service on the EC2 instance in AWS, allocate an public IP (54.XX.XX.208) as the public network egress of VPC\-02; create a VPN connection on the BytePlus side and register AWS information to the Customer gateway. Once all configurations are complete, initiate the VPN connection. Ping the ECS instance (IP: 192.168.2.88) in VPC\-01 from the EC2 instance in AWS. A successful ping indicates network connectivity is established.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7507e6edb98c00ac563bd93cc2b54d13.png) </span>

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5ZyoQVdT5L6n5Li6RUMy5YiG6YWN5YWs572RSVDlubbmt7vliqDlronlhajnu4Top4TliJk="></span>
### **Step 1: Allocate a public IP for AWS EC2 and add security group rules**


1. Log in to the AWS platform and allocate a public IP to the EC2 in the public subnet of VPC\-02, serving as VPC\-02's public network egress. The EIP allocated to the EC2 in this article is `54.XX.XX.208`.

2. Go to the network interface details bound to the EC2 and disable source/destination check for the EC2.

3. Go to the security group details associated with the EC2 and add inbound rules to allow access to the following ports.

   * TCP: 22

   * UDP: 500

   * UDP: 4500

4. Add a route to allow VPC\-01 (CIDR block: 192.168.0.0/16) to access the EC2 (private IP address: 172.31.16.111).


<span id=".5q2l6aqk5LqM77ya5Zyo54Gr5bGx5byV5pOO5L6n5Yib5bu6VlBO6L-e5o6l"></span>
### **Step 2: Create VPN Connect**


1. Log in to the VPN Connect console.

2. Create a VPN gateway. For procedure, see [Creating a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-VPN-gateway-2).

   After the VPN gateway is created, the assigned egress IP is `180.XX.XX.98`.

3. Create a customer gateway. Related configuration is shown below. For procedure, see [Creating a customer gateway](https://docs.byteplus.com/en/docs/vpn/Creating-a-customer-gateway1).

   The IP address is the EIP assigned to the EC2 on the AWS side, with `54.XX.XX.208` used in this example.

4. Create an IPsec\-VPN connection. Related configuration is shown below. For procedure, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1).

   * **Connection information**

   * **Advanced configuration**

5. Configure VPN gateway route to allow access to the AWS\-side VPC CIDR block (`172.31.0.0/16`). Related configuration is shown below. For procedure, see [Adding a VPN gateway route](https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route).


<span id=".5q2l6aqk5LiJ77ya5ZyoQVdT5L6n5a6J6KOFU3Ryb25nc3dhbuW5tuWPkei1t-i_nuaOpQ=="></span>
### **Step 3: Install Strongswan on the AWS side and initiate the connection**


1. Log in to the created EC2 on AWS platform and install Strongswan.

   * If using Amazon Linux2, execute the following command as root.

      ```Plain Text
      amazon-linux-extras install epel -y
      yum install strongswan
      ```
      

   * If using CentOS, subscribe first, then execute the following command as root.

      ```Plain Text
      yum install strongswan        
      ```
      

2. Run the following command to check the Strongswan version.

   ```Plain Text
   strongswan version        
   ```
   

3. Run the command `vim /etc/strongswan/ipsec.conf` to edit the ipsec.conf file and save after editing. IKE and IPsec configurations must match those used when creating the IPsec connection on BytePlus. The example configuration is as follows:

   ```Plain Text
   config setup
       # strictcrlpolicy=yes
       # uniqueids = no
   conn sample-self-signed
       # strictcrlpolicy=yes
       # uniqueids = no# Add connections here.conn %default
       authby=psk
       type=tunnel# Sample VPN connectionsconn huoshanyun
       keyexchange=ikev2 #The IKE version must match the BytePlus IPsec-VPN connection configuration, which is ikev2 here.
       left=172.31.16.111 #Private IP address of AWS EC2
       leftsubnet=172.31.0.0/16 # CIDR block of AWS VPC
       leftid=54.XX.XX.208 #Public IP address of AWS EC2
       right=180.XX.XX.98 #Egress IP of BytePlus VPN gateway
       rightsubnet=192.168.0.0/16#Subnet segment of BytePlus VPC
       rightid=180.XX.XX.98 # Egress IP of BytePlus VPN gateway
       auto=start
       ike=aes-sha1-modp1024
       ikelifetime=86400s
       esp=aes-sha1-modp1024
       lifetime=86400s
       aggressive=yes        
   ```
   

4. Edit `/etc/strongswan/ipsec.secrets` to configure the IPsec Pre\-Shared Key in the format: `{EC2-EIP} {BytePlus VPN gateway egress IP} : PSK "Pre-Shared Key from BytePlus IPsec-VPN connection advanced configuration"`. The example is: `54.XX.XX.208 180.XX.XX.98 : PSK "******"`

5. Run the following command to set the TCP MSS value.

   ```XML
   iptables -t mangle -A FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --set-mss 1350
   ```
   

6. Run the following command to enable system forwarding.

   ```Plain Text
   echo 1 > /proc/sys/net/ipv4/ip_forward        
   ```
   

7. Run the following command to start Strongswan.

   ```Plain Text
   systemctl enable strongswan
   systemctl start strongswan
   ```
   

   Check the service status to see that Security Associations are already connected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_77e8691166e057c85cf91f82afaad308.png) </span>


<span id=".6L-e6YCa5oCn5rWL6K-V"></span>
## Connectivity test

Log in to the created EC2 on the AWS platform and ping the IP address `192.168.2.88` of the cloud server in BytePlus\-side VPC\-01 (`CIDR block 192.168.0.0/16`). A successful ping indicates the private network access channel between BytePlus and AWS has been established.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_415cf133fceb62c1be080b7f95147b29.png) </span>
