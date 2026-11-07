---
title: "RabbitMQ supports public network allowlist via CLB"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/RabbitMQ_supports_public_network_allowlist_via_CLB"
---

The Message Queue for RabbitMQ product does not currently provide an allowlist function. You can use the CLB load balancing product to control the client IPs that access RabbitMQ instances. This topic describes the specific configuration steps for implementing the RabbitMQ allowlist using CLB.

<span id="a7e8226a"></span>
## Background information 

After a RabbitMQ instance is created, all devices within the same private network VPC environment are allowed to access the instance by default. If public network access is enabled for the instance, all public network devices are allowed to access the instance by default. Since the RabbitMQ product does not currently provide an allowlist function, if you need to restrict the client IP addresses that can access an instance, you can use the CLB load balancing product to control which client IP addresses can access the RabbitMQ instance.

Before you start using the CLB load balancing product, it is recommended that you first familiarize yourself with the following concepts related to the CLB load balancing product:


* Access control policy group: An access control policy group is a collection of IP entries used for centralized management of IP addresses. The policy group itself does not impose restrictions on the access control method; this is handled by the associated listener.

* Backend server group: A backend server group is a group of instances that receive and process requests. The CLB instance distributes client requests to servers in the backend server group based on the listener configuration.

* Listener: A listener forwards requests by matching the protocol and port. It then distributes request traffic to backend server groups according to the scheduling algorithm.


<span id="27a81b9f"></span>
## Preparations


* The RabbitMQ instance has been created in advance.

* If you need to enable public network access for a RabbitMQ instance, please refer to [Enable public network access](https://docs.byteplus.com/en/docs/rabbitmq/Set_public_network_access#.5byA5ZCv5YWs572R6K6_6Zeu).


<span id="d86daf5d"></span>
## Step 1: Obtain the IP address of the RabbitMQ instance's network interface

To control which client IP addresses can access the RabbitMQ instance through the CLB product, you need to configure the IP address of the network interface card (NIC) for the RabbitMQ instance in the backend server group of the CLB instance. When a CLB instance receives a client request, it distributes the request to backend servers according to the listener configuration.


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq), and select the target project and region at the top of the page.

2. In the **Instances** list, click the target instance to enter the instance details page.

3. On the **Instance information** tab, in the **Basic information** section, copy the RabbitMQ instance ID, and then click the instance's private network.

4. Select **Network Interface** from the left navigation pane of the private network console, enter the RabbitMQ instance ID to filter the results, and obtain the network interface IP address.


<span id="1dcf6118"></span>
## Step 2: Create a CLB instance


1. Log in to the [CLB Load Balancer Console](https://console.byteplus.com/clb), and select the target project and region at the top of the page.

2. In the left navigation bar, select **Instance management**, and then click **Create load balancer**.

3. On the **Create Load Balancer** page, configure the relevant parameters for the CLB instance.

   
   |**Parameters** |**DescriptionDescription** |
   |---|---|
   |**Basic information** ||
   |Billing type |CLB instances support two billing methods: Pay\-as\-you\-go and Subscription.<br><br><br>* Pay\-as\-you\-go: This is a postpaid model in which charges are calculated by the hour based on usage duration, and instances can be created or deleted at any time.<br><br>* Subscription: This is a prepaid model that charges based on the subscription duration. |
   |Region |Select the region for the CLB instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">CLB instances must be in the same region as RabbitMQ instances.</div><br> |
   |Availability zone |Select the availability zone for the CLB instance.<br><br>Support for primary and standby availability zones<br><br><br>* Under normal circumstances, the primary availability zone is enabled by default, and the secondary availability zone does not carry traffic.<br><br>* When the primary availability zone fails, the system automatically switches to the backup availability zone to continue providing load balancing services. |
   |Name |Set the name of a CLB instance |
   |Description |Set the description for the CLB instance. |
   |**Network configuration** ||
   |IP version |Supported IP versions for CLB instances. |
   |Network type |Select the network type for the CLB instance.<br><br><br>* Public network: When you create a public network load balancer, a CLB instance and a public IP are created simultaneously, and the public IP is bound to the CLB instance.<br><br>* Private network: To create a private network load balancer, do not assign a public IP when creating the CLB instance. If public network access is required, you can configure the 'Public network access' parameter during CLB instance creation, or bind a public IP to the CLB instance after it has been created. |
   |Private network |Choose the private network to which the CLB instance belongs. |
   |Subnet |Select the Subnet to which the CLB instance belongs. |
   |IPv4 address |Choose the allocation method for the CLB instance IPv4 address.<br><br><br>* When 'Manual IP Assignment' is selected, please manually enter an IPv4 address within the subnet range.<br><br>* When "Manual IP Assignment" is selected, batch creation of CLB instances is not supported. |
   |Public network access |You can select "Bind existing EIP" and choose an existing EIP to provide public network access for this CLB instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is valid only when "Private Network" is set to "Private".</div><br> |
   |**Performance limit** ||
   |Specification |Select the appropriate CLB instance specification based on business requirements. |
   

4. Read and select the relevant agreements, then click **Buy now**.


<span id="09d62296"></span>
## Step 3: Configure an access control policy group

An access control policy group is a collection of multiple IP entries used for centralized management of IP addresses. You can enter the client IP addresses or CIDR address ranges that are allowed to access the RabbitMQ instance into the policy group.


1. Log in to the [CLB Load Balancer console](https://console.byteplus.com/clb), and then select the target project and region at the top of the page.

2. In the left navigation bar, select **Access Control**, and then click **Create Access Control Policy Group**.

3. In the pop\-up dialog box, set the policy group name and project, specify the client IP address or CIDR address range allowed to access the RabbitMQ instance, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In testing scenarios, if you are using a home router or an office network, your device may be located within a private network. Devices in the private network communicate with the public network through NAT technology.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">At this point, the local IP address you obtain by running the <code>ipconfig</code> or <code>ifconfig</code> command in the command line is a private network address and cannot be directly configured in the access control policy group. You can use <a href="https://whatismyipaddress.com/">whatismyipaddress.com</a> to check the public IP broker address of your egress connection, then enter the IP address or CIDR address range into the policy group.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Dynamic Host Configuration Protocol (DHCP) will distribute this address to other tenants. Please remove the IP address or CIDR address range promptly after testing is complete.   </div>
   

<span id="f9011dc4"></span>
## Step 4: Configure a backend server group

The backend server group is a group of instances that receive and process requests. The CLB instance distributes client requests to the backend servers according to the listener configuration. You can enter the obtained RabbitMQ instance access port and network interface card IP address into the backend server group.


1. Log in to the [Cloud Load Balancer (CLB) console](https://console.byteplus.com/clb), and then select the target project and region at the top of the page.

2. In the left navigation bar, select **Instance Management**, click the CLB Instance name, and go to the instance details page.

3. On the **Backend Server Group** tab, click **Create Backend Server Group**, then set the server group name, select **IP type**, and click **OK**.

4. In the server group, click **Add Server**.

5. On the **Add IP address** page, enter the RabbitMQ instance network interface IP address, access port, and user\-defined weight, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The IP address of the network interface card for the RabbitMQ instance has been obtained in advance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The port for the public network address of the AMQP access point of the RabbitMQ instance is <code>5671</code>, and the port for the private network address is <code>5672</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The greater the weight, the more requests are forwarded. 0 means requests are not accepted, and 100 means the maximum number of requests that can be forwarded.   </div>
   


<span id="5c75c09c"></span>
## Step 5: Configure a listener

The listener provides the capability to forward requests by matching the protocol and port of requests, and distributes request traffic to backend server groups according to the scheduling algorithm. In the listener, you need to associate the access control policy group and the backend server group.


1. Log in to the [Cloud Load Balancer (CLB) console](https://console.byteplus.com/clb), then select the target project and region at the top of the page.

2. In the left navigation bar, select **Instance management**. Click the CLB instance name to enter the instance details page.

3. On the **Listener** tab, click **Add Listener**.

4. Configure the protocol, associate with an access control policy group, and then click **Next**.

   
   |**Parameters** |**DescriptionDescription** |
   |---|---|
   |Listener name |Set a custom name for the listener. If left blank, the default value is "protocol\-port", for example, "TCP\-5671". |
   |Load balancing protocol |Select the protocol type for the CLB instance listener. This topic uses **TCP**. |
   |Listening port |Enter the port to listen on. You need to listen to port `5671` on the public address of the AMQP endpoint for the RabbitMQ instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The listener port to be added must not be the same as any other listener port in the same CLB instance.</div><br> |
   |Scheduling algorithm |Specify the rule that the listener follows when forwarding requests. This topic uses **weighted round robin (WRR)** , where backend servers with higher weights are polled more frequently (with higher probability). |
   |Access control |Does the listener apply allowlist and blocklist controls to access requests? This topic chooses to enable access control and selects the **allowlist** control method. |
   |Strategy group name |Select a previously created access control policy group from the dropdown list. |
   

5. Associate an existing backend server group, and then continue to click **Next** until the listener addition is complete.

6. Return to the listener page and check the status.


<span id="4e32c769"></span>
## Result verification

After completing the above configuration, you can access the RabbitMQ instance using the CLB instance IP address and listener port. You can obtain the CLB instance IP address in the **Basic Information** of the CLB instance.

Effect: Client IPs in the access control policy group can continue to access the RabbitMQ instance, while other client IPs cannot.
