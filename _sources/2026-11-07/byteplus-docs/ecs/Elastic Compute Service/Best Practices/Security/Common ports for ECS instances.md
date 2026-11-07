---
title: "Common ports for ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Common_ports_for_ECS_instances"
---

When configuring a network ACL entry or security group rule, you need to specify a port number or port range. To help you add related rules more accurately, this topic describes common ports and temporary ports for ECS instances.

<span id=".6auY5Y2x56uv5Y-j"></span>
## High\-risk ports

The ports listed below are marked as high\-risk by some ISPs (Internet Service Providers). Even if these ports are allowed in a security group and network ACL, restricted accounts will still be unable to access them. Therefore, we recommend using non\-high\-risk ports.


|Protocol |Port |
|---|---|
|TCP |25 42 135 137 138 139 444 445 593 1025 1068 1434 3127 3128 3129 3130 4444 4789 5554 5800 5900 9996 |
|UDP |135 139 1026 1027 1028 1068 1433 1434 4789 5554 9996 |


For more information about Windows service and application ports, refer to the Microsoft official documentation: [Overview of Windows services and network port requirements](https://docs.microsoft.com/en-us/troubleshoot/windows-server/networking/service-overview-and-network-port-requirements).

<span id=".5bi455So56uv5Y-j"></span>
## Common ports


|Service |Port |Description |
|---|---|---|
|FTP |21 |Used for FTP services to upload/download files. |
|SSH |22 |Used for remotely connecting to Linux ECS instances. |
|Telnet |23 |Used for remotely logging in to ECS instances via the Telnet protocol. |
|HTTP |80 |Used for HTTP services to provide the access function. |
|POP3 |110 |Used for the POP3 protocol to send and receive emails. |
|NetBIOS |137, 138, 139 |* 137, 138: UDP ports used for file transfer via Network Neighborhood.<br><br>* 139: Used by requests to access NetBIOS/SMB services. Commonly used for Windows file/print sharing and Samba. |
|IMAP |143 |Used for the IMAP protocol to receive emails. |
|HTTPS |443 |Used for HTTPS services to provide the access function. HTTPS is a protocol that enables encryption and transmission over secure ports. |
|SQL Server |1433 |TCP port for SQL Server: Used to provide external services for SQL Server. |
|SQL Server |1434 |UDP port for SQL Server: Used to return the TCP/IP port used by SQL Server. |
|Oracle |1521 |Oracle communication port: Required to be allowed for the ECS instances with Oracle SQL deployed. |
|MySQL |3306 |Used to provide external services for MySQL databases. |
|Windows Server Remote Desktop Services |3389 |Port for Windows remote desktop service: Used to connect to Windows ECS instances. |
|Proxy |8080 |Port 8080: Commonly used for WWW proxy services to enable web browsing. |


<span id=".5Li05pe256uv5Y-j"></span>
## Temporary ports

Different ports are used based on which type of client initiating requests. Therefore, set the port range for the network ACL and security group based on your actual client type. The temporary port ranges of commonly used clients are as follows.


|Client |Port range |
|---|---|
|Linux |32768\-61000 |
|Windows Server 2003 |1025\-5000 |
|Windows Server 2008 and later versions |49152\-65535 |
|NAT Gateway |10000\-65535 |
