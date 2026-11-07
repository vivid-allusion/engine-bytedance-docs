---
title: "Create a development machine"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/create_a_development_machine"
---

<span id="c9d7cd95"></span>
# Prerequisites


* The Volcano Engine LAS service has been enabled, and account identity verification is complete. For detailed steps, refer to **Preparation**.

* At least one queue resource is available to support development machine deployment requirements. For instructions on creating resource queues, refer to [Queue management](https://docs.byteplus.com/docs/Byteplus_LAS/queue_manage).

* (Optional) To connect the development machine in a dedicated network environment, you also need to prepare relevant network resources and configurations:

   * At least one load balancer instance has been created. For detailed steps, refer to [Create instance](https://docs.byteplus.com/zh-CN/docs/clb/CLB-instances-01).

   * A private network has been created, and the core configuration requirements for the VPC are as follows. For detailed steps, refer to [Create private network](https://docs.byteplus.com/zh-CN/docs/vpc/Creating-a-VPC) **.** 

      * The VPC subnet availability zone is the same as the queue availability zone.

      * The VPC security group configuration is complete, and its inbound rules must include at least one rule allowing all traffic from the 100.64.0.0/10 subnet.


<span id="ba8300e3"></span>
# Create a development machine


1. Go to the development machine page.

   1. Log in to [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home?), and select the target region and project.

   2. In the left navigation bar, select Data Processing \> Development Machine to access the development machine page.

2. Click Create dev machine\*\*,\*\* then configure the following key parameters on the development machine configuration page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f209913c66db406ba2e17ea1d18d7695~tplv-goo7wpa0wc-image.image) </span>

   1. Configure basic information.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c2f1e7bc28742f4996c52b579e4b6fa~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter name |Description |
      |---|---|
      |Name |Enter the name of the development machine. **Required**.<br><br><br>* Supports 1–100 visible characters and only includes uppercase and lowercase letters, Chinese characters, numbers, hyphens, and underscores. |
      |Description |Enter an appropriate description for the development machine. **Optional**.<br><br><br>* Supports 1–200 visible characters. |
      

   2. Resource configuration.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44f2bc38d6a8406aaadaa30a18531b5b~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter name |Description |
      |---|---|
      |Queue |Select a prepared queue resource for subsequent environment deployment and task development of the development machine.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, LAS AI supports two types of queue resources: exclusive queues and regular compute queues. We recommend using exclusive queues (that is, EMR Serverless queues), as they can improve queue resource utilization and flexibility. For more information about queues, see <a href="https://docs.byteplus.com/docs/Byteplus_LAS/queue_manage">Queue management</a>.</div><br> |
      |Availability zone |Select the availability zone of the queue used by the current development machine. |
      |Resource allocation |Allocate queue CU resources to the current development machine. |
      |Resource Delivery Strategy |Set the delivery policy for queue resources. That is, if the queue resources are occupied by other jobs and there are not enough idle resources available, please select an appropriate delivery policy. Currently supported:<br><br><br>* wait: Release resources after other jobs finish.<br><br>* preempt: End the task immediately to release resources, which may cause other tasks to fail. |
      

   3. Configure environment information.

      
      |Parameter name |Description |
      |---|---|
      |Image type & image |Select the image for the development machine.<br><br>Currently supports built\-in images, custom images, and images from the Volcano Engine image repository. Custom images and images from the Volcano Engine image repository require the ssh\-server software to be installed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For Debian, Ubuntu, CentOS, and SUSE operating systems, ssh\-server will be automatically installed when you create a development machine. For other operating systems, you need to install it yourself when building the image.</div><br><br><br><br>* Built\-in image: LAS provides official built\-in images such as Daft, Ray, and Spark.<br><br>* Custom image: Supports deploying and starting the development machine with custom images built on the LAS platform.<br><br>* Volcengine image: Images from the Volcano Engine image repository.<br><br>* mirror URL: Supports configuring a self\-built image repository URL that is accessible from the public network. Caution: This image method is not supported when using a dedicated queue. |
      |Cloud disk |Select the cloud disk type and specify the cloud disk capacity required by the development machine, with a minimum of 20 GiB. **Optional**.<br><br><br>* Used to store files during development. Supports two types of cloud disks: Ultra SSD PL0 and Ultra SSD FlexPL.<br><br>* Cloud disk billing for a single development machine instance starts from the first run and ends upon deletion.<br><br>* The cloud disk is mounted as persistent storage at the root directory /. Data in this directory will be retained after shutdown or restart.<br><br>* When cloud disk capacity is insufficient, dynamic expansion on demand is supported.<br><br>* When deleting a development machine, all data on the cloud disk will be erased and cannot be recovered. Caution: Make sure to back up important data.<br><br>* To achieve permanent storage, configure a storage mount path. |
      |dataset mount |Select the LAS dataset to mount.<br><br><br>* If you have already created the data required for subsequent data processing tasks as LAS datasets, you can mount the dataset to the development machine here, making it easier to directly read the data when using the development machine later.<br><br>* Currently, up to 20 datasets can be mounted. For details on creating datasets, see [Dataset management](https://docs.byteplus.com/docs/Byteplus_LAS/Dataset_management). |
      |Mount storage path |Select the file system to mount and configure the mount path. Optional.<br><br><br>* You can use the storage mount feature to mount different types of storage, enabling access to required data or persistent storage of files generated during development.<br><br>* Currently, vePFS, TOS, and NAS storage mounting are supported. Future versions will support mounting storage media such as TOS (cloudFS) and HDFS.<br><br>* Currently, up to 20 file systems can be mounted. |
      |Environment variables |You can create environment variables for the development machine as needed, in Key\-Value format, making it convenient to reference them directly in task code later.<br><br>You can choose to configure environment variables using Key\-Value mode or text mode as needed. In text mode, enter the environment variable name and value directly in the text box in the `key:value` format. You can enter multiple environment variables, separated by line breaks. |
      

   4. Configure network information and access settings.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/973451a8c26044a6a8e8e3511dddd7d5~tplv-goo7wpa0wc-image.image) </span>

      
      |Category |Parameter name |Description |
      |---|---|---|
      |Network information |Ssh network mode |* Shared networks: The platform will provide a public IP for SSH login by default, but connection speed will be limited.<br><br>* Exclusive network: Users can configure load balancing to access the development machine, ensuring SSH connection experience.<br><br>* Shut down the public network: You can also choose to disable public access to the development machine. |
      ||Advanced network configuration |* After enabling, the network from the development machine to the target VPC can be connected.<br><br>* In the inbound direction of the security group, you must allow the rule for the network segment of your SSH client connection. The protocol type is TCP, the port range is 2222, and the source address must be the local machine or local network egress IP. Otherwise, you will not be able to log in to the development machine. If a custom port is configured, you must also configure the custom listening port value in the port range. |
      ||Public network access mode<br><br>(Exclusive networkneeds to be configured) |When Ssh network mode is set to Exclusive network, you need to configure the access mode for using the public network to access the development machine. Currently, two modes are supported: Public NAT gateway and load balance (only available to allowlist users, activation required).<br><br><br>* When Public NAT gateway is selected: you use the public IP of your own NAT gateway to access the development machine. You also need to set the corresponding Public NAT gateway and Public IP.<br><br>* When load balance is selected: you use load balancing to access the development machine.<br><br>   * The load balance mode is currently disabled by default and is only available to allowlist users. To use this mode, you need to [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) and contact Byteplustechnical support personnel for activation.<br><br>   * When load balancing is configured with a public network, the development machine will provide a public network SSH login command by default; otherwise, it will provide a private network SSH login command.<br><br>   * The development machine will, by default, connect to the VPC network associated with the configured load balancer. Therefore, you must also configure the subnet under this VPC, and the subnet's availability zone must match the one selected when creating the queue. |
      ||Advanced network configuration |* After enabling, the network from the development machine to the target VPC can be connected.<br><br>* In the inbound direction of the security group, you must allow the rule for the network segment of your SSH client connection. The protocol type is TCP, the port range is 2222, and the source address must be the local machine or local network egress IP. Otherwise, you will not be able to log in to the development machine. If a custom port is configured, you must also configure the custom listening port value in the port range. |
      |Access configuration |Ssh public key |SSH login to the development machine only supports public key authentication.<br><br><br>* The development machine supports SSH login. You need to enter an SSH public key. If you do not have one, you can generate it using the `ssh-keygen -t rsa` command.<br><br>* For multiple public keys, please enter them separated by line breaks. |
      ||Access port<br><br>(Exclusive networkneeds to be configured) |Currently, only SSH login is supported.<br><br><br>* The access port range is 1\-65535.<br><br>* Different instances require different ports to be specified.<br><br>* In exclusive mode, you can add custom ports. The listening port is the port inside the container, and the port exposed on the load balancer is used for invocation.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After adding a custom port, you need to add rules to the security group, including:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Protocol type: TCP.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Port range: the listening port you entered; source address is the local machine or local network egress IP.</div><br> |
      

3. After completing the above parameter configurations, review and check the service agreement in the lower right corner. Once done, click the "Create" button to start creating the development machine. At this point, the development status on the development machine list page will be "Starting".

   When the development machine status changes to "Running" it indicates that the development machine has been successfully created.


<span id="33e1558d"></span>
# Next steps


* After the development machine is created, you can remotely log in to the development machine and start task development. For remote login instructions, see [Connect to a development machine](https://docs.byteplus.com/docs/Byteplus_LAS/Remote_connection_to_the_development_machine).

* You can also view the operation logs of the development machine, monitor queue resource usage, and manage the development machine by starting, stopping, or copying it. For details, see [Manage development machines](https://docs.byteplus.com/docs/Byteplus_LAS/Manage_development_machines).
