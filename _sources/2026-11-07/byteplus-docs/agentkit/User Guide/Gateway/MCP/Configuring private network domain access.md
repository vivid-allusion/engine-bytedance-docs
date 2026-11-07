---
title: "Configuring private network domain access"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Configuring_private_network_domain_access"
---

If you create an MCP service in AgentKit and access a backend service through a private domain name, make sure that the private domain name can be resolved correctly in the selected VPC. You must also make sure that the resolved IP address has network connectivity to the VPC. This scenario refers to selecting **Fixed domain name** as the backend service type and selecting **Private network** as the access method. Therefore, the configuration takes effect only when both of the following conditions are met: the domain name can be resolved correctly in the selected VPC, and the IP address obtained through domain name resolution is accessible from the selected VPC.

This topic describes the configuration procedure for private domain name access based on three common scenarios. You can refer to the corresponding application scenario to complete the configuration.

## Quickly determine whether private domain name configuration is required

* **Scenario 1**: The domain name is a private domain name provided by a BytePlus cloud product. Domain names of this type can usually be resolved directly without additional configuration.

* **Scenario 2**: The backend service is deployed in a BytePlus VPC and uses a custom private domain name, for example,` api.internal.example.com`. In this case, add the domain name in PrivateZone and configure DNS records for the domain name.

* **Scenario 3**: The backend service is deployed on a third\-party cloud or in a self\-built IDC. In this case, the domain name must be resolved by the DNS system on the third\-party cloud or in the IDC. In addition to network connectivity, DNS forwarding configuration is required to forward DNS queries to the DNS service in the target network.

## Prerequisites

Before you start the configuration, confirm that you have the following information and conditions. The subsequent operations depend on this information.

* You have determined the BytePlus VPC and subnets to be associated when private network access is enabled for the MCP service.

* You have obtained the port on which the backend service actually listens, for example, 443 or 8080. You have allowed access from the BytePlus VPC in the security group, network ACL, and host firewall.

## Scenario 1: Domain names from BytePlus cloud products

If you use a domain name for ** private network access that is provided directly by a BytePlus cloud product**, this type of domain name can typically already be resolved in the BytePlus private DNS. In most cases, ** no additional DNS configuration is required, and** you can create the MCP service directly. For detailed instructions, see [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

### **Verification method**

If the selected VPC contains an ECS instance that you can log in to, you can verify resolution before you create the MCP service:

Execute the` nslookup <target domain name> `or `dig <target domain name>` command. If the domain name cannot be resolved in the target VPC, one of the following applies: the domain name is not a cloud product domain name that can be resolved directly in the current scenario, or the current VPC, network environment, or permission settings do not match your expectations. In this case, we do not recommend that you create the MCP service directly.

### **FAQ**

* If the domain name can be resolved as expected but access to the service fails, first check whether the required port is allowed, and then check whether the security group, network ACL, and service listening status are normal.

* If access fails after you change the VPC, note that network conditions can differ between VPCs. Perform resolution and connectivity verification again in the target VPC.

## Scenario 2: Custom domain names (self\-built in a BytePlus VPC)

This scenario applies when the backend service is deployed in a BytePlus VPC, and you plan the access domain name yourself, for example, `api.internal.example.com`. In this case, create a private domain name zone in BytePlus PrivateZone and configure DNS records for the domain name.

* **Full domain name**: For example, `api.internal.example.com`.

* **Zone**: Typically refers to the root domain part of the full domain name, for example `internal.example.com`.

### **Configuration method**

**Step 1: Add a domain name in PrivateZone**

1. Log in to the [PrivateZone console](https://console.byteplus.com/TrafficRoute/dns/privatezone/zones). On the "Domain management" page, select the "Domain name" tab and then click "Add domain".

2. On the **Add domain** page, refer to the following table to complete the configuration. This section lists only the required parameters. For a description of all parameters, refer to [Adding domain names](https://docs.byteplus.com/en/docs/byteplus-dns-suite/PU6MMV).

   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Domain name |The primary domain name. It can be a second\-level domain name or a domain name with more levels.<br><br><br>* For example, if you plan to use `api.internal.example.com`, the Zone is usually` internal.example.com`.<br><br>* Primary domain name restrictions:<br><br>   * It cannot be a domain name ending with `ivolces.com` or `privatelink.volces.com`. These domain names are reserved.<br><br>   * Only English letters (a\-z, A\-Z, case\-insensitive), numbers (0\-9), hyphens (\-), underscores (_), periods (.), and Chinese characters are allowed.<br><br>   * Hyphens (\-) cannot be used at the beginning or end of a single\-level domain name.<br><br>   * Multiple periods (.) cannot appear consecutively.<br><br>   * The length of a single\-level domain name cannot exceed 63 characters. Under the FQDN format, the total length of the domain name cannot exceed 254 characters. |
   ||Recursive DNS |Specify whether to enable recursive resolution for the domain name. For details, see [Implementing recursive resolution](https://docs.byteplus.com/docs/byteplus-dns-suite/uperuL).<br><br><br>* **Disabled**: (Default) If the domain name in the DNS query is a subdomain of the primary domain name but is not in any DNS record of the primary domain name, DNS resolution in PrivateZone fails.<br><br>* **Enabled**: If the domain name in the DNS query is a subdomain of the primary domain name but is not in the DNS records of the primary domain name, PrivateZone returns the query result from the public recursive DNS server.<br><br><br>> **warning**<br><br><br>> If the record type that you want to configure is CNAME and the record points to a public domain name, **we recommend that you enable recursive resolution for the domain name**. Otherwise, domain name resolution may fail.<br> |
   |VPC information |\- |Do not configure the effective scope of the domain name for now. After you create DNS records for the domain name, set the effective scope. |

3. After you complete the configuration, click Confirm **. ** You can then see the added domain name on the **Domain management ** page.

**Step 2: Add resolution records in a Zone**

1. On the "Domain management" page of the [PrivateZone console](https://console.byteplus.com/TrafficRoute/dns/privatezone/zones), click the **Domain name** tab. Then, click "Manage" in the Actions column for your domain name (for example, `internal.example.com`).

2. On the "**Record management**" page, click the "**DNS records**" tab, and then click "Create record set" **.**

3. Configure the parameters ** as described in the following table**, and then click "Submit". This section lists only the required parameters. For a description of all parameters, refer to [Adding DNS records](https://docs.byteplus.com/en/docs/byteplus-dns-suite/tmjP7G).

   |Category |Parameter |Description |
   |---|---|---|
   |Basic information |Domain name |The prefix of the subdomain name. Enter `api `since the full domain name` api.internal.example.com `is used as an example in this topic.<br><br><br>* To route user requests to `www.internal.example.com`, specify the domain name prefix as `www`.<br><br>* To route user requests to `internal.example.com`, specify the domain name prefix as `@`.<br><br>* To route user requests to all subdomains of `internal.example.com`, specify the domain name prefix as `*`.<br><br>* **Domain name rules**<br><br>   * Supports English letters (a\-z, A\-Z, case\-insensitive), numbers (0\-9), hyphens (\-), underscores (_), periods (.), wildcards (\*), @, and Chinese characters.<br><br>   * Hyphens (`-`) cannot be used at the beginning or end of a single\-level domain name.<br><br>   * Multiple periods (`.`)  cannot be used consecutively.<br><br>   * `@` can only indicate an empty domain name prefix and cannot coexist with other characters in the domain name prefix.<br><br>   * `*` can only be used in wildcard domain names:<br><br>      * `*` can only replace the leftmost single\-level domain name. For example, `*.example.com` is valid, but `example.*.com` and `abc*.example.com` are not.<br><br>      * Wildcard domain names can match domain names with the same level and their subdomains. For example, `*.example.com` matches all subdomains of `example.com`, including domain names such as `abc.example.com` or `abc.def.example.com`, but does not match `example.com`.<br><br>         > **warning**<br>         <br><br>         > The specific domain name affects how the wildcard domain name matches multi\-level subdomains. For example, if both `*.example.com` and `abc.example.com` exist in PrivateZone for private network resolution:<br>         <br><br>         * > DNS query requests for domain names ending with `abc.example.com` (such as `def.abc.example.com` or `123.abc.example.com`) fail to match.<br>         <br><br>         * > DNS query requests for domain names that do not end with `abc.example.com` but end with `example.com` (such as `123.def.example.com`) match `*.example.com`.<br>         <br><br>      * The matching priority of a specific domain name is higher than that of a wildcard domain name. For example, assume that a DNS query request uses the domain name` www.example.com`. If both` *.example.com` and `www.example.com` exist in PrivateZone for private network resolution, PrivateZone matches `www.example.com` first.<br><br>   * The length of a single\-level domain name cannot exceed 63 characters. Under the FQDN format, the total length of the domain name cannot exceed 254 characters. |
   ||Record type |Select the DNS record type based on the actual form of the backend service. For more information, see [Supported DNS record types](https://docs.byteplus.com/en/docs/byteplus-dns-suite/prQAdU).<br><br><br>* If the backend service has a fixed private IP address, you can use an A record or an AAAA record.<br><br>* If the backend service already has another available internal domain name, you can use a CNAME record. |
   |Record value |Record value |The record values in the record set. Each record value is one DNS record. How you specify the record value depends on the backend address:<br><br><br>* A record or AAAA record: Enter the actual private IP address of the backend service.<br><br>* CNAME record: Enter the target internal domain name.<br><br><br>If you cannot confirm whether to enter an IP or a domain name, we recommend that you first confirm the actual access address of the backend service before proceeding.<br><br>> **tip**<br><br><br>> If the record value is a domain name, it is displayed in FQDN format.<br> |
   ||Enable |Specifies whether the record value is enabled. If this parameter is set to **Enabled, ** the record value is included in DNS query responses. |

4. Return to the "Domain management" page and click "Edit associated VPCs" in the Actions column for your domain name (such as `internal.example.com`).

5. Click "Edit" to add VPC information.

   |Parameter |Description |
   |---|---|
   |Account |The BytePlus account used to associate with the VPC. |
   |VPC |The VPC associated with the domain name. Select **the VPC that you plan to use when you create the MCP service**. If the Zone is not associated with the correct VPC, DNS resolution for the domain name may fail in the target VPC, even if the DNS records are configured correctly.<br><br><br>* You can associate one or more VPCs. DNS resolution for the domain name is effective only within the associated VPCs.<br><br>* Make sure that the VPC uses the default private DNS server address. For information about the default private DNS server address of the VPC, refer to [Modifying private DNS](https://docs.byteplus.com/en/docs/vpc/Customizing-the-private-DNS). |

**Step 3: Verify domain name resolution and service port connectivity**

1. In a VPC associated with the Zone, select an ECS instance that you can log in to, and then execute the `nslookup <target domain name>` command. For example, execute `nslookup *.internal.example.com`.

2. Confirm that the command returns a resolution result.

   * If you configured an A record, confirm that the returned IP address matches the private IP address that you configured.

   * If you configured a CNAME record, confirm that the final resolution result is still the expected access address.

3. On the same ECS instance, test whether the target port, such as 443 or 8080, is accessible. If you verify only domain name resolution but do not verify port reachability, calls to the MCP service may still fail.

4. After all verifications pass, you can create the MCP service. For detailed operations, refer to [Creating MCP services](https://docs.byteplus.com/en/docs/agentkit/MCP_services).

### FAQ

* If you created a Zone but the domain name still cannot be resolved, check whether the Zone is associated with the correct VPC.

* If the resolution returns an incorrect IP address, check whether the specified record value and the record type are correct.

* If multiple resolution results exist for the same domain name, check whether conflicts exist among historical zones, self\-built DNS servers, or other resolution paths.

* If domain name resolution works but service access fails, check the listening address and listening port of the backend service, and the security group, network ACL, and host firewall configurations.

## Scenario 3: Private domain names in a third\-party cloud or a self\-built IDC (cross\-cloud or cross\-network)

This is the most complex scenario: the MCP service runs on the BytePlus side, but the domain name needs to be resolved by a DNS system in the third\-party cloud or the IDC. Generally, you need to complete the following two configurations:

1. First, establish stable network connectivity between the BytePlus VPC and the backend service, for example, by using Direct Connect or Cloud Enterprise Network (CEN).

2. Then, forward the DNS queries from the VPC on the BytePlus side to the DNS server in the target network.

### Scenario determination

If any of the following conditions are met, this scenario usually applies:

1. The backend service is deployed in a third\-party cloud environment such as Tencent Cloud, Alibaba Cloud, or Huawei Cloud.

2. The backend service is deployed in a self\-built IDC, an enterprise data center, or another private network environment.

3. The domain name must be resolved by the DNS service of a third\-party cloud or IDC itself, rather than having the final result returned by BytePlus PrivateZone directly.

### Network connectivity setup

Take a BytePlus VPC accessing a Tencent Cloud VPC as an example. First, complete the following:

1. The VPC on the BytePlus side and the VPC on the Tencent Cloud side are ready, and the two VPCs are connected through Direct Connect, a Transit Router (TR), CEN, or another private network solution. For the network connectivity configuration, refer to [Direct Connect - Best practices](https://docs.byteplus.com/en/docs/directconnect/best-practices-overview?lang=en).

2. Ensure that DNS queries sent from the BytePlus side can be received and processed by the target network. The approach is as follows: first, confirm whether the corresponding cloud vendor provides an "inbound DNS endpoint", a "DNS forwarding entry point", or an equivalent capability. Then, record the DNS server address and port that the cloud vendor provides.

   * **Tencent Cloud**: In the Tencent Cloud VPC to which the backend service belongs, create an inbound endpoint. Bind the inbound endpoint to a Tencent Cloud VPC that already has network connectivity with the BytePlus side, and record the IP address of the inbound endpoint. Record the DNS port used. Unless otherwise specified, the standard DNS port 53 is used. Confirm that the security policies on the target network side allow DNS requests. In most cases, check at least UDP 53 and TCP 53. For configuration details, see [Private DNS service address](https://cloud.tencent.com/document/product/1338/123753) in the Tencent Cloud official documentation.

   * **Alibaba Cloud**: Create a PrivateZone inbound endpoint in the Alibaba Cloud VPC where the backend service resides, record the inbound traffic service IP, and make sure that the security group allows traffic on port 53. For configuration details, see[ Inbound endpoint ](https://help.aliyun.com/zh/dns/pvtz-inbound-endpoint)in the Alibaba Cloud official documentation.

   * **Other cloud vendors**: The configuration approach is the same as Tencent Cloud. First, confirm whether the corresponding cloud vendor provides an "inbound DNS endpoint", a "DNS forwarding entry point", or an equivalent capability. Then, record the DNS server address and port that the cloud vendor provides. For detailed operations, refer to the documentation of the respective cloud provider or consult their customer service.

### Configuration method

Configuration in this scenario is relatively complex. A best practices document is available for this scenario. For detailed configuration, refer to [Integrating MCP services with gateway instances via private network domain names](https://docs.byteplus.com/en/docs/agentkit/Integrating_MCP_services_with_gateway_instances_via_private_network_domain_names).

### FAQ

* If you configure DNS before network connectivity is established, subsequent troubleshooting can easily go in the wrong direction.

* If DNS resolution fails, check the DNS server address returned by the target network side, and make sure that it is not confused with the management address or the console address.

* We recommend that you set the forwarding scope based on your business requirements. If the forwarding scope is too broad, unnecessary DNS queries are forwarded as well, which increases troubleshooting complexity.

* In standard DNS scenarios, both TCP 53 and UDP 53 must be allowed. If only one of them is allowed, check whether both ports are open.

* If the resolution result is correct but the service is still unreachable, check the backend port, routes, NAT, security policies, and host firewall configuration.
