---
title: "SealSuite SD-WAN domain scheduling principles and rules"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/sd-wan-domain-scheduling-principles-and-rules"
---

## Features and use cases

When SealSuite SD\-WAN domain scheduling resolves service domains, it selects an egress based on employee identity or the access branch. It also associates the DNS result with subsequent service forwarding. This document is intended for network administrators. It explains how cloud VPN with employee routing and branch networking with branch routing work, including domain matching rules and packet paths.

When employees access business systems through cloud VPN, the corresponding egress can be selected based on employee identity. When branch offices access the same service domain, the corresponding egress can be selected based on the ingress CPE. Domain scheduling associates "which domain is accessed" with "which egress is used."

**Scenario comparison**

|Scenario |DNS query source |Traffic ingress |Traffic egress |Scheduling granularity |
|---|---|---|---|---|
|Cloud VPN + employee routing |Cloud VPN client `dnsproxy` |**Access POP** (POP\-VPN, the POP node accessed by the client) |**Egress POP** → egress CPE / vCPE |Distinguish egress nodes by user identity |
|Branch networking + branch routing |Branch ingress CPE `dnsmasq` |**Ingress CPE** → access POP |**Egress POP** → egress CPE |Distinguish egress CPEs by ingress CPE |

**Role of DNS scheduling**

* **Select an egress by service domain**: SaaS, internal systems, and cross\-border resources are usually accessed by domain. DNS scheduling selects an egress based on the domain and associates domain rules with subsequent IP packet forwarding.

* **Use scheduling results for packet forwarding**: Central DNS returns the service A record and tun IP. The client creates a fake IP mapping. The ingress CPE creates a mapping between the real service IP and the tun IP. Subsequent packets are forwarded through the SD\-WAN tunnel to the specified egress CPE based on the mapping.

* **Share domain rules across two scenarios**: Employee routing and branch routing use the same tenant domain matching rules. They match egress CPEs based on user identity and ingress CPE, respectively.

## Basic concepts and architecture

|Concept |Description |
|---|---|
|Scheduled domain |A service domain that must be processed by SealSuite SD\-WAN domain scheduling. After a request matches the scheduling scope, the resolution request is sent to central DNS. |
|Central DNS |Selects an egress based on tenant domain rules and employee or ingress CPE information, and coordinates domain resolution on the egress side. |
|Ingress CPE |An access device on the branch side. It receives DNS requests and service traffic from branch endpoints. |
|Egress CPE / vCPE |An egress device connected to the network where the target resource resides. It handles egress\-side domain resolution and service forwarding. |
|POP |An SD\-WAN network access node. The access POP receives traffic from clients or ingress CPEs. The egress POP forwards traffic to the egress CPE. |
|Real service IP |The target service IPv4 address obtained by the egress CPE through DNS resolution. |
|Tunnel virtual IP (tun IP) |A tunnel address assigned by a POP for forwarding within the SD\-WAN network. |
|Client mapping address (fake IP) |The address returned by the client to the local application. The client maintains its associations with the real service IP and tunnel virtual IP. |

The overall architecture includes the management plane, DNS scheduling control plane, and the access, backbone, and egress networks that carry service traffic. Central DNS selects the egress and coordinates resolution. Clients, CPEs, and POPs handle service forwarding.

The following figure shows two access methods: employee client access and branch CPE access. Dashed lines indicate configuration delivery. Thin solid lines indicate DNS queries and egress resolution coordination. Thick solid lines indicate service forwarding paths. Traffic is forwarded between the access POP and the egress POP through the backbone network.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/review-20261021/sdwan-architecture-en.svg)

## Employee access scheduling process

When employees access service domains through cloud VPN, the client handles DNS query routing, scheduling result mapping, and access\-side packet translation. The following sections describe the complete process in three stages: resolution, request forwarding, and return packet processing.

**Responsibilities of the two DNS groups on the client**

Before the client accesses cloud VPN, it requests `/vpn/list`. The server delivers two DNS groups for the cloud VPN:

|DNS group |Purpose |Downstream recursive / authoritative |
|---|---|---|
|Tenant\-configured DNS (primary / secondary) |Resolves **non\-scheduled domains** (common public internet / standard SaaS) |Upstream recursive / DNS server |
|Central DNS IP |Resolves **scheduled domains** (items that match the client Bloom Filter) |Aggregated by central DNS → local resolution by egress CPE |

**Scheduled domain determination and extension fields**

* **Domain determination**: The client `dnsproxy` treats a Bloom Filter hit as a scheduled domain and sends the query to central DNS. If no hit occurs, the query is sent to tenant\-configured DNS.

* **Request extension fields**:

   * **Cloud VPN client routing**: The request carries "tenant + suggested egress node." Central DNS uses the egress CPE suggested by the client.

   * **Employee routing**: The request carries information such as "tenant + employee identity + device identity + client virtual IP + connection mode." Central DNS determines the egress CPE based on employee routing rules and may override the value suggested by the client.

* **Response content**: In addition to the A record, the central DNS response carries the tun IP. The client uses it to create a local three\-part mapping: "real service IP ↔ fake IP ↔ tun IP."

### Scheduling sequence

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/review-20261021/sdwan-sequence-1-en.svg)

**Processing steps**

1. **Preparation**: The client obtains two configuration groups from `/vpn/list`: tenant DNS and central DNS. After the client accesses cloud VPN, the access POP assigns a virtual IP and tun IP. The egress CPE has established a persistent connection with central DNS through gRPC 49920.

2. **Domain determination**: The application sends a DNS query to the local `dnsproxy`. A Bloom Filter hit routes the query to central DNS. Otherwise, the query is routed to tenant\-configured DNS.

3. **Send the query**: `dnsproxy` sends the DNS query to central DNS over UDP 443. The extension fields carry employee routing information.

4. **Select an egress**: Central DNS matches domain rules by tenant. It then matches the egress CPE based on employee identity.

5. **Local resolution**: Central DNS sends a resolution request to the egress CPE through gRPC 49920. The egress CPE initiates local resolution against a DNS server. After obtaining the service A record, it returns the record to central DNS.

6. **Return the resolution result**: Central DNS returns the A record + tun IP to the client over UDP 443. The client `dnsproxy` assigns a fake IP, creates a "real IP ↔ fake IP" mapping, and finally returns the fake IP to the application.

7. **Data\-plane forwarding**: The application sends packets to the fake IP. The client performs DNAT to translate it to the tun IP and sends the packets into the WireGuard tunnel. The packets travel along "access POP → backbone → egress POP → egress CPE." The egress CPE restores the real service destination IP and performs SNAT to forward packets to the destination resource. Return packets go back to the client through the tunnel. The client restores addresses and delivers the packets to the application.

### Access example

The following example describes an employee in the Chinese mainland accessing a US SaaS application through cloud VPN. The service domain is `portal.example.com`, and the egress is a US vCPE. The following network parameters are examples.

**Example network parameters**

|Element |Value (example) |
|---|---|
|Target domain |`portal.example.com` |
|Client physical NIC IP |`192.168.1.100` |
|Client VPN virtual IP (assigned by the access POP) |`100.64.10.5` |
|Employee identity (anonymized) |`openUID=1234`, `deviceID=5678` |
|Access POP · POP\-VPN (SH\-POP) |`192.0.2.10` (external WireGuard, port randomized by tenant) |
|Central DNS service IP |`10.100.0.53` (UDP 443) |
|Egress POP (US\-POP) |Backbone egress POP |
|Egress CPE · US\-vCPE (cpe\-us\-1) |Physical NIC `10.20.30.40` |
|Egress CPE tun IP (assigned and delivered by the egress POP) |`169.254.1.10` |
|Real service IP (local resolution result of the egress CPE) |`203.0.113.50` |
|Client local fake IP |`30.100.0.7` (assigned by dnsproxy after receiving the response) |

**Stage 1: DNS resolution**

Resolution path: client → central DNS → egress CPE.

1. The application initiates `gethostbyname("portal.example.com")`, and the system DNS points to `dnsproxy`.

2. `dnsproxy` determines a hit through the Bloom Filter → the query goes to central DNS instead of tenant\-configured DNS.

3. `dnsproxy` constructs a DNS query packet. The extension fields are filled with employee routing information: `{tenant=T, openUID=1234, deviceID=5678, client virtual IP=100.64.10.5, connection mode=WireGuard}`.

4. The query is sent to central DNS `10.100.0.53` over **UDP 443**.

5. Central DNS matches the domain rules of tenant T and hits `portal.example.com`. It then matches the egress CPE based on employee identity: `cpe-us-1` (US\-vCPE).

6. Central DNS sends a resolution request through the persistent **gRPC 49920** connection established with `cpe-us-1`:  *"Locally resolve portal.example.com for tenant T."*

7. US\-vCPE requests the A record from a DNS server based on the /etc/resolv.conf configuration and obtains `A = 203.0.113.50`.

8. US\-vCPE returns the A record to central DNS through the persistent gRPC connection.

9. Central DNS obtains `tun IP = 169.254.1.10` based on the "tun IP that the egress POP has assigned to US\-vCPE" and returns `A + tun IP` to the client `dnsproxy` over UDP 443.

10. `dnsproxy` assigns the fake IP `30.100.0.7` from `30.100.0.0/16` and creates the three\-part mapping `fake IP 30.100.0.7 ↔ real IP 203.0.113.50 ↔ tun IP 169.254.1.10`. It returns `30.100.0.7` to the application as the A record.

**Stage 2: Request forwarding**

The following packet structure shows the packet format after client wg\-go completes DNAT and when the packet enters the WireGuard tunnel. The following table lists field changes hop by hop from the application layer to the destination server.

```text
+------------------------------------------------------------+
|                     Outer IP Header (IPv4)                 |
|                                                            |
|   src   = 192.168.1.100      (Client physical NIC)         |
|   dst   = 192.0.2.10            (Ingress POP · POP-VPN)       |
|   proto = 17 (UDP)           TTL = 64                      |
+------------------------------------------------------------+
|                       Outer UDP Header                     |
|                                                            |
|   sport = <random>           dport = <tenant WG port>      |
|                              (per-tenant, randomized)      |
+------------------------------------------------------------+
|                 WireGuard Transport Data                   |
|                                                            |
|   msg_type = 4  (Transport Data)                           |
|   receiver_index / counter / encrypted-payload             |
|   AEAD encrypted with per-tenant WireGuard session key     |
+------------------------------------------------------------+
              [ Encrypted · carries the inner packet ]
+------------------------------------------------------------+
|                     Inner IP Header (IPv4)                 |
|                                                            |
|   src     = 100.64.10.5      (Client VPN vIP)              |
|   dst     = 169.254.1.10     (Egress CPE tun IP)           |
|   proto   = 6 (TCP)          TTL = 64                      |
|   options : original_dst = 203.0.113.50                    |
+------------------------------------------------------------+
|                       Inner TCP Header                     |
|                                                            |
|   sport = <random>           dport = 443                   |
|   flags = SYN                                              |
+------------------------------------------------------------+
|                     Application Payload                    |
|                                                            |
|   TLS ClientHello · SNI = portal.example.com               |
+------------------------------------------------------------+
```

The application initiates a TCP SYN to `30.100.0.7:443`. The following table shows field changes from inside to outside:

|Hop |Inner src |Inner dst |Notes |
|---|---|---|---|
|① Sent by the application |`100.64.10.5` |`30.100.0.7` (fake IP) |Application perspective |
|② Client wg\-go DNAT |`100.64.10.5` |`169.254.1.10` (tun IP) |Original dst=`203.0.113.50` is written to the IP option for egress CPE restoration |
|③ Client WireGuard encapsulation |Outer `192.168.1.100:random → 192.0.2.10:tenant WG port` ||UDP, port randomly assigned by tenant |
|④ Access POP · POP\-VPN decapsulation |`100.64.10.5` |`169.254.1.10` |Routes to the backbone based on the tun IP |
|⑤ Access POP → egress POP backbone forwarding |Outer encapsulation remains unchanged. The packet is routed across regions between POPs over the backbone (not WireGuard) ||Backbone tunnel |
|⑥ Egress POP → US\-vCPE |`100.64.10.5` |`169.254.1.10` |Forwarded to the egress CPE through a WireGuard tunnel |
|⑦ US\-vCPE destination address restoration and SNAT |`10.20.30.40` (physical NIC) |`203.0.113.50` (real IP) |Restores dst from the IP option and performs SNAT for internet egress |

**Stage 3: Return packet processing**

Return packets pass through the target server, egress CPE, egress POP, backbone network, and access POP in sequence, and then return to client wg\-go. The following packet structure corresponds to the WireGuard packet that the access POP sends to client wg\-go. The outer layer is the public UDP packet of the final hop. The inner layer has completed return\-path DNAT on the egress CPE, and the real source address is stored in the IP option. After client wg\-go receives the packet, it restores the inner source address from the tun IP to the fake IP based on the mapping, and then delivers the packet to the application.

```text
+------------------------------------------------------------+
|                     Outer IP Header (IPv4)                 |
|                                                            |
|   src   = 192.0.2.10            (Ingress POP · POP-VPN)       |
|   dst   = 192.168.1.100      (Client physical NIC)         |
|   proto = 17 (UDP)           TTL = 64                      |
+------------------------------------------------------------+
|                       Outer UDP Header                     |
|                                                            |
|   sport = <tenant WG port>   dport = <client random>       |
+------------------------------------------------------------+
|                 WireGuard Transport Data                   |
|                                                            |
|   msg_type = 4  (Transport Data)                           |
|   receiver_index / counter / encrypted-payload             |
|   AEAD encrypted with per-tenant WireGuard session key     |
+------------------------------------------------------------+
              [ Encrypted · carries the inner packet ]
+------------------------------------------------------------+
|                     Inner IP Header (IPv4)                 |
|                                                            |
|   src     = 169.254.1.10     (Egress CPE tun IP)           |
|   dst     = 100.64.10.5      (Client VPN vIP)              |
|   proto   = 6 (TCP)          TTL = 64                      |
|   options : original_src = 203.0.113.50                    |
+------------------------------------------------------------+
|                       Inner TCP Header                     |
|                                                            |
|   sport = 443                dport = <original random>    |
|   flags = SYN + ACK                                        |
+------------------------------------------------------------+
|                     Application Payload                    |
|                                                            |
|   TLS ServerHello · portal.example.com                     |
+------------------------------------------------------------+
```

Then client wg\-go restores the inner `src = 169.254.1.10` to `src = 30.100.0.7` (fake IP) based on the local mapping. It also uses `original_src = 203.0.113.50` in the IP option to maintain tuple consistency. The application finally sees `src=30.100.0.7:443, dst=100.64.10.5:<random>`.

1. The destination server `203.0.113.50` returns a packet with `src=203.0.113.50, dst=10.20.30.40`.

2. US\-vCPE matches the SNAT session and restores `dst=100.64.10.5` in reverse. It also records src in the IP option and changes it to `src=169.254.1.10`.

3. The packet returns to the client through the reverse tunnel along "egress CPE → egress POP → backbone → access POP → client."

4. Client wg\-go receives the inner `src=169.254.1.10, dst=100.64.10.5`, reads the real src `203.0.113.50` from the IP option, and restores it to `30.100.0.7` (fake IP) based on the existing mapping.

5. The application sees the return packet `src=30.100.0.7, dst=100.64.10.5`, which corresponds to the same connection as the request.

## Branch networking scheduling process

DNS queries from branch endpoints are received by the ingress CPE. The ingress CPE handles domain\-based DNS query routing and access\-side packet translation. Central DNS selects an egress based on the ingress CPE.

**DNS query routing on the ingress CPE**

* Branch endpoints use the ingress CPE LAN IP as the default DNS.

* `dnsmasq` on the ingress CPE determines matches by **strict domain suffix matching**:

   * If the query matches a scheduled domain, it is forwarded to central DNS over **UDP 443**.

   * If the query does not match, it is forwarded to an upstream DNS server (public recursive / customer\-hosted).

**Extension fields (branch routing)**

Request extension fields carry "tenant + ingress CPE identifier." Central DNS uses this information to locate the tenant and then **matches the egress CPE based on the ingress CPE**. If no match occurs, it falls back to the tenant\-level default egress. The same domain can use different egresses in different branches.

### Scheduling sequence

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/review-20261021/sdwan-sequence-2-en.svg)

**Processing steps**

1. **Preparation**: The branch ingress and egress CPEs have been assigned tun IPs by POPs. The egress CPE has established a persistent connection with central DNS through gRPC 49920.

2. **Ingress DNS query routing**: DNS requests from branch endpoints first reach the ingress CPE. `dnsmasq` determines whether a domain is a scheduled domain by strict domain suffix matching.

3. **Send the query**: If a match occurs, the query is forwarded to central DNS over UDP 443. The extension fields carry branch routing information (tenant + ingress CPE).

4. **Select an egress**: Central DNS matches domain rules by tenant. It then matches the egress CPE based on the ingress CPE. If no match occurs, it falls back to the tenant default egress.

5. **Local resolution**: Central DNS sends a resolution request to the egress CPE through gRPC 49920. The egress CPE initiates local resolution against a DNS server and returns the result.

6. **Return the resolution result**: Central DNS returns the A record + tun IP to the ingress CPE over UDP 443. The ingress CPE responds to the branch endpoint.

7. **Data\-plane forwarding**: The branch endpoint sends packets based on the A record. The ingress CPE performs DNAT + WireGuard tunnel encapsulation. The packets travel along "access POP → backbone → egress POP → egress CPE." The egress CPE restores the real service destination address and performs SNAT to forward packets to the destination resource. Return packets go back to the ingress CPE through the tunnel. The ingress CPE restores addresses and forwards the packets to the branch endpoint.

### Access example

The following example describes a branch office in the Chinese mainland accessing a US resource through branch networking. The service domain is `portal.example.com`, and the egress is a US vCPE. The following network parameters are examples.

**Example network parameters**

|Element |Value (example) |
|---|---|
|Target domain |`portal.example.com` |
|Branch endpoint IP |`10.10.1.50` |
|Ingress CPE LAN IP (also the branch DNS) |`10.10.1.1` |
|Ingress CPE ID |`cpe-sh-1, WAN IP 198.51.100.20 (example)` |
|Ingress CPE tun IP (assigned and delivered by the access POP) |`169.254.2.20` |
|Access POP (SH\-POP) |Public IP 192.0.2.10 (WireGuard port randomized by tenant) |
|Central DNS service IP |`10.100.0.53` (UDP 443) |
|Egress POP (US\-POP) |Backbone egress POP |
|Egress CPE · US\-vCPE (cpe\-us\-1) |Physical NIC `10.20.30.40` |
|Egress CPE tun IP (assigned and delivered by the egress POP) |`169.254.1.10` |
|Real service IP (local resolution result of the egress CPE) |`203.0.113.50` |

**Stage 1: DNS resolution**

Resolution path: branch endpoint → ingress CPE → central DNS → egress CPE.

1. The branch endpoint `10.10.1.50` sends a DNS query for `portal.example.com` to `10.10.1.1:53` (ingress CPE LAN DNS).

2. `dnsmasq` on the ingress CPE hits a scheduled domain by strict domain suffix matching → the query enters the central DNS forwarding path.

3. `dnsmasq` constructs a DNS query packet. The extension fields are filled with branch routing information: `{tenant=T, ingress CPE=cpe-sh-1, WAN IP 198.51.100.20 (example)}`.

4. The query is sent to central DNS `10.100.0.53` over **UDP 443**.

5. Central DNS matches the domain rules of tenant T and hits `portal.example.com`. It then matches the egress CPE based on ingress CPE `cpe-sh-1, WAN IP 198.51.100.20 (example)`: `cpe-us-1` (US\-vCPE). If no match occurs, it falls back to the tenant default egress.

6. Central DNS sends a resolution request through the persistent **gRPC 49920** connection established with `cpe-us-1`:  *"Locally resolve portal.example.com for tenant T."*

7. US\-vCPE requests the A record from a DNS server based on the /etc/resolv.conf configuration and obtains `A = 203.0.113.50`.

8. US\-vCPE returns the A record to central DNS through the persistent gRPC connection.

9. Central DNS obtains `tun IP = 169.254.1.10` from the tun IP table assigned by the egress POP, and returns `A + tun IP` to the ingress CPE over UDP 443.

10. The ingress CPE creates the `203.0.113.50 ↔ 169.254.1.10` mapping locally, and then returns `A = 203.0.113.50` to the branch endpoint as the DNS response. The branch endpoint is not aware of the tun IP.

**Stage 2: Request forwarding**

The following packet structure shows the packet format after the ingress CPE completes DNAT and when the packet enters the WireGuard tunnel. The following table lists field changes hop by hop from the branch endpoint to the destination server.

```text
+------------------------------------------------------------+
|                     Outer IP Header (IPv4)                 |
|                                                            |
|   src   = 198.51.100.20     (Ingress CPE WAN)                             |
|   dst   = 192.0.2.10      (Ingress POP)                          |
|   proto = 17 (UDP)           TTL = 64                      |
+------------------------------------------------------------+
|                       Outer UDP Header                     |
|                                                            |
|   sport = <random>           dport = <tenant WG port>      |
|                              (per-tenant, randomized)      |
+------------------------------------------------------------+
|                 WireGuard Transport Data                   |
|                                                            |
|   msg_type = 4  (Transport Data)                           |
|   receiver_index / counter / encrypted-payload             |
|   AEAD encrypted with per-tenant WireGuard session key     |
+------------------------------------------------------------+
              [ Encrypted · carries the inner packet ]
+------------------------------------------------------------+
|                     Inner IP Header (IPv4)                 |
|                                                            |
|   src     = 10.10.1.50       (Branch endpoint)             |
|   dst     = 169.254.1.10     (Egress CPE tun IP)           |
|   proto   = 6 (TCP)          TTL = 64                      |
|   options : original_dst = 203.0.113.50                    |
+------------------------------------------------------------+
|                       Inner TCP Header                     |
|                                                            |
|   sport = <random>           dport = 443                   |
|   flags = SYN                                              |
+------------------------------------------------------------+
|                     Application Payload                    |
|                                                            |
|   TLS ClientHello · SNI = portal.example.com               |
+------------------------------------------------------------+
```

The branch endpoint initiates a TCP SYN to `203.0.113.50:443`. The following table shows field changes from inside to outside:

|Hop |Inner src |Inner dst |Notes |
|---|---|---|---|
|① Sent by the branch endpoint |`10.10.1.50` |`203.0.113.50` |Endpoint perspective. dst is the real service IP |
|② Ingress CPE hits SD\-WAN PBR + DNAT |`10.10.1.50` |`169.254.1.10` (egress CPE tun IP) |Translated based on the previously created `203.0.113.50 ↔ 169.254.1.10` mapping. Original dst is stored in the IP option for restoration |
|③ Ingress CPE WireGuard encapsulation |Outer `198.51.100.20 (ingress CPE WAN) → 192.0.2.10 (access POP):(tenant WG port)` ||UDP, port randomly assigned by tenant |
|④ Access POP decapsulation |`10.10.1.50` |`169.254.1.10` |Routes to the backbone based on the tun IP |
|⑤ Access POP → egress POP backbone forwarding |Outer encapsulation remains unchanged. The packet is routed across regions between POPs over the backbone (not WireGuard) ||Backbone tunnel |
|⑥ Egress POP → US\-vCPE |`10.10.1.50` |`169.254.1.10` |Forwarded to the egress CPE through a WireGuard tunnel |
|⑦ US\-vCPE destination address restoration and SNAT |`10.20.30.40` (physical NIC) |`203.0.113.50` (real IP) |Restores the real dst from the IP option and performs SNAT for internet egress |

**Stage 3: Return packet processing**

Return packets pass through the target server, egress CPE, egress POP, backbone network, and access POP in sequence, and then return to the ingress CPE. The following packet structure corresponds to the WireGuard packet that the access POP sends to the ingress CPE. The outer layer is the public UDP packet of the final hop. The inner layer has completed return\-path DNAT on the egress CPE, and the real source address is stored in the IP option. After the ingress CPE receives the packet, it restores the inner source address from the tun IP to the real service IP based on the mapping, and then delivers the packet to the branch endpoint.

```text
+------------------------------------------------------------+
|                     Outer IP Header (IPv4)                 |
|                                                            |
|   src   = 192.0.2.10      (Ingress POP)                         |
|   dst   = 198.51.100.20     (Ingress CPE WAN)                            |
|   proto = 17 (UDP)           TTL = 64                      |
+------------------------------------------------------------+
|                       Outer UDP Header                     |
|                                                            |
|   sport = <tenant WG port>   dport = <CPE random>         |
+------------------------------------------------------------+
|                 WireGuard Transport Data                   |
|                                                            |
|   msg_type = 4  (Transport Data)                           |
|   receiver_index / counter / encrypted-payload             |
|   AEAD encrypted with per-tenant WireGuard session key     |
+------------------------------------------------------------+
              [ Encrypted · carries the inner packet ]
+------------------------------------------------------------+
|                     Inner IP Header (IPv4)                 |
|                                                            |
|   src     = 169.254.1.10     (Egress CPE tun IP)           |
|   dst     = 10.10.1.50       (Branch endpoint)             |
|   proto   = 6 (TCP)          TTL = 64                      |
|   options : original_src = 203.0.113.50                    |
+------------------------------------------------------------+
|                       Inner TCP Header                     |
|                                                            |
|   sport = 443                dport = <original random>    |
|   flags = SYN + ACK                                        |
+------------------------------------------------------------+
|                     Application Payload                    |
|                                                            |
|   TLS ServerHello · portal.example.com                     |
+------------------------------------------------------------+
```

After receiving the decrypted inner packet, the ingress CPE reads `original_src = 203.0.113.50` from the IP option, restores the inner `src = 169.254.1.10` to `src = 203.0.113.50`, and forwards the packet to the branch endpoint based on the branch LAN route. The branch endpoint finally sees `src=203.0.113.50:443, dst=10.10.1.50:<random>`, which corresponds to the same connection as the request.

1. The destination server `203.0.113.50` returns a packet with `src=203.0.113.50, dst=10.20.30.40`.

2. US\-vCPE matches the SNAT session and restores the inner `dst=10.10.1.50` in reverse. It also records src in the IP option and changes it to `src=169.254.1.10`.

3. The packet returns to the ingress CPE through the reverse tunnel along "egress CPE → egress POP → backbone → access POP → ingress CPE."

4. The ingress CPE receives the inner `src=169.254.1.10, dst=10.10.1.50`, reads the real src `203.0.113.50` from the IP option, restores the source address, and forwards the packet to the branch endpoint.

5. The branch endpoint sees the return packet `src=203.0.113.50, dst=10.10.1.50`, which is consistent with the four\-tuple sent earlier.

## Differences between the two scenarios

Both scenarios share the central DNS scheduling capability, but they differ in DNS entry, domain determination method, egress selection basis, and the address visible to the endpoint.

|Dimension |Cloud VPN + employee routing |Branch networking + branch routing |
|---|---|---|
|DNS query source |Client `dnsproxy` |Ingress CPE `dnsmasq` |
|Query protocol / port |UDP 443 |UDP 443 |
|Scheduled domain determination method |Bloom Filter hit |Strict domain suffix matching |
|Suffix matching limits |Second / third level. Fourth\-level and deeper domains are not supported. `*.abc.com` is equivalent to `abc.com` |Suffixes of any depth. Wildcards such as `*.abc.com` are not supported |
|Egress selection basis |Match the egress CPE by user identity. The client\-suggested value may be overridden |Match the egress CPE by ingress CPE. If no match occurs, fall back to the default egress |
|fake IP allocation |Locally assigned by the client as `30.100.x.y` |The ingress CPE returns the real service IP and does not assign a fake IP to branch endpoints |
|Traffic ingress |Access POP (POP\-VPN) |Ingress CPE → access POP |
|Traffic egress |Egress POP → egress CPE |Egress POP → egress CPE |
|Scheduling granularity |Employee level / device level |Branch level / ingress CPE level |

## Domain matching rules and notes

Clients and branch ingress CPEs use different domain matching methods. When the same rule is used in both scenarios, consider the domain level, wildcard, and suffix scope.

|Configuration format |Cloud VPN client side (Bloom Filter) |Branch side (dnsmasq suffix matching) |
|---|---|---|
|`abc.com` |Matches `abc.com` and any of its subdomains |Matches all domains that end with `.abc.com` |
|`*.abc.com` |Equivalent to `abc.com` |**Does not take effect** (wildcards are not recognized) |
|`x.y.z.abc.com` (fourth level or deeper) |**Does not take effect** |Matches all domains with this suffix |
|`x.com` |Matches `x.com` and its subdomains |Matches all domains that end with `x.com` (including `abcx.com`) |

* **Fourth\-level domain limit on the cloud VPN side**: Scenarios that must distinguish `a.b.c.example.com` from `d.e.f.example.com` are not supported on the client side. Use branch\-side matching rules instead.

* **Short suffix risk on the branch side**: Do not use short suffixes that cannot uniquely identify the service, such as `x.com`. Use exact matching or a longer suffix if needed.

* **DoH / Secure DNS bypass**: Chrome / Firefox Secure DNS bypasses the client `dnsproxy` and directly uses public DNS. Scheduling will fail.

## Required protocols and ports

Domain queries, egress\-side resolution coordination, and service tunnels use different links. Clients and ingress CPEs query central DNS over UDP 443. The egress CPE actively establishes a gRPC bidirectional connection over TCP 49920. Central DNS uses this connection to send resolution requests and receive results.

|Link |Initiator |Port |Protocol / packet |Purpose |
|---|---|---|---|---|
|Cloud VPN client → central DNS |Client `dnsproxy` |**UDP 443** |DNS packet + extension fields (cloud VPN client routing / employee routing) |Scheduled domain resolution. **Stateless, not gRPC** |
|Ingress CPE → central DNS |Ingress CPE `dnsmasq` |**UDP 443** |DNS packet + extension fields (branch routing) |Scheduled domain resolution. **Stateless, not gRPC** |
|Egress CPE ↔ central DNS |Egress CPE initiated |**TCP 49920** |**gRPC bidirectional persistent connection** |Carries egress CPE registration, heartbeats, and resolution requests sent by central DNS |
|Client / CPE ↔ access POP |Data plane |UDP (port randomly assigned by tenant) |WireGuard |Data tunnel. **tun IP is assigned and delivered by the access POP** |
|Egress POP ↔ egress CPE |Data plane |UDP (port randomly assigned by tenant) |WireGuard |Data tunnel. **The egress CPE\-side tun IP is assigned and delivered by the egress POP** |
|Backbone POP ↔ POP |Data plane |— |Cross\-region backbone forwarding (WireGuard is not used) |Routes and forwards inner packets between POPs |

**Link and address assignment notes**

* **All DNS queries to central DNS use UDP 443** (not 53 or gRPC 49920). The query link is stateless. Central DNS does not need to maintain persistent connections for a large number of clients / ingress CPEs.

* **gRPC 49920 is used only on the egress CPE side**: Central DNS uses this connection to send resolution requests to the egress CPE. The log message `dns_grpc: connection refused` specifically indicates an exception in this channel.

* **tun IP (** **`169.254.x.y`** **) is assigned and delivered by POPs**. CPEs do not assign it by themselves. Centralized POP management avoids subnet conflicts and centrally maintains tunnel address assignments.

### Address CIDR blocks and mapping relationships

The following table summarizes the purpose, allocator, and generation time of each address type. Tunnel virtual IPs are assigned by POPs. Client fake IPs are assigned by the client after it receives the scheduling response.

|Mapping / CIDR block |Default CIDR block |Allocated or maintained by |Allocation time |
|---|---|---|---|
|tun IP (tunnel virtual IP) |`169.254.0.0/16` |**Assigned by access and egress POPs** |When the WireGuard tunnel is established |
|fake IP ↔ real IP |`30.100.0.0/16` |Client `dnsproxy` local assignment |When the central DNS response is received |
|fake IP ↔ tun IP |Client internal |Client `wg-go` |When DNAT is performed for outbound packets |
|tun IP ↔ real IP |Egress CPE internal |Egress CPE dst restore |When packets pass through the CPE |
|Client virtual IP |`100.64.0.0/16` |Assigned by the access POP |When the client accesses cloud VPN |
