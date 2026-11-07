---
title: "FTP overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/FTP-overview"
---

File Transfer Protocol (FTP) is an application\-layer protocol used for file transfer between a client and a server over a computer network. Typically, it operates on two ports: 20 and 21.


* Port `20`: A data transfer port, used for uploading and downloading files.

* Port `21`: A command transfer port, used for transmitting commands.


<span id=".5L2_55So5qih5byP"></span>
## Usage modes

FTP supports two usage modes: active mode and passive mode.


* Active mode: Requires both a client and a server to open and listen on a port at the same time to create connections.

* Passive mode: A server creates a process to listen on the corresponding port. Due to firewall settings on most client machines and other factors, we recommend using passive mode to set up an FTP service.


<span id=".55So5oi35YiG57G7"></span>
## User types


* Real user: A user with an FTP service account. When a user of this type logs in to an FTP server, the default home directory is the one named after the user. By default, the vsftpd server classifies all created accounts as "Real user".

* Guest user: A user who can only access directories within the home directory and cannot access files outside of it. This user type offers a certain level of security.

* Anonymous user: A user who has no designated account on the FTP server and can access certain public resources anonymously. This user type has the lowest security level. Therefore, we recommend storing only public files with it.


<span id=".5bi46KeB6Zeu6aKY"></span>
## Operation guide


* [Setting up FTP sites (Ubuntu 22.04)](https://docs.byteplus.com/en/docs/ecs/Setting_up_FTP_sites_Ubuntu)

* [Setting up FTP sites (CentOS 7.6)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Linux)

* [Setting up FTP sites (Windows 2019)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Windows)

* [Setting up FTP sites (Windows 2012)](https://docs.byteplus.com/en/docs/ecs/Setting_up_FTP_sites_Windows_2012)


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

[FTP site setup FAQ](https://docs.byteplus.com/en/docs/ecs/FTP_site_setup_FAQ)
