---
title: "Viewing instance metadata"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata"
---

Instance metadata contains basic information of an ECS instance on the cloud platform. You can use metadata to configure or manage your instances. This topic describes how to view instance metadata.

<span id=".5L2_55So6aG755-l"></span>
## Usage notes

You can access instance metadata within the instance only. Since the data is not encrypted, anyone with access to the instance can view the metadata. If the metadata contains sensitive data, you should take proper measures to protect the sensitive data, such as access control and encryption.

<span id="69UMmAa4"></span>
## Instance metadata items

Expand the table below to view the instance metadata information you can access through the metadata service.


<span id="JkytIerV"></span>
### Summary table of instance metadata items

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Description</div>



* <div data-tips="true" data-tips-type="default">In the table below, replace <code>[mac]</code> and <code>[volume_id]</code> with the actual MAC address and volume ID of the instance.</div>


* <div data-tips="true" data-tips-type="default">Case\-insensitive.</div>


* <div data-tips="true" data-tips-type="default">":", "\-", "/" are allowed.</div>




|Metadata item |Description |Examples |
|---|---|---|
|mac |MAC address of the instance |00:16:3e:53:xx:xx |
|hostname |Instance hostname |iv\-ybo19qc2zqijuuub\*\*\*\* |
|uuid |Unique identifier of the instance |8508262e\-df5a\-11ec\-9ec1\-0c42a14c\*\*\*\* |
|instance_id |Instance ID |i\-ybo19qc2zqijuuub\*\*\*\* |
|instance_type_id |Instance type |ecs.g1.large |
|image_id |ID of the image used for instance startup |image\-4ay4awvwifaqrvqd\*\*\*\* |
|region_id |The ID of the region where the instance is located. |cn\-beijing |
|availability_zone |The availability zone where the instance is located. |cn\-beijing_a |
|private_ipv4 |The primary private IPv4 address of the primary network interface. |192.XX.XX.2 |
|eip_address |The EIP of the instance primary network interface. |10.XX.XX.88 |
|network/interfaces/macs/[mac]/primary_ip_address |The primary private IP address of the network interface. |172.XX.XX.127 |
|network/interfaces/macs/[mac]/eip_address |The list of EIPs associated with the instance. |10.XX.XX.1 |
|network/interfaces/macs/[mac]/vpc_id |The VPC ID of the instance. |vpc\-mini07ggfxmo5smt1b5f\*\*\*\* |
|network/interfaces/macs/[mac]/subnet_id |The subnet ID of the instance. |subnet\-13g3mh3hjglj43n6nu5if\*\*\*\* |
|network/interfaces/macs/[mac]/private_ip_addresses |The list of private IPv4 addresses assigned to network interfaces. |172.XX.XX.127 |
|network/interfaces/macs/[mac]/subnet_cidr_block |The subnet mask corresponding to the network interface. |172.XX.XX.0/24 |
|network/interfaces/macs/[mac]/gateway |IPv4 gateway address of the subnet where the network interface resides |172.XX.XX.1 |
|network/interfaces/macs/[mac]/interface_type |The network interface attribute. |* primary: the primary network interface<br><br>* secondary: the secondary network interface<br><br>* rdma: RDMA network interface, returned only for high\-performance compute\-optimized instances |
|payment/charge_type |Billing method |* PostPaid: Pay\-as\-you\-go<br><br>* PrePaid: Subscription |
|payment/created_at |The time when the instance is created. |2022\-4\-30 13:39:12 |
|payment/expired_at |The expiration date of the subscription\-based instance. |2022\-5\-30 13:39:12 |
|network/interfaces/macs/[mac]/security_group_ids |The ID of the security group with which the instance associates. |sg\-mini0ddjs3k05smt1b6n\*\*\*\* |
|network/interfaces/macs/[mac]/security_group_names |The name of the security group with which the instance associates. |default |
|block_devices |Disk ID list |vol\-3tf33o3o254bwbhd\*\*\*\* |
|block_devices/[volume_id]/device_type |You can query the volume type (Volume or local volume) based on the volume ID. |* The volume type. Valid values:<br><br>   * ESSD_PL0: ESSD PL0<br><br>   * ESSD_FlexPL: ESSD FlexPL<br><br>* The local volume type. Valid values:<br><br>   * LOCAL_SSD: local SSD<br><br>   * LOCAL_HDD: local HDD |
|serial_number |View the mapping relationship between Volume IDs and Volume serial numbers. |[{"serial_number":"3vqvpywv352tq1di\*\*\*\*","volume_id":"vol\-3vqvpywv352tq1di\*\*\*\*"}] |
|iam/security_credentials |The list of IAM roles associated with the instance. |ServiceRoleForECS |
|spot_instance_termination_time |The interruption time of spot instances. |2023\-02\-23T17:35:00Z |
|instance_network_bandwith_baseline |The network baseline bandwidth (outbound/inbound), in Mbps. |2560 |
|instance_network_bandwith_maximum |The network peak bandwidth (outbound + inbound), in Mbps. |12288 |
|instance_network_throughput_maximum |The maximum throughput (outbound + inbound), in Kpps. |150 |





<span id="UInUWXqD"></span>
## Access methods

<span id="CTQnuECn"></span>
### Overview

There are two ways to view metadata: Normal Mode and Security Hardening Mode.


* **Normal Mode**: Use CURL to access a preset fixed IP address and fetch instance metadata. This method is relatively straightforward and simple, with no complex authentication process required.

* **Security Hardening Mode**: The instance uses tokens for identity authentication to view instance metadata. Compared with Normal Mode, it provides better protection against Server\-Side Request Forgery (SSRF) attacks.



|**Item** |**Normal Mode** |**Security Hardening Mode** |
|---|---|---|
|Interaction mode |Request/Response |Session |
|Security verification |Authentication of source IP address within the same VPC |Authentication of source IP address within the same VPC + Authentication of credentials for accessing instance metadata<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The access credentials have the following characteristics:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Short validity period: The access credentials are valid for up to 6 hours. After expiration, the credentials will become invalid, and you need to re\-obtain them.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Instance association: The access credentials are only valid for one instance. If you copy the credentials and use them on another instance, access will be denied.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Proxy access denied: If the request includes the header <code>X-Forwarded-For</code>, the instance metadata will refuse to issue access credentials to enhance security.</div><br> |
|Viewing method |Direct access to the endpoint through commands |You must first obtain metadata access credentials for authentication, and then access the endpoint via a command. The request must contain the token header. |
|Security |Relatively low<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Requests are authenticated based on IP addresses. Attackers can forge the source IP address of requests to bypass IP address authentication and launch SSRF attacks, posing a risk of instance metadata leakage.</div><br> |Relatively high<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Before accessing metadata, you need to obtain the access credentials, which can only be generated within the ECS instance. The credentials are time\-sensitive and apply only to specific instances. Attackers find them difficult to guess or forge, capable of preventing most SSRF attacks.</div><br> |


<span id="SMDxOmnU"></span>
### Procedure


<Tabs>
<Tab zoneid="DNt8D9AUzy" title="Security Hardening Mode">
<TabTitle>Security Hardening Mode</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">In the following commands, the arguments to be set are described as follows:</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0"><code><validity period of metadata access credentials></code>: The value ranges from 1 to 21,600 seconds.</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0"><code><metadata></code>: Replace with the specific metadata item you want to query. For details, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata#.5a6e5L6L5YWD5pWw5o2u6aG5">Instance metadata items</a>.</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0"><code><token></code>: Replace with the obtained token. If the token is invalid, an "Unauthorized request" response will be returned. The token validation rules are as follows:</div>


   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">It must be within the validity period.</div>


   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">It must be a token for this instance.</div>




<Tabs>
<Tab zoneid="lFHtdJcxWH" title="For Linux instances">
<TabTitle>For Linux instances</TabTitle>

1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to obtain metadata access credentials, with a specified validity period.

   ```Bash
   curl --location --request PUT '100.96.0.96/latest/api/token' \
   --header 'X-volc-ecs-metadata-token-ttl-seconds:<validity period of metadata access credentials>'
   ```
   

3. Execute the following command to obtain instance metadata.

   ```Bash
   curl --location '100.96.0.96/latest/<metadata>' \
   --header 'X-volc-ecs-metadata-token: <token>'
   ```
   

   The response is displayed as follows (For example, the `metadata` is `payment/charge_type`).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_500d7cfae0b2ad0bc561c58b5c5feb71.png) </span>


</Tab>
<Tab zoneid="mndl75KhKb" title="For Windows instances">
<TabTitle>For Windows instances</TabTitle>

1. [Log in to Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the following command to obtain metadata access credentials, with a specified validity period.

   ```Bash
   Invoke-RestMethod -Uri "http://100.96.0.96/latest/api/token" -Method PUT -Headers @{"X-volc-ecs-metadata-token-ttl-seconds"="<validity period of metadata access credentials>"}
   ```
   

3. Execute the following command to obtain instance metadata.

   ```Bash
   Invoke-RestMethod -Uri "http://100.96.0.96/latest/<metadata>" -Headers @{"X-volc-ecs-metadata-token"="<token>"}
   ```
   

   The response is displayed as follows (For example, the `metadata` is `payment/charge_type`).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f710443998150a178f856930bf1ed25.png) </span>


</Tab>
</Tabs>



</Tab>
<Tab zoneid="kABLfKDd8t" title="Normal Mode">
<TabTitle>Normal Mode</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Replace <code><metadata></code> with the specific metadata item you want to query. For details, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata#.5a6e5L6L5YWD5pWw5o2u6aG5">Instance metadata items</a>.</div>



1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following commands.

   * For Linux instances

      ```Plain Text
      curl http://100.96.0.96/latest/<metadata>
      ```
      

   * For Windows instances (PowerShell)

      ```Plain Text
      Invoke-RestMethod http://100.96.0.96/latest/<metadata>
      ```
      


</Tab>
</Tabs>


<span id="JWIS4ZO1"></span>
## Configure metadata access mode

<span id="XvnBLzs3"></span>
### Overview

When creating an instance, you can set the metadata access mode to Normal Mode and Security Hardening Mode or Security Hardening Mode.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Security Hardening Mode is currently in Beta. If you need a trial, please contact your account manager to apply.</div>


* <div data-tips="true" data-tips-type="warning">To enable Security Hardening Mode, the following conditions must be met:</div>


   * <div data-tips="true" data-tips-type="warning">The instance type is <strong>not GPU.</strong></div>


   * <div data-tips="true" data-tips-type="warning">The instance image is a custom image that supports Security Hardening Mode. <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images">Learn more</a></div>


* **Security Hardening ** **Mode**: Only allows accessing instance metadata through a token\-based authentication method, enhancing security further.

* **Normal Mode and Security Hardening Mode:**  allows access to instance metadata directly through the normal mode or the token\-based security hardening mode.


<span id="iMBo0td9"></span>
### Procedure

Refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances#.6Ieq5a6a5LmJ6YWN572u) to complete the **Basic configuration** and **Network configuration** in sequence. Then, in the  ** ** **Custom configuration** stage, expand "Advanced options" and select the access mode for metadata. Follow the on\-screen instructions step by step to create the instance.

&nbsp;

&nbsp;
