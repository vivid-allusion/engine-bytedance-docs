---
title: "Assigning a private domain name"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Customizing-the-private-DNS"
---

## Scenarios

When there are numerous cloud resources within a private network, managing ECSs solely by IP addresses can be **challenging and hinder collaboration**. Assigning private domain names efficiently resolves this issue.

For example, assigning the domain name `server1.ecs.cn` to an ECS with IP 192.168.1.11. When other cloud resources privately access `server1.ecs.cn`, the corresponding private DNS service resolves this domain to 192.168.1.11 and returns it, allowing the other resources to access the ECS via 192.168.1.11.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81b5a26b31a4e63235e5c25b2a69ba03.png)

## Action description

There are two ways to assign private domain names to ECSs:

* **Self\-built or third\-party Private DNS Service**: If you need to use an existing self\-built or third\-party private DNS service in the cloud, you must modify the DnsServer address of the VPC, manually configure domain resolution records for cloud services within that DNS service, and independently handle the setup and maintenance of the private DNS environment.

* [PrivateZone](https://console.byteplus.com/TrafficRoute/dns/privatezone/zones) ** (Recommended)** : Based on the VPC's default DnsServer, it automatically configures domain resolution records for cloud services. Compared to self\-built or third\-party private DNS services, it offers lower latency, simpler configuration, and lower cost.

## Procedures

When using a self\-built or third\-party private DNS service, refer to the following steps to modify the DnsServer address.

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target project and region.

3. Click the name of target VPC.

4. Click the edit icon next to DNS and modify the value in the input field.

   A maximum of 5 DNS addresses are supported. Separate multiple IP addresses with half\-width commas (,).

5. Click **Save** to confirm the modification.

6. After completing the changes in the console, you must also log in to the ECS instance for the DNS configuration to take effect immediately.

   * If the DHCP service is enabled on your ECS instance, you will need to renew its DHCP service.

      * For existing instances within the VPC, you must perform one of the following operations: restart the ECS, restart the DHCP Client service, or restart the network service.

      * The configuration will automatically take effect for newly added ECS instances in the VPC.

   * If DHCP is not enabled on your ECS instance, you must configure the DNS settings manually. The process differs depending on the operating system. For example, on Linux:

      1. Run the `vi /etc/resolv.conf` command in the command line, then press `i` to enter edit mode.

      2. Change the IP address after the `nameserver` directive to the IP of your target DNS server. Each `nameserver` parameter corresponds to one DNS server address.

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e982af911c15d7203d63070a9445097.png)

      3. Press ESC to exit edit mode, type in :wq and press Enter to save and exit.

      4. Reboot the ECS.

## What to do next

* After changing the DNS server address, if you need to access cloud services (such as Torch Object Storage), you must also configure the corresponding domain name resolution records for these services on your private DNS server.

* Additionally, you need to allow traffic to and from the new DNS server's IP address in the relevant security groups and network ACLs (if applicable). For specific steps, see [Adding security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) and [Adding network ACL rules](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules).
