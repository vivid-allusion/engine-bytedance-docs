---
title: "Troubleshooting cloud VPN domain access exceptions"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/cloud-vpn-domain-access-troubleshooting"
---

After you connect to cloud VPN, business websites may still fail to open, time out, or load pages incompletely. This document is intended for enterprise IT and network administrators. It describes how to choose a troubleshooting direction based on cURL request results, and how to locate exceptions by using Access Policies, CPE logs, and packet capture results.

## Prepare before troubleshooting

This document applies to access exceptions for cloud VPN domain resources. It does not apply to access exceptions for pure IP resources or basic network outages in the office network.

* Before you start troubleshooting, confirm that the Endpoint has successfully connected to cloud VPN.

* The Admin Console and CPE checks in this document are performed by enterprise IT or network administrators. Operating a CPE requires the corresponding device management permissions. If the VPN connection has not been established, see [Troubleshoot VPN connections (in Chinese)](https://help.feilian.cn/help-center/vpn-connection-troubleshooting-guide).

* Record the failure time, Endpoint operating system, SealSuite client version, connection node, and affected user scope. Prepare a business address that can reproduce the issue. Use the same domain name and port in subsequent tests to compare results from the Endpoint, browser, and CPE.

## Identify the failure symptom

First confirm the domain name of the failed request. Then use cURL to identify the stage where the request stops. Finally, select the corresponding section based on the result. The following troubleshooting sections are separate branches for different symptoms. You do not need to perform them one by one.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/round2-20261021/vpn-diagram-0-en.svg)

Select the corresponding comparison method and check direction based on the failure scope.

|Impact scope |Comparison method and check direction |
|---|---|
|Access still fails after changing networks |Verify from other networks and from the target site side. Check the target service or its egress. Failures across multiple networks are a troubleshooting clue, but cannot independently determine the root cause. |
|Exception occurs only after connecting to cloud VPN |Run cURL on the Endpoint. Check DNS, Access Policy, and forwarding path based on the failure stage. |
|Exception occurs only on individual Endpoints |Compare with normal Endpoints for version, DNS proxy, system proxy, security software, and network filters. |
|Intermittent failures or fluctuating speed |Record the occurrence time. Compare path detection, link quality, and packet captures at both ends. |

After identifying the abnormal segment, verify only the related adjustment each time, and retest the same domain name. After access is restored, record the test time and result. If the issue persists, retain command output, configurations, logs, and packet captures for further analysis.

### 1. Identify the affected resource

Follow these steps to distinguish access issues for the main page and dependent resources.

1. Compare working and affected endpoints. Confirm whether the issue occurs only after connecting to cloud VPN, and whether all users are affected or only some users are affected.

2. Confirm the domain name and port where access fails.

   If the main page cannot open, confirm the target address from the browser address bar. If the main page can open but some functions are abnormal, open the **Network** panel in Developer Tools, refresh the page, and find the domain name of the failed request.

   A page may access multiple domain names, such as APIs, scripts, images, videos, and CDNs.

3. Select a domain name and port that can reproduce the issue.

   In subsequent tests on the Endpoint, browser, and CPE, test the same object and record each result and time.

### 2. Test with cURL

Use cURL on the affected endpoint to view resolution, connection, handshake, and HTTP response details. Ping uses ICMP and does not carry the HTTP Host or TLS SNI, so it cannot replace domain access tests. Follow the operations below to obtain complete output, and then select a troubleshooting direction.

Perform the following tests on the Endpoint where the issue occurs. Replace the domain name and port in the examples with actual values.

1. Run the request and retain the complete output.

   ```shell
   curl -Iv https://<affected-domain>:<port>
   ```

   Use `http://` for HTTP websites. The command parameters are described below.

   |Parameter |Description |
   |---|---|
   |`-I` |Sends a HEAD request and obtains only response headers. Some services process HEAD requests differently from GET requests used by browsers. If necessary, remove `-I`, or copy the actual failed browser request for comparison. |
   |`-v` |Outputs details such as resolution, connection, handshake, and request response. |
   |`-k` |Skips certificate verification. Use it only for comparison with normal verification results. A successful request with this parameter does not mean the certificate is valid. |

2. Determine the failure stage based on the output.

   If no address is resolved, check DNS. If the connection fails after `Trying` appears, check TCP. If the handshake fails after `Connected to` appears, check TLS and access permissions. If an HTTP response is received, continue to check the status code and business result.

3. If certificate verification fails, append `-k` for a comparison test.

   ```shell
   curl -Ikv https://<affected-domain>:<port>
   ```

   This operation determines whether the request can continue after skipping certificate verification. It must not be used as a fix for certificate issues.

The following request example shows output from the DNS resolution, TCP connection, TLS handshake, and HTTP response stages. The example uses the `-k` parameter to skip certificate verification. It is only used to identify log stages. Remove this parameter when checking certificates. Addresses, times, and certificate information are subject to the actual output.

```bash
root@macos ~ # curl -Ikv https://www.baidu.com
# 1. DNS resolution stage
* Host www.baidu.com:443 was resolved.
* IPv6: (none)
* IPv4: 30.100.0.9, 30.100.0.10, 30.100.0.11, 30.100.0.12

# 2. TCP connection stage
*   Trying 30.100.0.9:443...
* Connected to www.baidu.com (30.100.0.9) port 443
* ALPN: curl offers h2,http/1.1

# 3. TLS handshake stage
* (304) (OUT), TLS handshake, Client hello (1):
* (304) (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS handshake, Certificate (11):
* TLSv1.2 (IN), TLS handshake, Server key exchange (12):
* TLSv1.2 (IN), TLS handshake, Server finished (14):
* TLSv1.2 (OUT), TLS handshake, Client key exchange (16):
* TLSv1.2 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (OUT), TLS handshake, Finished (20):
* TLSv1.2 (IN), TLS change cipher, Change cipher spec (1):
* TLSv1.2 (IN), TLS handshake, Finished (20):
* SSL connection using TLSv1.2 / ECDHE-RSA-AES128-GCM-SHA256 / [blank] / UNDEF
* ALPN: server accepted http/1.1

# 4. TLS certificate verification stage
* Server certificate:
*  subject: C=CN; ST=Beijing; L=Beijing; O=Beijing Baidu Netcom Science Technology Co., Ltd.; CN=baidu.com
*  start date: Jul  9 02:32:55 2026 GMT
*  expire date: Jan 24 02:32:55 2027 GMT
*  issuer: C=BE; O=GlobalSign nv-sa; CN=GlobalSign RSA OV SSL CA 2018
*  SSL certificate verify ok.

# 5. ALPN protocol negotiation stage
* using HTTP/1.x
> HEAD / HTTP/1.1

# 6. HTTP request stage
> Host: www.baidu.com
> User-Agent: curl/8.7.1
> Accept: */*
>
* Request completely sent off

# 7. HTTP response stage
< HTTP/1.1 200 OK
HTTP/1.1 200 OK
< Cache-Control: private, no-cache, no-store, proxy-revalidate, no-transform
< Content-Length: 0
< Content-Type: text/html
< Pragma: no-cache
< Server: bfe
< Date: Thu, 24 Sep 2026 11:13:40 GMT
<

# 8. HTTP connection keep-alive stage
* Connection #0 to host www.baidu.com left intact
```

### 3. Select a troubleshooting direction

Based on the complete output of the same request, select the corresponding section in the following table to troubleshoot the specific issue. Timeouts may occur at different stages. Do not rely only on the exit code. After each adjustment, retest the same service address and confirm whether the result changes.

|Request result |Troubleshooting section |
|---|---|
|The domain name cannot be resolved, resolution times out, or the address does not match expectations |[Domain resolution exception](https://docs.byteplus.com/en/docs/31/123492#.5Z-f5ZCN6Kej5p6Q5byC5bi4) |
|The address is resolved, but the TCP connection fails |[TCP connection failure](https://docs.byteplus.com/en/docs/31/123492#.dGNwLei_nuaOpeWksei0pQ==) |
|TCP is connected, but the request fails during the TLS handshake |[TLS handshake failure](https://docs.byteplus.com/en/docs/31/123492#.dGxzLeaPoeaJi-Wksei0pQ==) |
|Certificate verification fails, or an abnormal HTTP response is received |[Certificate verification or HTTP response exception](https://docs.byteplus.com/en/docs/31/123492#.6K-B5Lmm5qCh6aqM5oiWLWh0dHAt5ZON5bqU5byC5bi4) |
|The cURL request meets expectations, but browser access is still abnormal |[cURL is normal, but web access is abnormal](https://docs.byteplus.com/en/docs/31/123492#.Y3VybC3mraPluLjvvIzkvYbnvZHpobXorr_pl67lvILluLg=) |

## Domain resolution exception

If cURL cannot resolve a domain name, or the resolved address is inconsistent with the resource routing configuration, first check the DNS used by the Endpoint. Then check central DNS and the egress CPE based on the result. A resolved address only means a DNS response was obtained. You still need to check whether the address meets expectations. For example, if the routing configuration for a domain name should return a `30.100.x.x` scheduling address, but a public IP address is returned, check resource matching and the resolution path.

### Determine the resolution result

Run `nslookup <affected-domain>` on the affected endpoint, and record the DNS server, response status, and returned address. The following example shows output through a local DNS proxy.

```bash
root@macos ~ # nslookup www.baidu.com
Server:        127.0.0.1
Address:       127.0.0.1#53

Name:    www.baidu.com
Address: 30.100.0.24
Name:    www.baidu.com
Address: 30.100.0.25
```

Select a check direction based on the resolution symptom.

|Resolution symptom |Check direction |
|---|---|
|Request times out |Check whether the local DNS proxy is listening, whether the request is sent, and whether the response is returned. Then check the reachability of the physical network and central DNS. |
|NXDOMAIN, SERVFAIL, or no required record |Record the specific response status. NXDOMAIN indicates that the queried domain name does not exist. SERVFAIL indicates that the server cannot complete the query. Missing required records does not equal NXDOMAIN. Check the domain name, upstream DNS, and CPE logs. Do not directly determine that this is a gRPC failure. |
|Unexpected address returned |Check the domain resource, employee routing policy, and whether the system or browser bypasses the SealSuite DNS proxy. |
|Expected address returned |Continue to check the TCP connection and access permissions. |

### Check the Endpoint DNS proxy

After cloud VPN is connected, the local DNS proxy listens on `127.0.0.1:53`. After a request enters the proxy, domain rules are matched through a Bloom Filter. Requests that hit cloud VPN domain rules are sent to central DNS. Requests that do not hit rules use physical network DNS.

```text
Application DNS request
  → Local DNS Proxy (127.0.0.1:53)
    → Hits cloud VPN domain rules: sent to central DNS
    → Does not hit rules: uses physical network DNS
```

Common exceptions can be checked as follows. Confirm whether a third\-party VPN conflict exists based on the port, request path, and results before and after disabling the component.

|Common exception |Possible cause |Verification and handling |
|---|---|---|
|`127.0.0.1:53` is not listening |DNS Proxy is not started, fails to start, or has a port conflict. |Check port usage and SealSuite logs. After closing the conflicting program, reconnect to cloud VPN. |
|The port is normal, but the request does not enter the proxy |System DNS order, system proxy, third\-party VPN, or network filtering components changed the request path. |Check system DNS and proxy settings. Disable third\-party network components and retest. |
|Browser and nslookup results are inconsistent |The browser has DoH, private DNS, or an independent proxy enabled. |Temporarily disable Secure DNS/DoH and the browser proxy, and then retest the same domain name. |
|The exception persists after uninstalling a third\-party VPN |Drivers, filters, or services remain. |Check and fully remove residual network components. Restart the Endpoint and retest. |

The following uses macOS as an example to check the Endpoint environment. Before adjusting proxies or security software, record the original settings. After testing, restore configurations that do not need to change.

1. Check system DNS configuration.

   ```shell
   scutil --dns
   ```

   Check whether the resolver configuration contains `127.0.0.1`, and compare it with the actual query result from `nslookup`.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/vpn-domain-20261012/image-01.png)

2. Check port 53 and the occupying process.

   ```shell
   sudo lsof -i udp:53
   sudo ps -fp <PID>
   ```

   Replace `<PID>` with the process ID displayed by the previous command, and confirm whether it is `corplink-service`. If another program occupies the port, verify the conflict before handling it, and then reconnect to cloud VPN.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/vpn-domain-20261012/image-02.png)

3. Check the system proxy and third\-party VPN.

   In the proxy settings of the current network connection, check HTTP, HTTPS, SOCKS, and automatic proxy configurations.

   Temporarily disable related proxies, and then retest the same domain name. The settings entry may vary by system version.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/review-fixes-20261021/vpn-redacted.png)

On macOS, check proxy settings in the details of the current network. Check Private Relay in iCloud settings. Search for firewall and network filters in System Settings. Menu locations may vary across macOS versions. If the resolution paths or results used by `dig`, `traceroute`, `nslookup`, and `curl` are inconsistent, temporarily disable iCloud Private Relay. Then run query and access tests again for the same domain name, and compare results before and after disabling it. After testing, restore settings that do not need to change. For information about Private Relay, see [Apple's official description](https://www.apple.com/sg/privacy/docs/iCloud_Private_Relay_Overview_Dec2021.PDF).

4. Check network filters and firewalls.

   Check filtering rules and interception records in third\-party security software.

   If you need to disable a component for comparison, limit the test duration and restore it after testing. Do not determine a conflict only based on installation records.

   If the exception persists after uninstalling a third\-party VPN, check whether its drivers, services, or filters remain.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/vpn-domain-20261012/image-05.png)

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/vpn-domain-20261012/image-06.png)

### Check resolution timeouts

If the local DNS proxy works properly but queries still time out, capture packets to confirm requests and responses sent to central DNS. No response at all may be related to the request path, return path, or server status. Analyze this together with packets. When an Endpoint accesses central DNS through the physical NIC, it may also be affected by ISP or cross\-region network fluctuations.

Even if a central DNS query fails, it may return responses such as `NXDOMAIN` or `SERVFAIL`. Distinguish between "an error response is received" and "no response is received at all". In deployments that use Beijing public central DNS, the path for overseas Endpoints to directly reach this address may be affected by cross\-border links. Compare the result after forwarding through a domestic CPE.

If you have confirmed that the direct path from the Endpoint to central DNS is abnormal, and the enterprise has deployed an available CPE in China, use an employee routing policy to forward the related traffic through the CPE. Follow these steps to verify this first for affected users.

1. Add IP resources for central DNS.

   For deployments connected to China\-region tenants, the central DNS addresses are listed below. For tenants in other regions, use the central DNS addresses configured for the actual deployment instead. China\-region tenants mainly use two central DNS addresses: `180.184.33.35` for old tenants and `180.184.34.245` for new tenants. If you are not sure which central DNS the current tenant uses, add both IP addresses to IP resources.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/round2-20261021/ip-resource-en.png)

2. Add the IP resources to an employee routing policy, and specify the domestic CPE egress point.

   First limit the effective objects to affected users. Expand the scope only after confirming that the CPE can access central DNS.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/publish-audit-20261021/routing-scheduling.png)

3. Run domain resolution and cURL tests again.

   Use `traceroute` to observe path changes to the central DNS address. Use packet capture to confirm that traffic passes through the expected CPE.

   No response in path detection cannot independently prove failure. Use resolution and business access results for final verification.

### Check CPE resolution and logs

If the Endpoint has received a DNS response but the expected record is missing, check the domain spelling and the actual egress CPE. Then check the CPE upstream DNS and scheduling logs. Internal domain names require a DNS server that can resolve those domain names.

Perform the following operations on the actual egress CPE.

1. Run a health check.

   ```bash
   cd /opt/feilian/cpe/bin/
   ./feilian-cpe-health-check
   ```

   Check whether the following items in the output are successful. The `sdwan-rpc.feilian.cn:49920` endpoint below applies to deployments connected to China\-region tenants. For tenants in other regions, check the endpoint configured for the actual deployment.

   * Network test connection to central DNS gRPC `sdwan-rpc.feilian.cn:49920`.

   * Business application connection to central DNS gRPC `sdwan-rpc.feilian.cn:49920`.

   * Central DNS UDP port is reachable.

   * Primary and backup POPs, and primary and backup tunnels are in normal status.

2. Check DNS configuration and test resolution locally on the CPE.

   View the `nameserver` entries in `/etc/resolv.conf`.

   The following is a configuration example.

   ```bash
   root@node:~# cat /etc/resolv.conf
   # Dynamic resolv.conf(5) file for glibc resolver(3) generated by resolvconf(8)
   #     DO NOT EDIT THIS FILE BY HAND -- YOUR CHANGES WILL BE OVERWRITTEN
   nameserver 100.96.0.2
   nameserver 100.96.0.3
   options rotate
   nameserver 1.1.1.1
   ```

   Run `nslookup <affected-domain>` to verify whether the CPE can resolve the domain name locally. The following example shows output for a successful resolution.

   ```bash
   root@node:~# nslookup www.baidu.com
   Server:         100.96.0.2
   Address:        100.96.0.2#53
   
   Non-authoritative answer:
   www.baidu.com   canonical name = ps_other.a.shifen.com.
   Name:   ps_other.a.shifen.com
   Address: 61.135.162.87
   ```

   If the domain name cannot be resolved, configure a DNS server that can resolve the domain name for the CPE. Then run `nslookup <affected-domain>` again and confirm that the expected address is returned.

3. View event logs for the same time and domain name.

   In `cpe.event.log`, filter for the domain name and `dns_grpc` records, and compare requests and replies. Replace the domain name in the command with the affected domain name.

   ```bash
   tail -f /opt/feilian/cpe/log/cpe.event.log | grep '<affected-domain>'
   
   # Or filter the dns_grpc module and search for the specified domain name
   cat /opt/feilian/cpe/log/cpe.event.log | grep dns_grpc | grep -i www.baidu.com
   
   {"client_ip":"-","level":"INFO","module":"dns_grpc","msg":"<controller> dispatchRequest requestID: 73e7626e-b457-4bea-84da-c36c3bc8cc72, action: 1001, req: \rwww.baidu.com","path":"service/grpc/conn_receive.go:57","pid":"-","request_id":"-","time":"2026-09-28T11:10:15.032+08:00","uid":"-"}
   {"client_ip":"-","level":"INFO","module":"dns_grpc","msg":"<controller> dispatcher send reply msg: requestID:\"73e7626e-b457-4bea-84da-c36c3bc8cc72\"  action:1001  data:\"\\n\\x00\\x12\\rwww.baidu.com\\x1a\\x0e169.254.128.33\\\"\\x0e182.61.200.108\\\"\\x0e182.61.200.110\"","path":"service/grpc/conn_receive.go:160","pid":"-","request_id":"-","time":"2026-09-28T11:10:15.033+08:00","uid":"-"}
   ```

   |Log result |Description |Troubleshooting direction |
   |---|---|---|
   |No request for the corresponding domain name appears |The request may not reach this CPE, or may be scheduled to another egress point. |Check the central DNS link, resource matching, and actual egress CPE. |
   |Request appears but no result is returned |CPE\-side resolution or upstream DNS is abnormal. |Check `/etc/resolv.conf`, upstream DNS reachability, and resolution permissions. |
   |Both request and reply are normal |CPE DNS processing is generally normal. |Return to the Endpoint to check whether the response is returned and whether the subsequent access link succeeds. |

## TCP connection failure

If cURL has resolved the address, but the connection fails or times out after `Trying`, check the Access Policy, CPE forwarding, and target service port. Exit code `7` indicates a connection failure, but it does not necessarily mean active rejection. For exit code `28`, check logs to confirm the stage where the timeout occurs.

The following example shows output for a timeout during the connection stage.

```bash
user@macos ~ % curl -Ikv https://www.baidu.com
* Host www.baidu.com:443 was resolved.
* IPv6: (none)
* IPv4: 30.200.0.58, 30.200.0.59, 30.200.0.60, 30.200.0.61
*   Trying 30.200.0.58:443...
* connect to 30.200.0.58 port 443 from 192.168.13.245 port 57284 failed: Operation timed out
*   Trying 30.200.0.59:443...
* connect to 30.200.0.59 port 443 from 192.168.13.245 port 57361 failed: Operation timed out
*   Trying 30.200.0.60:443...
* connect to 30.200.0.60 port 443 from 192.168.13.245 port 57412 failed: Operation timed out
*   Trying 30.200.0.61:443...
* connect to 30.200.0.61 port 443 from 192.168.13.245 port 57468 failed: Operation timed out
* Failed to connect to www.baidu.com port 443 after 300011 ms: Couldn't connect to server
* Closing connection
curl: (28) Failed to connect to www.baidu.com port 443 after 300011 ms: Couldn't connect to server
```

Follow these steps to check the connection path.

Use the following steps to check access policies, CPE forwarding settings, and packets for this scenario.

1. Check access permissions for the target IP address.

   In the SealSuite Admin Console, go to **Zero Trust Access \> VPN \> Access Policy** to check the policies actually matched by the target user.

   A larger priority value is matched first. With the same priority, the most recently modified policy takes precedence.

   A high\-priority IP deny policy may override a domain allow policy.

   For more information, see [Manage VPN access permissions](https://docs.byteplus.com/en/docs/sealsuite/docs-managing-access-control-rules_2).

2. Detect the path, and compare the target access result on the egress CPE.

   On macOS, run the following path detection based on the target TCP port.

   ```bash
   root@macos ~ # sudo traceroute -P TCP -p 443 -w 1 www.baidu.com
   traceroute to www.baidu.com (30.200.0.85), 64 hops max, 40 byte packets
    1  * * *
    2  * * *
    3  * * *
    ...
   10  * * *
   ```

   If path detection shows `* * *` throughout, no probe response was received. Check the Access Policy for the target user and compare it with other domain names that the user can access normally. If the tunnel address of the egress CPE is visible, continue to check connectivity from the CPE to the target site. Use packet capture to confirm whether actual business packets pass through the CPE.

   On the actual egress CPE, run a cURL test for the same domain name and port, and compare it with the Endpoint result. If the CPE also cannot connect, continue to check the link and port from the CPE to the target service. If the CPE can connect but the Endpoint fails, continue to check the Access Policy and CPE forwarding path.

3. Check the CPE forwarding configuration.

   The following commands read configurations. Confirm exceptions by using routes and packets before adjusting configurations.

   |Command |Check item |
   |---|---|
   |`iptables -L FORWARD -n` |Check whether the default policy and rules of the FORWARD chain allow target traffic, and whether DROP is hit. If the default policy is DROP, continue to check whether valid allow rules exist. |
   |`sysctl net.ipv4.ip_forward` |Confirm that IPv4 forwarding is enabled. The value is `1`. |
   |`sysctl net.ipv4.conf.all.rp_filter` |Check reverse path verification. Strict mode `1` may affect asymmetric routing. Check it together with interface configuration and routes. Do not determine the fault only based on this value. `0` means disabled, and `2` means loose mode. |

4. Capture packets on the Endpoint and actual egress CPE at the same time, and reproduce the connection failure.

   After packet capture starts at both ends, run the cURL request again on the affected endpoint for the same domain name and port, and record the test time. After the request ends, stop packet capture and save the packet capture files from both ends. Compare the request time, target address, and port. Check whether `SYN` reaches the CPE and is sent to the target, and whether `SYN-ACK` returns to the CPE and Endpoint.

   If requests are sent from the CPE but no response packet returns, check the target service, firewall after the CPE, ACL, and return route. If the CPE has received response packets but the Endpoint has not, check the forwarding path from the CPE back to the Endpoint.

### Compare packets in four CPE directions

If the corresponding ICMP traffic is confirmed to be allowed, use Ping together with CPE packet capture to help check the forwarding path. This only verifies the tested ICMP traffic. It cannot replace HTTP/HTTPS domain policy verification. Larger packets can also help observe MTU and fragmentation\-related symptoms.

Collect packets by following these steps. First confirm that packets are sent from the Endpoint, and then compare each CPE interface. This avoids mistaking local send failures for tunnel faults.

1. Send test packets from the Endpoint.

   The following uses a `2000`\-byte payload as an example.

   Linux `-M do` and Windows `-f` prohibit fragmentation. If the payload exceeds the interface MTU, packets may fail to be sent locally. Reduce the payload and try again.

   The macOS example allows fragmentation by default. Results from the three commands cannot be directly equated.

   ```shell
   # macOS (automatically fragments by default)
   ping -s 2000 <target>
   
   # Linux (-M do prohibits fragmentation and can detect PMTU)
   ping -s 2000 -M do <target>
   
   # Windows
   ping -l 2000 -f <target>
   ```

2. Capture ICMP packets on the CPE at the same time.

   ```shell
   # Filter ICMP packets whose packet length is greater than 1000 bytes
   sudo tcpdump -i any 'icmp and len>1000' -eevvnn
   ```

   This filter ignores shorter packets. When reducing the test payload or checking fragmentation and ICMP error responses, adjust the filter conditions accordingly to avoid missing packets.

3. Compare the four observation points and save the results.

   ```shell
   sudo tcpdump -i any 'icmp and len>1000' -v -w /tmp/icmp.pcap
   ```

   After capturing enough packets for reproduction, press `Ctrl+C` to stop. The packet capture file is saved in `/tmp/icmp.pcap`.

The following figure uses `tun0_master` and `eth0` as examples to show the forwarding directions. The actual NIC names and source address translation behavior depend on the device configuration.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/round2-20261021/vpn-diagram-13-en.svg)

After confirming the interface, target address, packet capture filter conditions, and previous observation point, check according to the following table. Not seeing packets means further verification is needed. It cannot directly identify the packet loss cause.

|Direction and location |Packet source address → destination address |Meaning when packets are observed |Check direction when packets are not observed |
|---|---|---|---|
|① Forward ingress: CPE tunnel interface tun0_master |Endpoint virtual IP → real target IP |The test packet has reached the CPE tunnel ingress. |Confirm that the Endpoint has sent packets, the actual route passes through this CPE, and tunnel status and client policies are correct. |
|② Forward egress: CPE physical interface eth0 |Physical interface IP after SNAT → real target IP |The packet has been sent from the physical interface. If SNAT exists, check the translated source address. |If packets exist at the previous observation point, check the FORWARD chain, ip_forward, rp_filter, policy routes, and SNAT. |
|③ Reverse ingress: CPE physical interface eth0 |Real target IP → physical interface IP |The target reply has returned to the CPE physical interface. |Confirm that the request has been sent. Check the downstream link after the CPE, target service, firewall, ACL, and return route. |
|④ Reverse egress: CPE tunnel interface tun0_master |Real target IP → Endpoint virtual IP |The response packet has entered the tunnel path back to the Endpoint. Continue to check whether the Endpoint receives it. |If response packets exist on the physical interface, check reverse routes, connection tracking status, rp_filter, and other filtering rules. |

## TLS handshake failure

After cURL shows `Connected to`, if the request times out or reports an error after `Client hello`, check TLS negotiation and domain access permissions. A successful TCP connection does not guarantee that the handshake and subsequent transmission will succeed.

The following example shows output for a timeout after ClientHello is sent. This output alone cannot determine whether the failure is caused by an Access Policy.

```bash
root@macos ~ # curl -Iv --max-time 5 https://blocked.example.com:443
* Host blocked.example.com:443 was resolved.
* IPv4: 10.20.30.40
*   Trying 10.20.30.40:443...
* Connected to blocked.example.com (10.20.30.40) port 443    # TCP connection has been established
* ALPN: curl offers h2,http/1.1
* (304) (OUT), TLS handshake, Client hello (1):                 # ← No ServerHello after ClientHello is sent. Waiting times out
* Operation timed out after 5000 milliseconds with 0 bytes received
* Closing connection
curl: (28) Operation timed out
```

Common handshake symptoms and check directions are as follows.

|Output feature |Check direction |
|---|---|
|`Operation timed out` after ClientHello |Check domain access permissions. Check whether the server and devices in the path receive and reply to handshake packets. |
|`Connection reset by peer` |Use comparison tests and packet capture on the Endpoint and CPE to confirm where the connection is reset. Do not determine the source based only on RST. |
|`wrong version number` or `alert handshake failure` |Confirm that the port provides HTTPS service, and check the TLS version and cipher suites. Append `--tls-max 1.2` for compatibility comparison, but do not use downgrade as the default fix. |
|`curl: (35)` |View the complete TLS error and previous connection logs. If necessary, use packet capture to confirm the failure stage. |

Run the same cURL request for the same domain name and port on the egress CPE, and compare the handshake result with that on the Endpoint. If both sides fail, continue to check the target service and the common path. If only the Endpoint fails, check the path from the Endpoint to the CPE together with access permissions and packet captures at both ends. Check the resolved addresses, proxy settings, and TLS environment on both sides.

In the Admin Console, follow these steps to check permission configurations.

1. Go to **Zero Trust Access \> VPN \> Access Policy**, and use **Accessibility Detection**.

   Select the domain name type, enter the target user object and affected domain name, and run the check. Verify the matched policy. Access check only checks static configuration matching and does not generate real business traffic. After the check passes, still run cURL, DNS queries, or packet capture on the Endpoint to verify the actual access result.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/round2-20261021/vpn-detection-en.png)

2. Check the effective nodes and objects of the policy.

   If no effective node is specified, the policy usually applies to all related nodes. If nodes are specified, confirm that they include the cloud VPN node actually used.

   Check the target user, resource, action, and priority.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/round2-20261021/vpn-nodes-en.png)

3. After modification, access the same domain name again from the affected endpoint, and save the cURL result.

   HTTP domain identification is usually based on Host. HTTPS is usually based on SNI in TLS ClientHello.

   ICMP and TCP/UDP requests that do not carry domain information must use resource configurations based on the actual protocol. Do not use Ping results to replace domain permission verification.

## Certificate verification or HTTP response exception

This branch includes certificate verification failures and HTTP response exceptions. For certificate verification failures, check the certificate and local trust configuration. For HTTP response exceptions, an HTTP response has been received. Continue to evaluate the status code, request content, and response source. Select the corresponding section below based on the actual error.

### Certificate verification failure

Use `curl -Iv` without `-k` to retain the error. Run the same request on the egress CPE, and compare domain resolution, certificate, proxy, and local CA configurations. Different results on the two sides can only narrow the check scope. They cannot directly prove that certificate replacement has occurred.

The following examples show output for a certificate domain mismatch and an expired certificate. Check the domain name, validity period, and certificate chain in the error. Then check the server certificate configuration or the Endpoint trust store.

```bash
* Host wrong.example.com:443 was resolved.
* IPv4: 1.2.3.4
*   Trying 1.2.3.4:443...
* Connected to wrong.example.com (1.2.3.4) port 443
* (304) (OUT), TLS handshake, Client hello (1):
* (304) (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS handshake, Certificate (11):
* Server certificate:
*  subject: CN=www.other-site.com          # Certificate domain name is inconsistent with the accessed domain name
*  start date: ...
*  expire date: ...
*  issuer: ...
* SSL certificate problem: certificate subject name does not match wrong.example.com
* Closing connection
curl: (60) SSL certificate problem: certificate subject name does not match
```

```bash
* Host internal.example.com:443 was resolved.
* IPv4: 10.1.2.3
*   Trying 10.1.2.3:443...
* Connected to internal.example.com (10.1.2.3) port 443
* (304) (OUT), TLS handshake, Client hello (1):
* (304) (IN), TLS handshake, Server hello (2):
* TLSv1.2 (IN), TLS handshake, Certificate (11):
* Server certificate:
*  subject: CN=internal.example.com
*  start date: Jan  1 00:00:00 2020 GMT
*  expire date: Dec 31 23:59:59 2023 GMT  # Certificate has expired
*  issuer: CN=Internal CA                  # Self-signed or private CA
* SSL certificate problem: certificate has expired
* Closing connection
curl: (60) SSL certificate problem: certificate has expired
```

### HTTP response exception

If the request has received an HTTP response, but the status code or business result is abnormal, first check the request method, URL, authentication information, and response headers. Then find the corresponding request in the target application, proxy, or gateway logs. HEAD may differ from the actual browser request. Use the same request for comparison.

The following example shows an HTTP 502 response. This status code alone cannot prove that the fault occurs in the target application. It also cannot exclude connection issues between the proxy and the upstream.

```bash
* Host app.example.com:443 was resolved.
* IPv4: 30.100.0.9
*   Trying 30.100.0.9:443...
* Connected to app.example.com (30.100.0.9) port 443
* TLS handshake completed
* Server certificate:
*  subject: CN=app.example.com
*  SSL certificate verify ok.
> HEAD / HTTP/1.1                          # TLS has passed, and the request has been sent
> Host: app.example.com
> User-Agent: curl/8.7.1
>
< HTTP/1.1 502 Bad Gateway                  # Server returns an error status code
< Server: nginx
< Content-Type: text/html
<
* Connection #0 to host app.example.com left intact
```

Check the corresponding configuration based on the error message. HTTP 4xx/5xx may be returned by the target application, gateway, or proxy. First confirm the response source.

|Symptom |Check direction |
|---|---|
|Certificate domain mismatch |Check the accessed domain name, resolved address, server certificate, and SNI configuration. Check whether a proxy is used. |
|Expired certificate or self\-signed certificate |Check the certificate validity period, Endpoint time, trust chain, and local CA. An untrusted private CA does not mean the certificate has been replaced. |
|HTTP 4xx/5xx |Check the request method, path, authentication, and response headers. Find the corresponding request in application or gateway logs. If HEAD and GET results are inconsistent, retest the actual browser request. |

## cURL is normal, but web access is abnormal

If the cURL request for the primary domain name succeeds, but the browser still cannot open the page or the page is incomplete, continue to check failed resources and browser requests. Primary domain access does not mean the APIs, scripts, images, or CDNs that the page depends on are all accessible.

Compare in the affected browser and on the same Endpoint by following these steps.

1. Find failed resources and check domain routing.

   Open the **Network** panel in Developer Tools, refresh the page, and find requests that fail, stay Pending for a long time, or time out.

   Check whether these domain names belong to the expected resource scheduling scope.

2. Compare browser proxy and Secure DNS settings.

   Temporarily disable related proxy plugins or Secure DNS (DoH), and retest to observe whether the result changes.

   The request path may change as a result. However, do not determine the cause only because the setting is enabled. After testing, restore settings that do not need to change.

3. View the **Timing** of abnormal requests.

   The time consumed in each stage provides the following clues. Evaluate them together with the specific request and link metrics.

   * **Initial Connection / SSL**: Check TCP connection setup time and TLS handshake time.

   * **TTFB**: Affected by request transmission, network round trips, and server processing time.

   * **Content Download**: Check download time together with response size, bandwidth, packet loss, and server sending status.

4. Copy the abnormal request to the terminal for testing.

   In **Network**, right\-click the request and choose **Copy \> Copy as cURL**. When using PowerShell, choose the corresponding **Copy as PowerShell** format.

   Run it in the matching terminal. Compare results and time consumed under the same URL, method, and request headers.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/vpn-domain-20261012/image-18.png)

5. Check CPE network quality and bandwidth usage.

   In the Admin Console, view bandwidth, latency, and packet loss changes around the failure time. Confirm whether bandwidth saturation or link fluctuations exist.

   If you need further throughput tests, see [Troubleshooting case: Slow cloud VPN upload and download speeds (in Chinese)](https://help.feilian.cn/help-center/cloud-vpn-upload-and-download-speed-slow-troubleshooting-case).

If no obvious exceptions are found in link latency, packet loss rate, or CPE bandwidth usage, but the page still loads slowly, contact the application administrator. Continue to check site resource loading policies and server performance together with failed requests and timing results.

## Mobile access exception

If similar issues occur on mobile devices, first exclude client version and DNS path differences. Applications may dynamically access multiple domain names and IP addresses. Configuring only one primary domain name may not cover all requests.

Verify each item by following these steps. After each adjustment, reconnect and test the same service.

1. Update the SealSuite client.

   iOS and HarmonyOS users can check for updates in the corresponding app stores. Android app store versions may vary. Obtain the installation package through the [SealSuite client download guide](https://docs.byteplus.com/en/docs/sealsuite/downloding-the-sealsuite-client).

2. Compare DNS settings of the system and browser.

   Temporarily disable dedicated DNS, private DNS, or Secure DNS, and then test.

   These settings may use different encrypted DNS protocols and change the resolution path. They cannot all be called DoH.

3. If necessary, an Administrator expands the routing scope for small\-scale verification.

   If it is difficult to collect all application dependency domain names, evaluate using `0.0.0.0/1` and `128.0.0.0/1` to cover the IPv4 address space, and then configure the corresponding routing policy.

   This does not cover IPv6. Actual forwarding still requires checking policy matching results. Full\-tunnel traffic diversion expands the impact scope for CPE egress, bandwidth, and cross\-region links. If the CPE is located overseas, domestic services may also detour through overseas locations, increasing access latency. First verify access results and bandwidth usage with a small number of users. Then evaluate whether to expand the effective scope.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/publish-audit-20261021/routing-scheduling.png)

## Verify the troubleshooting result

After processing the corresponding branch, retest with the same affected domain name and port. Confirm the resolution, request, and actual page access results.

1. Verify domain resolution and business access again.

   Run `nslookup` and cURL tests, and then access the original business address in the browser. Confirm that the domain name can be accessed stably, the DNS resolved address meets expectations, and cURL and browser access results are consistent. If dependent resources on the page are abnormal, retest those resources at the same time.

2. Record adjustments and retest results.

   Retain the test time, adjusted configurations, and results before and after the adjustment. Specify whether the issue is resolved.

3. If the issue persists, organize troubleshooting information for further analysis.

   Summarize the checks performed in this troubleshooting process and their results according to the following checklist.

   * Faulty domain name, port, occurrence time, reproduction method, and affected user scope.

   * Endpoint operating system, SealSuite client version, connection node, and actual egress CPE.

   * DNS query result, complete cURL output, and browser failed request and error.

   * Related resource configurations, employee routing policy, and access permission matching result.

   * CPE health check result, event logs at the corresponding time, and packet capture files from the Endpoint and CPE.

## Appendix: cURL error codes

Common exit codes and subsequent check directions are listed below. Different cURL versions may use different error text. View the complete output at the same time.

|Error code |Meaning |Corresponding failure stage and troubleshooting direction |
|---|---|---|
|`curl: (0)` |Success |The command is executed successfully. You still need to check the HTTP status code and actual business result. |
|`curl: (5)` |Could not resolve proxy |Proxy address resolution failed. Check the Endpoint system proxy configuration, PAC script, or proxy server reachability. |
|`curl: (6)` |Couldn't resolve host |DNS resolution failed. Check the Endpoint DNS Proxy and central DNS link. |
|`curl: (7)` |Failed to connect |Connection setup failed. Possible causes include connection rejection, unreachable port, or proxy connection failure. Check with detailed logs. |
|`curl: (16)` |HTTP/2 error |HTTP/2 frame\-layer error. Try adding \-\-http1.1 for downgrade testing to exclude incompatibility between intermediate devices and HTTP/2. |
|`curl: (22)` |HTTP page not retrieved (\-\-fail) |When failure detection options such as \-\-fail are enabled, an HTTP error response may cause this exit code. Check the response source, request, and application logs. |
|`curl: (28)` |Connection timed out |Connection or data transfer timed out. Possible causes include unreachable target port, blocked link, or no response from the peer. |
|`curl: (35)` |SSL connect error |TLS handshake failed. Check whether the domain policy allows access, whether SNI is recognized, and whether intermediate devices interfere with the handshake. |
|`curl: (47)` |Too many redirects |The redirect limit is reached when following redirects. This is usually a redirect loop. Check the target site configuration. |
|`curl: (51)` |SSL certificate problem |Certificate or peer identity verification failed. Check domain matching, trust chain, validity period, and proxy configuration. |
|`curl: (52)` |Empty reply from server |TCP is connected, but the server returns no data. Possible causes include server exceptions or silent disconnection by an intermediate device. |
|`curl: (55)` |Failed sending network data |Sending data failed. Check connection interruption, the link, and intermediate devices together with logs. |
|`curl: (56)` |Failure receiving network data |Receiving response data failed. Possible causes include connection reset (RST), abnormal peer disconnection, or intermediate device intervention. |
|`curl: (58)` |Problem with the local certificate |Local client certificate issue. In mutual TLS scenarios, the client certificate is not properly configured or has expired. |
|`curl: (60)` |Peer certificate cannot be authenticated |The server certificate chain is not trusted. Check the local trust store and certificate chain, and compare with verification on the CPE side. |
|`curl: (77)` |Problem reading the SSL CA cert |Failed to read the local CA certificate store. Check the certificate file path, permissions, or whether the system CA package is corrupted. |
|`curl: (92)` |Stream error in HTTP/2 framing layer |HTTP/2 stream error. Try \-\-http1.1 downgrade testing to troubleshoot compatibility between intermediate proxies and HTTP/2. |
|`curl: (96)` |QUIC connection error |HTTP/3/QUIC connection failed. UDP is blocked or QUIC is not supported. Try forcing TCP/HTTP2. |
|`curl: (97)` |Proxy handshake error |Proxy handshake failed. The HTTP/SOCKS proxy configuration is incorrect, or the proxy itself is abnormal. |
|`curl: (98)` |Client certificate required |The server requires a client certificate for mutual TLS. Check whether the client certificate is correctly imported and selected. |

For the complete error code list (0–100+), see the official documentation: [curl man page — Exit Codes](https://curl.se/docs/manpage.html#EXITCODES).
