---
title: "Security group use cases"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Security-group-use-cases"
---

Security groups control the traffic for associated network interfaces. This topic provides common configuration examples.

## Precautions

For security reasons, it is recommended to exercise caution when allowing traffic on commonly used service ports such as SSH (22), Redis (6379), MemCached (11211), MySQL (3306), SMB (445), RDP (3389), and SQL Server (1433).

## Preparations

Before configuration, you need to understand the security group rule matching description. For details, please refer to [matching description](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).

## Configuration examples

### Remote connection

* **Connect to a Linux ECS**

   To connect remotely to a Linux ECS via SSH, allow port 22 in the server's security group. Configuration examples:

   |Direction |Priority |Strategy |Protocol type |Port range |Source |
   |---|---|---|---|---|---|
   |Inbound |Set priority (e.g. 1) |Allow |TCP |22 |0.0.0.0/0 or specified IP address |

* **Connect to a Windows ECS**

   To connect remotely to a Windows ECS via RDP, allow port 3389 in the server's security group. Configuration examples:

   |Direction |Priority |Strategy |Protocol type |Port range |Source |
   |---|---|---|---|---|---|
   |Inbound |Set priority (e.g. 1) |Allow |TCP |3389 |0.0.0.0/0 or specified IP address |

### Web service

When deploying a web service accessible to all internet users, you need to configure your security group to allow traffic over the ports designated for HTTP and HTTPS protocols. Configuration examples:

|Direction |Priority |Strategy |Agreement |Port range |Source |
|---|---|---|---|---|---|
|Inbound |Set priority (e.g. 1) |Allow |TCP |80 |0.0.0.0/0 |
|Inbound |Set priority (e.g. 1) |Allow |TCP |443 |0.0.0.0/0 |

### Ping test

Use the Ping utility to test connectivity between your ECSs. To do this, you need to add a rule allowing ICMP protocol in the relevant security group. Configuration examples:

|Direction |Priority |Strategy |Protocol type |Port range |Source |
|---|---|---|---|---|---|
|Inbound |Set priority (e.g. 1) |Allow |ICMP |All |0.0.0.0/0 |

### Specify address and port

If your service should only be accessible through specific ports and to specific IP addresses, use the configuration example below:

|Direction |Priority |Strategy |Protocol type |Port range |Source |
|---|---|---|---|---|---|
|Inbound |Set priority (e.g. 1) |Allow |TCP |Specified port (e.g., 1100) |Specified IP address (e.g., 192.168.1.22) |
