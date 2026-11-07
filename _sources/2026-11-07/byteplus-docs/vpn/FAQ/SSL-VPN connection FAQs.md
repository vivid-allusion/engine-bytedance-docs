---
title: "SSL-VPN connection FAQs"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/SSL-VPN-connection-FAQs"
---

* [How many SSL-VPN client certificates can one SSL-VPN server create simultaneously?](https://docs.byteplus.com/en/docs/52/5088#p9L5uEmH)

* [How long is the validity period of an SSL-VPN client certificate?](https://docs.byteplus.com/en/docs/52/5088#70cSz3oV)

* [How to handle an expired SSL-VPN client certificate?](https://docs.byteplus.com/en/docs/52/5088#XtYVC0va)

* [What impact does deleting an SSL-VPN client certificate have on downloaded certificates?](https://docs.byteplus.com/en/docs/52/5088#SSLY7WKo)

* [How to check the expiration time of an SSL-VPN client certificate?](https://docs.byteplus.com/en/docs/52/5088#3522FVgF)

* [Can an SSL-VPN client certificate be used on only one client device?](https://docs.byteplus.com/en/docs/52/5088#2xHxSRU6)

* [Are there any restrictions on the Local Network when creating an SSL-VPN server?](https://docs.byteplus.com/en/docs/52/5088#RDSiNTiO)

* [Are there any restrictions on the Client IP Pool when creating an SSL-VPN server?](https://docs.byteplus.com/en/docs/52/5088#FvkV72uc)

* [Can different clients use the same client IP for an SSL-VPN connection?](https://docs.byteplus.com/en/docs/52/5088#0iKtT1My)

* [How to troubleshoot common errors by checking the SSL-VPN connection logs?](https://docs.byteplus.com/en/docs/52/5088#Hk1WXWBa)


<span id="p9L5uEmH"></span>
## How many SSL\-VPN client certificates can one SSL\-VPN server create simultaneously?

Currently, one SSL\-VPN server can create up to 200 SSL\-VPN client certificates simultaneously.

<span id="70cSz3oV"></span>
## How long is the validity period of an SSL\-VPN client certificate?

The default validity period of an SSL\-VPN client certificate is 3 years.

<span id="XtYVC0va"></span>
## How to handle an expired SSL\-VPN client certificate?

If an SSL\-VPN client certificate expires, you need to delete the existing SSL\-VPN client certificate and all related configurations, then re\-download the SSL\-VPN client certificate from the SSL VPN Client Certificate console. For procedure, see [Downloadign an SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate?LibVersion=3.26.0).

<span id="SSLY7WKo"></span>
## What is the impact of deleting an SSL\-VPN client certificate on the downloaded certificate?

After deleting the SSL\-VPN client certificate in an SSL\-VPN connection, the downloaded SSL\-VPN client certificate becomes invalid immediately and can no longer be used to establish an SSL\-VPN connection.

<span id="3522FVgF"></span>
## How to check the expiration time of an SSL\-VPN client certificate?

You can check the expiration time of the SSL\-VPN client certificate in the SSL VPN Client Certificate console.

<span id="2xHxSRU6"></span>
## Can an SSL\-VPN client certificate be used on only one client device?

An SSL\-VPN client certificate can be used on multiple client devices.

<span id="RDSiNTiO"></span>
## Are there any restrictions for the Local Network CIDR block when creating an SSL\-VPN server?

In SSL\-VPN, Local Subnet refers to the CIDR blocks that can be accessed by clients over an SSL\-VPN connection. A local subnet can be a CIDR block of a VPC subnet, a CIDR block of a data center interconnected with the VPC via Direct Connect, or a CIDR block of a cloud service such as TOS or a cloud database. The Local Network has the following restrictions:


* Recommended mask for local subnets: `/8` to `/32`.

* The local subnet must not conflict with the remote CIDR.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each SSL\-VPN server can add up to <strong>5</strong> Local Networks.</div>


<span id="FvkV72uc"></span>
## Are there any restrictions for the Client IP Pool when creating an SSL\-VPN server?

In SSL\-VPN, client IP pool refers to the CIDR blocks assigned by an SSL\-VPN server to client devices for communication. It is not the local CIDR blocks of client devices. When a client connects through an SSL\-VPN connection, the VPN gateway will assign an IP address from the specified client IP pool for client use. The client IP pool has the following restrictions:


* Mask of remote CIDR: `/16` to `/28`.

* The client IP pool cannot conflict with the local subnet.

* The client IP pool cannot be the same as the VPN gateway route.

* The client IP pool cannot conflict with route entries in the VPN gateway's default route table.

* The client IP pool cannot overlap with `100.64.0.0/10`, `169.254.0.0/16`, `127.0.0.0/8`, `224.0.0.0/4`, or `240.0.0.0/4` CIDR blocks.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Overlap here means the client IP pool neither includes nor belongs to the above CIDR blocks.   </div>
   

* The number of available IP addresses under the client IP pool mask must exceed four times the selected SSL Max Connections when creating the VPN gateway. For example: if the SSL Max Connections is 10, the client IP pool must have more than 40 available IP addresses.


<span id="0iKtT1My"></span>
## Can different clients use the same client IP for SSL\-VPN connections?

Different SSL\-VPN client certificates can use the same client IP to initiate connections at **different time intervals**, but cannot use the same client IP to initiate connections at **the same time interval**.

<span id="Hk1WXWBa"></span>
## How to troubleshoot common errors by checking the SSL\-VPN connection logs?

After you [enable](https://docs.byteplus.com/en/docs/vpn/Viewing-IPsec-VPN-connection-logs#.5q2l6aqk5LqM77ya5byA5ZCvSVBzZWPov57mjqXml6Xlv5c=) VPN Connect Log, you can view the SSL\-VPN connection logs in the console. Refer to the table below to match log keywords with corresponding troubleshooting methods.


|**Log keyword** |**Error cause** |**Troubleshooting method** |
|---|---|---|
|* Connection reset, restarting [\-1]SIGUSR1[soft,connection\-reset] received, client\-instance restarting<br><br>* TCP/UDP: Closing socket |Client actively or automatically reconnected. |* Check if the client was restarted or reconnected at the time indicated in the log.<br><br>* Check the validity of the SSL\-VPN client certificate.​ If the certificate is expired, [delete](https://docs.byteplus.com/en/docs/vpn/Deleting-an-SSL-client-certificate) the current certificate and all its configurations, then [re-download and install it](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate).<br><br>* Check the client's system time.​ The time difference between the client and the SSL\-VPN server must not exceed 10 minutes. We recommend adjusting the client's time to match the standard time. |
|* OpenSSL: error:1416F086:SSL routines:tls_process_server_certificate:certificate verify failed<br><br>* TLS_ERROR: BIO read tls_read_plaintext error<br><br>* TLS Error: TLS object \-\> incoming plaintext read error<br><br>* TLS Error: TLS handshake failed |SSL verification failed, or the client's system time differs significantly from the server's time. ||
|VERIFY ERROR: certificate has expired |Certificate expired. |Check the validity of the SSL\-VPN client certificate.​ If the certificate is expired, [delete](https://docs.byteplus.com/en/docs/vpn/Deleting-an-SSL-client-certificate) the current certificate and all its configurations, then [re-download and install it](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate). |
|No server certificate verification method has been enabled |SSL VPN certificate verification failed. ||
|* Options error: \-\-ca fails with 'ca.crt': No such file or directory (errno=2)<br><br>* Options error: \-\-cert fails with 'vsc\-\*\*\*\*.crt': No such file or directory (errno=2)<br><br>* WARNING: cannot stat file 'vsc\-\*\*\*\*.key': No such file or directory (errno=2)<br><br>* Options error: \-\-key fails with 'vsc\-\*\*\*\*.key'<br><br>* Options error: Please correct these errors. |Certificate configuration error. ||
|Authenticate/Decrypt packet error: cipher final failed |Mismatch between SSL\-VPN server and client encryption configurations. |Confirm that the encryption algorithm of the installed SSL\-VPN client certificate matches the one configured on the SSL\-VPN server. If they do NOT match: Delete the current SSL\-VPN client certificate and all its configurations, then [re-download and install the SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The encryption algorithm for the SSL\-VPN client certificate corresponds to the value of the <code>cipher</code> field in the <strong>config.ovpn</strong> file.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can view the SSL\-VPN server's encryption algorithm in <a href="https://console.byteplus.com/vpn/sslServer">the SSL VPN Server console</a>: click the name of the target SSL\-VPN server instance, and check the details on the instance details page.</div><br> |
|* There are no TAP\-Windows adapters on this system. You should be able to create a TAP<br><br>* CreateFile failed on TAP device<br><br>* All TAP\-Win32 adapters on this system are currently in use |Missing TAP virtual Ethernet adapter on the client. Reinstall required. |1. Confirm whether you checked the **TAP Virtual Ethernet Adapter​**  option during the OpenVPN software installation. If the option was NOT checked, you can either manually create a virtual Ethernet adapter or reinstall the OpenVPN software.<br><br>2. If **TAP Virtual Ethernet Adapter** was checked during installation, exit the OpenVPN software and try running it again with administrator privileges. |
|* network is unreachable<br><br>* TLS Error: TLS key negotiation failed to occur within 60 seconds (check your network connectivity)<br><br>* TLS Error: TLS handshake failed |Network unreachable or connectivity issues. |1. Use the `ping` or `mtr` command on the client to test connectivity to the public IP address of the VPN gateway and assess network quality.<br><br>   * If the public network line quality is poor (e.g., high latency or packet loss), contact your ISP (Internet Service Provider) for assistance with troubleshooting.<br><br>   * If connectivity is normal, proceed to Step 2.<br><br>2. Check the SSL\-VPN server [logs](https://docs.byteplus.com/en/docs/vpn/Viewing-IPsec-VPN-connection-logs) to see if connection attempts from the client are recorded.<br><br>   * If client connection attempts are NOT found in the logs, try changing the **port** used by the SSL\-VPN server, then [re-download and install the SSL-VPN client certificate on the client](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate).<br><br>   * If client connection attempts are found in the logs, proceed to Step 3.<br><br>3. Check whether the SSL\-VPN server protocol is set to **TCP**​ (which offers higher reliability).<br><br>   * If the server protocol is NOT TCP: Change the SSL\-VPN server protocol to TCP. You can view the current protocol type on [the SSL VPN Server console](https://console.byteplus.com/vpn/sslServer): click the name of the target SSL\-VPN server instance, and check the details on the instance details page.<br><br>   * If the server protocol is TCP: Try restarting the client or reinstalling the VPN software on the client. If multiple VPN software applications are installed on the client, we recommend using only one to establish the SSL\-VPN connection.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In long\-distance cross\-region access scenarios, if the issue persists after changing the SSL\-VPN server protocol to <strong>TCP</strong>, we recommend resolving it through a public network acceleration product.   </div><br>    |
|* MANAGEMENT: \>STATE:1676379239,TCP_CONNECT,,,,,,<br><br>* TCP: connect to [AF_INET]\*.\*.\*.\*:1194 failed: Unknown error |Protocol or port mismatch between client and SSL\-VPN server. |Try changing the **protocol** and **port** used by the SSL\-VPN server, then [re-download and install the SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate). |
|MANAGEMENT: \>STATE:1676370715,WAIT,,,,, |SSL Max Connections quota reached. |Check the number of connected clients under the VPN gateway instance to confirm if the quota is exceeded.<br><br><br>* If the client count exceeds the quota, you can: upgrade the quota for SSL Max Connections, or temporarily disconnect some clients to free up resources.<br><br>   > After disconnection, wait approximately 5 minutes for the system to automatically release the resource quota.   <br>   <br><br>* If the client count is within the quota, change the SSL\-VPN server's **protocol** to **TCP**, then [re-download and install the SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate). |
|* Data Channel Offload doesn't support DATA_V1 packets<br><br>* Upgrade your server to suggest an upgrade to the server version |The VPN software version on the client is incompatible with the BytePlus SSL\-VPN server. |Install the VPN software recommended for VPN gateway on the client. For more information, see [Configuring the client](https://docs.byteplus.com/en/docs/vpn/Configuring-the-client). |
|* TLS error: The server has no TLS ciphersuites in common with the client. Your \-\-tls\-cipher setting might be too restrictive.<br><br>* OpenSSL: error:1408A0C1:SSL routines:ssl3_get_client_hello:no shared cipher |No common TLS cipher suites between SSL\-VPN server and client, causing no common encryption algorithm available. ||
