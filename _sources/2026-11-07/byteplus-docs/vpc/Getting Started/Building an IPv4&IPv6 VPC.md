---
title: "Building an IPv4&IPv6 VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Building-an-IPv6-VPC"
---

## Scenarios

This topic describes how to configure a dual\-stack VPC.

> **tip**

> VPC's IPv6 is currently in invite\-only Beta. If you need a trial, please contact your account manager.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b44f42e92f874b571b5bf5695e402fa8.png)

## Configuration procedures

> **tip**

> The following section only covers essential parameters and their recommended values. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.

### Step 1: Create VPC and subnet

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select your target region.

3. Click **Create VPC**.

4. Configure parameters based on the table below.

   |Parameters |Notes |Sample value |
   |---|---|---|
   |**VPC information** |||
   |Region |Select the Region where the Virtual Private Cloud resides. Select a region closer to your business operations to reduce network latency. |China (Beijing) |
   |Name |Type in the name for the VPC. |vpc\-01 |
   |IPv4 CIDR |Set the VPC's IPv4 CIDR block.<br><br>> **warning**<br><br><br>> After creation, the CIDR block of the VPC cannot be modified.<br> |192.168.0.0/16 |
   |IPv6 CIDR |Enable the VPC's IPv6 CIDR block. When enabled, the system automatically assigns an IPv6 CIDR block to the VPC. By default, IPv6 addresses support only private communication and an IPv6 gateway is automatically created. |Enable |
   |**Subnet** |||
   |Zone |Select the Availability Zone where the Subnet resides. |AZ\-A |
   |Name |Enter the subnet name. |Subnet\-A |
   |IPv4 CIDR |The subnet CIDR must fall within the VPC's IPv4 address range and must not overlap with existing subnets.<br><br>> **warning**<br><br><br>> After creation, the CIDR block of the subnet cannot be modified.<br> |192.168.1.0/24 |
   |IPv6 CIDR |Enable the IPv6 CIDR block of the Subnet. Once enabled, the subnet IPv6 CIDR defaults to a /64 mask. You can customize the last 8 bits of the subnet IPv6 CIDR by entering a decimal value between 0 and 255. |Enable, 1 |

5. Click **Create** to complete the VPC configuration.

### Step 2: Create an ECS instance and associate an EIP

1. In the left\-side navigation pane, click **Quick Links \> ECS**.

2. Click **Create Instance** to begin configuring your ECS instance.

3. Follow the interface prompts to complete ECS configuration step\-by\-step, including base configuration, network & security, and advanced settings. Specific configurations are detailed in the table below.

   > **tip**

   > This section only covers essential parameters and their recommended values. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case. For more parameter details, see [Purchasing an Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   |Parameters |Notes |Sample value |
   |---|---|---|
   |**Basic configuration** || |
   |Region and AZ |Select the region and availability zone for the ECS instance. Its region must match the region of the VPC. |China (Beijing), Availability Zone A |
   |Image |Images provide ECSs with pre\-configured operating systems and essential application data. Please select according to your actual needs. |Public image, CentOS 7.9 |
   |**Network Configuration** |||
   |VPC |Select the VPC created in Step 1. |vpc\-01 |
   |Subnet |Select a subnet under the created vpc\-01. |subnet\-01, Auto\-assign IP |
   |IPv6 |Select **Free IPv6 Address Allocation**. |Check |
   |EIP |Enable this option to automatically assign an EIP during ECS creation, providing Internet access capabilities.<br><br><br>* ISP: Supports BGP (Multi\-ISP).<br><br>* Metering method: The EIP Metering method is the same as that of the ECS instance. In this example, it is **Pay\-as\-you\-go**. Pay\-as\-you\-go EIP addresses support billing by bandwidth cap and pay\-by\-data\-transfer.<br><br>* Bandwidth cap: The maximum bandwidth for EIP, measured in Mbps. |* ISP: BGP (Multi\-ISP)<br><br>* Billing method: Pay\-by\-data\-transfer<br><br>* Bandwidth cap: 5Mbps |
   |Security group |This topic selects the default security group in vpc\-01 to control inbound and outbound traffic for the primary network interface of ECSs. If you use another security group, you need to create it in advance. For the procedure, see [Creating a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group). |Default |

4. Click **Next: Confirm**.

5. Follow the console guidance to review and accept the legal terms.

6. Click **Buy now** to complete the creation.

### Step 3: Configure private IPv6 address

Configure the IPv6 address for ECS\-A.

> **tip**

> This topic uses CentOS 7.9 as an example. For other operating systems, see [ECS configuration for private IPv6 addresses](https://docs.byteplus.com/en/docs/ecs/Configuring-private-IPv6-addresses-for-ECS-instances).

1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to open the network interface configuration file.​​

   `vi /etc/sysconfig/network-scripts/ifcfg-eth0`

3. Press `i` to enter edit mode. Verify if the file contains the following content. If not, input the specified content:

   ```Plain Text
   DHCPV6C=yes
   IPV6INIT=yes
   ```

4. Press `Esc` to exit edit mode, then type `:wq` and press Enter.

5. Execute `reboot` to restart the ECS instance.

6. Run `ip address show` command to view the configuration updates.

   As shown below, the IPv6 address of ECS's primary network interface has been successfully identified.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c8b37bfd8d015dc75994f620abfd933e.png)

### Step 4: Enable IPv6 Internet bandwidth

1. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select your target region.

3. Click the IPv6 gateway name of VPC\-X.

4. On the IPv6 Internet bandwidth tab, click **Enable Internet bandwidth** on the right side of ECS\-A's IPv6 address.

5. Configure parameters based on the table below.

   |Parameters |Notes |Sample value |
   |---|---|---|
   |Billing method |Currently only Pay\-as\-you\-go is supported. |Pay\-as\-you\-go |
   |Metering method |Select a metering method for IPv6 Internet bandwidth, supporting [Pay-by-bandwidth](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go#.5oyJ5bim5a695LiK6ZmQ6K6h6LS5) and [Pay-by-data-transfer](https://docs.byteplus.com/en/docs/IPv6/Pay-as-you-go#.5oyJ5a6e6ZmF5rWB6YeP6K6h6LS5). |Pay\-by\-data\-transfer |
   |ISP |Currently supports BGP (Multi\-ISP). |BGP (multi\-line) |
   |Maximum bandwidth |Set the bandwidth cap for IPv6 internet bandwidth, measured in Mbps. For specific scope, see [Bandwidth limits](https://docs.byteplus.com/en/docs/IPv6/Limits). |1 Mbps |
   |Bandwidth Package |Check to add to [Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package). When an IPv6 internet bandwidth instance is associated with a bandwidth package, it can share the package's bandwidth, effectively reducing internet bandwidth costs. |Not selected |
   |Agreement |Follow the console guidance to review and accept the legal terms. |\- |

6. Click **Apply** to complete the action.

### Step 5: View/Allow security group

View the ECS's security group and allow required traffic.

> **tip**

> The default security group automatically allows private network communication between ECSs within the same group and outbound internet access. For demonstration purposes, this topic uses inbound port 80 access as an example. Please adjust configurations according to your actual requirements.

1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select your target region.

3. In the left\-side navigation pane, click **Instances**.

4. Click the name of ECS\-A.

5. On the **Security Group** tab, you can view the current rule status.

6. Click **Configure** to the right of the default security group **Default**.

7. On the **Inbound rule** tab, click **Add rule**. Configure parameters based on the table below.

   |Parameters |Notes |Sample value |
   |---|---|---|
   |Priority |Set the priority of the security group rule. Range: 1\-100. Default: 1, which is the highest priority. |1 |
   |Policy |Select a strategy for the security group, supporting allow or deny. When priorities are equal, the deny policy takes precedence over the allow policy. |Allow |
   |Protocol type |Select the protocol for the security group. Support TCP, UDP, and ICMP. |TCP |
   |Port range |Limit the port range based on different protocol types. |80 |
   |Source |Type in the IP address or CIDR block allowed to access ECSs within the security group.​​ |::/0 |

8. Click **Confirm** to complete the action.

## Verify

1. Log in to the ECS instance ECS\-A.

2. At the command line, execute the command `ping 8.8.8.8`.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fcba3bf711e346482e905c915392e7c6.png)

3. In the command line, enter `ping6 <IPv6 public DNS, such as 240c::6666, 240c::6644>`. If data is returned, it confirms that ECS\-A can access internet services via its IPv6 address.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_640efa119971c7b677e8e469cccec6bc.png)
