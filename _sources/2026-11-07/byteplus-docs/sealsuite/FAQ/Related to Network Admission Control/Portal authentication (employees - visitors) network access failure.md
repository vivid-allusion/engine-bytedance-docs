---
title: "Portal authentication (employees/visitors) network access failure"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/portal-certification-staff-visitor-networking-failure-troubleshooting-guide"
---

This guide provides Administrators with a systematic troubleshooting process. Use it to resolve issues where users, such as employees and visitors, cannot automatically open the authentication page after connecting to Portal Wi\-Fi, encounter errors while loading the login page, or still cannot access the Internet after identity verification, such as account login, SMS verification, or QR code scanning.

# Prerequisites

1. You have read the [Portal authentication](https://docs.byteplus.com/en/docs/sealsuite/selecting-network-access-authentication-methods) documentation and fully understand the use cases and process differences between the two PortalServer authentication methods.

2. Read [Network Access Control FAQ](https://docs.byteplus.com/en/docs/sealsuite/docs-wi-fi-managemant-faq) first to confirm whether a quick solution already exists for your issue. If the documents above do not resolve the issue, follow the troubleshooting steps in this article for in\-depth diagnosis.

# Troubleshooting process

The troubleshooting path for Portal authentication consists of the following four logical stages:

1.  **[Common] Page pop\-up stage**: Whether the Endpoint can successfully load the redirected Portal page, that is, whether the user can see the login page.

2.  **[Common] Identity submission stage**: Whether the backend can correctly identify the credentials when the user submits them, such as account and password, SMS code, or QR code.

3.  **[Branch] Data interaction stage**: Troubleshoot credential flow based on the authentication implementation, either **AC built\-in Portal Server** or **SealSuite Portal Server**.

4.  **[Common] Access decision stage**: Whether the RADIUS node finally delivers the allow instruction.

# Detailed troubleshooting steps

## Step 1: Troubleshoot network access and authentication page pop\-up exceptions

The Portal page can pop up only after basic IP communication is established between the Endpoint and the network device. Before adjusting authentication configurations, first confirm that the Endpoint has completed **pre\-connection**.

### 1. Check the access layer status

Before troubleshooting Portal, make sure the Endpoint has connected to the network and obtained a valid identity. This prevents misidentifying underlying network issues as authentication failures:

* **SSID association check**: If the Endpoint cannot connect or disconnects immediately after connection, the issue is a wireless link\-layer failure, such as signal interference, excessive AP load, or encryption mode mismatch. Troubleshoot the wireless configuration first.

* **IP address acquisition check**: The Endpoint must successfully obtain a valid IP address through DHCP. If the IP address is empty or is an automatically configured address, such as `169.254.x.x`, the network link is unreachable and the Portal authentication process cannot be triggered.

### 2. Check the redirection logic

Portal pop\-ups work as follows: the network device (AC) intercepts HTTP requests initiated by the Endpoint and forcibly redirects them to the authentication page URL.

* **Interception logic**:

   * If the target IP accessed by the Endpoint is in the **Portal allowlist (authentication bypass rules)** , the network device directly allows the traffic and does not trigger the pop\-up.

   * If the target IP accessed by the Endpoint is not in the allowlist, the network device intercepts the request and returns a redirection packet, triggering the browser to open the authentication page.

* **Manual trigger test**: If the page does not pop up automatically, enter an HTTP address that is not included in the Portal allowlist in the browser address bar, such as `http://www.baidu.com`, and check whether redirection occurs. If manual access opens the page but automatic pop\-up fails, the Endpoint detection mechanism (CNA) is blocked.

### 3. Verify the Portal allowlist configuration

Confirm that the Portal allowlist on the network device (AC) contains the following key addresses. Missing entries can interrupt the redirection process or cause page loading failures:

* **DNS server address**: This address must be allowed. Otherwise, the Endpoint cannot resolve the authentication page domain name or subsequent authentication information receiving address.

* **Portal authentication page address**: This is the SealSuite backend domain name or IP address. If it is not allowed, the AC intercepts the traffic for loading the login page again, causing the page to fail to open.

In the network device details, check the authentication page address for Staff Wi\-Fi and Guest Wi\-Fi. The following screenshots show the addresses that browsers use to load the login page. Confirm that these addresses are included in the Portal allowlist.

**Staff Wi\-Fi: authentication page address**

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/e494f049d4fad467.png)

**Guest Wi\-Fi: authentication page address**

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/80369681c169915a.png)

* **Authentication information receiving address**:

   * **Solution 1 (AC built\-in)** : Allow the AC's own Portal listening address, usually the AC interface IP address.

   * **Solution 2 (SealSuite hosted)** : Allow the Portal listening address of the corresponding SealSuite backend, that is, the IP address of the Radius node where Portal Server is enabled.

In the same device details, check the authentication information receiving address for Staff Wi\-Fi and Guest Wi\-Fi. The following screenshots show where authentication information is submitted. Use the Portal Server options above to determine which address to allow.

**Staff Wi\-Fi: authentication information receiving address**

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/75d7dd0f6ec36865.png)

**Guest Wi\-Fi: authentication information receiving address**

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/90ec4c3487ccd242.png)

### 4. Eliminate environmental interference factors

If the configurations above are correct but the pop\-up still does not appear, check for the following environmental interference:

* **Competing network connections**: Check whether the Endpoint has a wired network port enabled at the same time. If the wired network has a higher priority, traffic does not pass through Wi\-Fi, so wireless Portal authentication cannot be triggered.

* **Proxy and VPN**: Check whether the Endpoint has a global web proxy or VPN enabled. Encrypted and encapsulated traffic prevents the network device from identifying HTTP/HTTPS requests, so redirection cannot be triggered.

* **HTTPS and HSTS restrictions**: Some browsers force HTTPS access for specific domain names. Because some network devices can usually redirect only HTTP requests, use a plain HTTP address for the initial trigger test.

## Step 2: Troubleshoot authentication page display and account login

After the Endpoint successfully triggers redirection and opens the Portal page, focus on the page loading status and identity credential verification.

### 1. Troubleshoot page loading errors: Network device matching mechanism

If the page displays "Failed to obtain configuration. Refresh and try again" or the backend returns code `{"code":174003, "message":"无法匹配到当前AP"}`, the SealSuite backend cannot identify the network device that initiated the current authentication request.

* **Matching logic**: When the Endpoint opens the authentication page, the SealSuite backend parses the parameters carried in the URL and associates them with the "network device" configuration preset in the Admin Console. Only after matching succeeds can the system deliver the correct "authentication information receiving address".

* **Troubleshoot matching methods in different versions**:

   1. **SealSuite 3.1.5 and later (new mechanism)** :

      The system identifies the device by the unique numeric string (device ID) appended to the end of the URL.

      * **Troubleshooting point**: Check the redirection URL configured on the AC and confirm whether the SealSuite Admin Console\-generated device ID is fully included at the end.

   2. **Versions earlier than SealSuite 3.1.5 (old mechanism)** :

      The system compares the `apmac` parameter in the URL with the device MAC address configured in the backend.

      * **Troubleshooting point**: Check whether the URL contains the `apmac` parameter and whether its value exactly matches the MAC address entered in the [Network devices] list in the Admin Console.

* **Compatibility between old and new versions**:

   New versions (3.1.5+) remain compatible with the old `apmac` matching logic. If both ID and `apmac` exist in the URL, the system preferentially associates the request based on the device ID.

### 2. Troubleshoot account login verification

The account and password entered by the user on the Portal page must be verified by the identity source in the SealSuite backend.

* **Account consistency**:

   The account and password used for Portal authentication are exactly the same as the credentials used by employees to access the SealSuite Portal or log in to the SealSuite client.

* **Common error handling**:

   * **Error code 10110001**: The prompt indicates "Incorrect username or password".

      * **Troubleshooting action**: Focus on verifying the account status and whether the entered password is accurate.

   * **Cannot redirect after authentication succeeds**:

      * **Troubleshooting action**: Check whether the account has permission to access the network. If the account has no permission, the system cannot obtain network access credentials or perform subsequent redirection, even if the password is correct.

## Step 3: Verify the authentication information submission path

After the user enters the account and password on the Portal page and clicks "Log in", the browser redirects to an address that processes authentication requests, that is, the "authentication information receiving address". By identifying the ownership of this address, you can determine the current system mode and select the next troubleshooting branch.

### 1. Observe the redirection action and submission address

When clicking Log in, closely observe changes in the browser address bar, or use the browser developer tools (F12 \- Network tab) to check the target URL of the request.

* If the redirection address is in the form `http://[AC-IP]:8000/login` or `http://[AC-IP]/portal/logon.cgi`, your environment is using the AC built\-in Portal Server authentication solution, and the browser is trying to send the account and password directly to the AC. Go directly to [In-depth troubleshooting for AC built-in Portal authentication](https://docs.byteplus.com/en/docs/31/123485#5fe32b21), and focus on checking vendor\-specific field name formats and the RADIUS integration secret.

* If the redirection address is in the form `http://[SealSuite-node-IP]:9100/login`, your environment is using the SealSuite Portal Server authentication solution, and the browser is trying to send the account and password to the SealSuite server for processing. Go directly to [In-depth troubleshooting for SealSuite Portal Server authentication](https://docs.byteplus.com/en/docs/31/123485#a017fe72), and focus on checking whether port 9100 is listening, the `userip/nasip` parameters in the URL, and the Portal protocol handshake.

After an HTTPS certificate is loaded for SealSuite Portal Server, the authentication information receiving address must use `https://portal-server-ip:9100/login`. Confirm that the configured certificate path and content are correct. If the address uses a domain name, confirm that the domain name resolves to the corresponding RADIUS node IP address. The port depends on the actual configuration.

### 2. Test redirection connectivity

Regardless of the mode, if the page remains unresponsive for a long time after clicking Log in or displays "Connection timed out", perform the following checks:

* **Network probing**: On the Endpoint side or a test machine in the same network segment, use `telnet` or `tcping` to test whether the target port is reachable, such as AC port 80/8000 or SealSuite port 9100.

* **Path troubleshooting**: This indicates that firewall interception, ACL restrictions, or physical routing failures exist on the network path between the Endpoint and the receiving address. Restore network\-layer connectivity first. If the port is reachable but errors persist, follow the branching judgment above and proceed to Step 4 or Step 5 for deeper protocol troubleshooting.

When RADIUS uses the built\-in service of SealSuite Server, if the Portal service is listening but the Endpoint still cannot access it and packet capture shows continuous TCP SYN retransmissions, check whether the server inbound firewall rules block the Portal listening port, such as TCP 9100. After allowing the port according to the actual configuration, save the firewall rules to prevent them from becoming invalid after a server restart.

### 3. Handle browser security warnings

* **Symptom**: During redirection, the browser may display a warning such as "Connection is not secure" or "Your connection is not private".

* **Cause**: The current configuration uses the unencrypted HTTP protocol, or HTTPS with a self\-signed certificate.

* **Recommendation**: During troubleshooting, click "Advanced" on the web page and select "Continue". To eliminate this prompt at the root, load a compliant SSL certificate in the SealSuite backend or on the network device and enable HTTPS.

## Step 4: Troubleshoot branch paths

### In\-depth troubleshooting for AC built\-in Portal authentication

If you confirm in **Step 3** that the browser redirects to the AC's own IP address, such as port 8000, follow this path for in\-depth troubleshooting.

#### 1. Check the field name format

The AC built\-in service has strict fixed requirements for the field names (username/password) submitted in the form. Check the "authentication username field" and "authentication password field" in the SealSuite Admin Console network device configuration. They must exactly match the vendor requirements shown in the following table and are case\-sensitive.

|Vendor |Authentication information receiving address example |Username field name |Password field name |
|---|---|---|---|
|**Huawei** |`http://ac-ip:8000/login` |`username` |`password` |
|**H3C** |`http://ac-ip/portal/logon.cgi` |`PtUser` |`PtPwd` |
|**Aruba** |`https://securelogin.arubanetworks.com/cgi-bin/login` |`user` |`password` |
|**Cisco** |`http://192.0.2.1/login.html` |`username` |`password` |
|**ruckus** |`http://ac-ip:9997/login` |`username` |`password` |

#### 2. Check AC and RADIUS communication integration

After the AC successfully receives credentials, it initiates an authentication request to SealSuite as a RADIUS client. Failures at this point are usually reflected as rejections on the RADIUS side.

* **Shared secret check**: Check whether the RADIUS shared secret configured on the AC side is exactly the same as the shared secret configured for the network device in the SealSuite backend.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/e443d005355004c1.png)

* **RADIUS log analysis**: If you observe the following errors in `/var/log/feilian/radius.event.log` in the SealSuite backend, an integration issue exists:

   * **`client authentic failed`**: The RADIUS shared secret is incorrectly configured.

   * **`get client err`**: The AC device IP address was not correctly entered in the SealSuite backend.

### In\-depth troubleshooting for SealSuite Portal Server authentication

If you confirm in **Step 3** that the browser redirects to **port 9100** of the SealSuite node, follow this path for in\-depth troubleshooting.

#### 1. Verify the Portal module status and URL parameters

In this solution, the SealSuite Portal module acts as a forwarding intermediary and has strict URL parameter requirements.

* **Check whether port 9100 is listening**: Run `lsof -i:9100` in the RADIUS node backend to verify whether the Portal service is listening on port 9100.

   * The expected result is as follows:

      ```Bash
      # Execute command
      root@radius-node:~# lsof -i:9100
      
      # Expected output example
      COMMAND     PID   USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
      feilian-r  [PID]  root   25u  IPv6   1234567      0t0  TCP *:9100 (LISTEN)
      ```

   * If no result is returned, the Portal module is not started. Check in the Admin Console whether the Portal Server instance of this node is enabled.

* **Check required URL parameters**:

   1. **`userip`**: The AC must carry this parameter during redirection. If it is missing, the Portal module cannot locate the Endpoint IP address that initiated the request and returns the error `{"error":"portal http request do not contain arg userip"}`.

   2. **`nasip`**: If this parameter is not carried, SealSuite Portal Server uses the **wireless controller integration address** configured in the Admin Console as the target AC address by default. To extract another controller address from the Portal authentication URL, specify the parameter through **controller IP address field name**. The value of this parameter takes precedence over the default integration address. Check whether the actual target address is correct and confirm that UDP port 2000 is reachable.

   3. **Device ID /**  **`apmac`**: Used to identify device assets. As described in Step 2, this is the prerequisite for matching the backend configuration.

If `nasip` is not carried, the following prompt may appear in logs. It indicates that the service is using the default integration address. This prompt itself does not mean authentication failure. Check whether the target address in the logs is as expected.

```text
portal http request do not contain argument nasip using default bas address 192.168.1.1:2000
```

#### 2. Troubleshoot the protocol handshake between the Portal module and the AC (packet capture analysis)

After the Portal module receives credentials, it performs a "Portal protocol" handshake with the AC over UDP port 2000.

> **Note**

> If Wireshark cannot parse Portal packet details, use the [portal.lua plugin](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/portal-troubleshooting-20261009/portal.lua). Copy the file to the Wireshark plugin directory. For example, the directory for Wireshark 4.6 on Windows is `C:\Program Files\Wireshark\plugins\4.6`. The directory varies based on the installation location and version. Use the actual environment as the reference.

Run the following packet capture command on the SealSuite RADIUS node based on the authentication object, reproduce the issue, and save the packets. TCP 9100 corresponds to Endpoint authentication information submission. UDP 2000 corresponds to the Portal protocol. UDP 1812 and 3812 correspond to employee and visitor RADIUS authentication, respectively. If you have modified the ports, replace them with the actual values.

```bash
# Employee Portal authentication
sudo tcpdump -i any '((tcp port 9100) or (udp port 2000) or (udp port 1812))' -v -w 1.pcap

# Visitor Portal authentication
sudo tcpdump -i any '((tcp port 9100) or (udp port 2000) or (udp port 3812))' -v -w 2.pcap
```

* **Observe packet flow direction**:

   1. **`REQ_AUTH`** ** (authentication request)** : Portal module ➔ AC. If the AC does not receive it or does not respond, check whether Portal protocol listening is enabled on the AC.

      ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/7cbf0a076fc999fd.png)

   2. **RADIUS interaction coordination troubleshooting (** **`ACCESS-REQUEST`** ** / ** **`ACCEPT`** **)** :

      After receiving the preceding request, the AC immediately initiates verification to the RADIUS node.

      * **Normal case**: The AC sends `ACCESS-REQUEST`, and the RADIUS node returns `ACCESS-ACCEPT` after verification succeeds. The AC proceeds to the next step only after receiving this return.

      * **Exception cases**:

         * If only `REQ_AUTH` is observed and `ACCESS-REQUEST` is not observed, check whether the AC received and processed the Portal request, and whether it initiated authentication to the correct RADIUS address and port. Locate the cause based on the AC\-side configuration and packet capture result.

         * If RADIUS returns `ACCESS-REJECT`, the Portal result subsequently sent by the AC must be a failure. Go to [Step 5: Troubleshoot RADIUS authentication results and audit logs](https://docs.byteplus.com/en/docs/31/123485#2f03ba5d) to view the rejection reason in logs, such as incorrect password or insufficient permissions.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/4c0b4a27bfd2251f.png)

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/79ef9b01fa7db65d.png)

   3. **`ACK_AUTH`** ** (authentication response)** : AC ➔ Portal module. If the returned `ErrCode` is not 0, analyze it based on the AC error prompt:

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/335423345f1825fd.png)

   | Error code | Meaning | Troubleshooting direction |

   | \-\-\- | \-\-\- | \-\-\- |

   | **ErrCode=0** | **Authentication succeeded** | Authentication succeeded. If Internet access still fails, see [Authentication result report analysis](https://docs.byteplus.com/en/docs/31/123485#4e176c93) and check post\-authentication network access. |

   | **ErrCode=1** | **Authentication rejected** | The AC received the request but rejected it for some reason. Check the Portal security configuration on the AC side, or check whether the maximum number of connections is exceeded. |

   | **ErrCode=2** | **Link already established** | The user is already online. Check the user's online status on the AC. If you need to handle an existing session, follow the operation instructions from the corresponding vendor. |

   | **ErrCode=3** | **Authentication in progress** | The AC is processing concurrent requests from this Endpoint. Advise the user to wait for a moment and avoid clicking Log in repeatedly. |

   | **ErrCode=4** | **Error occurred** | An internal AC system error or protocol parsing exception occurred. Check whether the protocol version (Portal 1.0/2.0) between the AC and SealSuite matches. |

   4. **`AFF_ACK_AUTH`** ** (acknowledgment response)** : Portal module ➔ AC. This completes the final three\-way handshake confirmation.

   ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/114ad1f33977504a.png)

#### 3. Troubleshoot the communication link between the Portal module and the AC

If the module sends a request but does not receive a response packet from the AC for a long time:

* **Allow UDP port 2000**: Portal 1.0/2.0 uses UDP port 2000 for communication by default. Ensure bidirectional connectivity on this port between the SealSuite node and the AC.

* **AC protocol switch**: Some ACs require manual enabling of "external Portal server support" or "Portal protocol listening".

* **Locate the issue with packet capture**: Run `tcpdump -i any port 2000 -v` on the SealSuite RADIUS node for observation. If you only see `REQ_AUTH` being sent and no response packets, the packet is blocked on the transmission path or the AC does not respond.

## Step 5: Troubleshoot RADIUS authentication results and audit logs

When SealSuite Portal Server is used, after the AC receives the Portal authentication request, it initiates authentication to the RADIUS node and returns the authentication result to Portal Server. When the AC built\-in Portal Server is used, the AC receives the authentication information and initiates RADIUS authentication. Confirm the authentication result based on RADIUS packets and event logs.

### 1. Quickly identify log error messages

Log in to the RADIUS node and view `/var/log/feilian/radius.event.log`. Before looking for the specific authentication result, check whether the following common errors exist. These errors usually indicate that an exception has occurred during the RADIUS communication stage:

|Error type (Log Message) |Log explanation and action |
|---|---|
|**`get client err xxx`** |RADIUS did not obtain the AC device. Check whether the device IP configured in the backend is correct. |
|**`client authentic failed`** |**Shared secret error**. Check whether the RADIUS Secret configured on the AC and in the backend is consistent. |
|**`client message authentic failed`** |Message verification failed due to a **shared secret error**. |
|**`parse packet err`** |**Failed to parse packet**. The packet format is abnormal. |
|**`get config: json unmarshal failed`** |JSON parsing failed for the configuration returned during configuration retrieval. The system internal configuration is abnormal. |
|**`http error: xxxx`** |Failed to request the backend API. Check network communication between nodes. |
|**`receive tls error`** |**TLS handshake failed**. This is usually caused by certificate errors, such as Windows wildcard domain name or self\-signed certificate issues. |
|**`Eap check: not contain...`**  |The packet is not of the EAP type. If 802.1X authentication was selected by mistake, check the configuration. |
|**`MSCHAP Failure`** |The password entered for 802.1X authentication is incorrect. This appears only when 802.1X compatibility is enabled. |
|**`get user error: forbidden`** |**Access denied**. The user has no permission or has been disabled. |
|**`recv duplicate request`** |**Duplicate request received**. This is usually because RADIUS failed to return a packet within a short period. Check network latency. |
|**`chap user password wrong`** |**CHAP authentication password error**. |

### 2. Locate issues through authentication result reports (user conn report)

If the underlying communication logs above are normal, search for the keyword `user conn report` in the logs. This record reflects the final processing result at the business layer. Troubleshoot based on the value of `connResult`:

* **connResult = 1 (authentication succeeded)**

   The SealSuite authentication process has ended. If the Endpoint still cannot access the Internet at this point, troubleshoot in the following order:

   1. **IP address acquisition**: Confirm whether the Endpoint obtained the correct IP address and gateway for the corresponding VLAN through DHCP.

   2. **Troubleshoot DHCP\-delivered information**: If RADIUS delivers a dynamic VLAN, confirm that this VLAN has been created on the AC and upstream switch, and that the corresponding DHCP address pool works properly.

   3. **Check the AC allow status**: On the AC command line, check whether the user has entered the "online list". If the user is online but has no traffic, check whether the post\-authentication ACL policy associated on the AC blocks service traffic.

* **connResult = 2 (authentication failed)**

   The authentication process is interrupted due to a specific error, such as authentication user permissions or authentication timeout. Troubleshoot based on the specific error information in the logs.

* **connResult = 3 (authentication degraded)**

   Authentication did not fully succeed and a restrictive policy was triggered. Go to **Dynamic Control** \> **Control policies** in the SealSuite Admin Console, and check whether degradation was caused by hitting a control policy, such as an Endpoint compliance check where antivirus software is not enabled.

### 3. Decode visitor RADIUS packets

Visitor RADIUS authentication uses UDP 3812 by default. If Wireshark does not recognize packets on this port as RADIUS, manually specify the decoding protocol.

1. In Wireshark, find the packet on UDP port 3812, right\-click it, and select **Decode As…** .

2. In the pop\-up window, set the **Current** column corresponding to **UDP port 3812** to **RADIUS**, and click **OK**.

After configuration, you can view fields such as attributes, Code, and Identifier in RADIUS packets. If visitor authentication uses another port, set the decoding protocol for the actual port.

# Still unresolved?

If you have completed all troubleshooting steps above but the issue persists, prepare the following information and contact the SealSuite technical support team so that we can efficiently locate the issue.

Contact your SealSuite technical support representative and provide the information listed below.

## Information collection checklist

1. **Basic information**: Faulty account, fault time accurate to the minute, and affected scope, such as individual users or all users.

2. **Configuration verification screenshots**:

   * AC side: Portal configuration page and RADIUS solution configuration page.

   * SealSuite backend: Configuration details page of the network device.

3. **Core log files**:

   * `/var/log/feilian/radius.event.log` of the RADIUS node.

   * Packet capture file in `pcap` format when the fault occurred.

4. **Full\-screen error screenshot**: Complete error page containing the browser address bar and URL parameters.

# Root cause analysis and prevention recommendations

To avoid potential authentication failures, focus on the following preventive work during deployment and maintenance:

1. **Plan the deployment architecture properly**: Clarify the network locations and interaction paths among the AC, SealSuite backend, RADIUS node, and Endpoint.

2. **Pre\-allow Access Policies**: Pre\-allow all required IP addresses and ports in firewalls or ACLs, such as DNS 53, RADIUS 1812/1813, Portal 2000/9100, and HTTP/HTTPS.

3. **Use analysis tools proficiently**: Understand the authentication mechanism and use Wireshark proficiently for packet\-level analysis. Focus on round trips of key packets such as `REQ_AUTH` and `ACCESS-REQUEST`.
