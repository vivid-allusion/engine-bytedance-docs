---
title: "Quick troubleshooting for macOS 802.1X network access"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/macos-8021x-network-access-quick-troubleshooting"
---

When a macOS device cannot access an enterprise Wi\-Fi network through 802.1X authentication, the administrator can use this document to check network access logs, authentication packets, and system logs. These checks help narrow down the issue step by step. This document also applies when authentication succeeds but network access still fails, or when the client reports a connection error.

## Troubleshooting workflow

First check the Admin Console and RADIUS logs. Then select a troubleshooting method based on whether the issue can be reproduced. If the issue is reproducible, capture packets as described in Step 3. If the issue occurs intermittently and packets cannot be captured in real time, analyze logs as described in Step 4 and Step 5. Use the following troubleshooting sequence.

1. Check employee network access logs to verify employee permissions and Dynamic Control results.

2. Check RADIUS authentication logs to determine whether authentication requests reached the server and how they were processed.

3. Capture client packets to identify where a reproducible issue stalls during authentication.

4. Analyze SealSuite client logs to trace intermittent issues through the connection process and status codes.

5. Analyze macOS system logs to further check how system authentication components process the request.

## Step 1: Check employee network access logs

First view the network access records of the affected employee. Confirm whether network access permissions or Dynamic Control affected authentication. Follow these steps. If no record is found, continue checking RADIUS node logs.

1. Log in to the SealSuite Admin Console and go to **Audit Logs \> Staff Network Log**. Search for the affected employee.

2. Check the employee's network access permissions and Dynamic Control result. Focus on the following items.

   * Confirm whether network access permissions are correctly assigned to the employee.

   * Confirm whether the employee triggered a Dynamic Control rule that denies network access.

      ![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/2bcbe76fbf23767a.png)

If no network access failure record is found for the employee, continue with Step 2. Search the RADIUS detailed authentication logs by username.

## Step 2: Check RADIUS authentication logs

RADIUS node logs indicate whether authentication requests reached the server, and show the specific result of each authentication success, failure, or downgrade. Follow these steps.

1. Log in to the RADIUS node connected to the AC. Use the username as a keyword to filter the `/opt/feilian/radius/log/radius.event.log` log.

2. Confirm whether authentication records exist for the user. If no record exists, select a troubleshooting direction based on the impact scope.

   * Only one user has no authentication logs, while other users authenticate normally: Check the user's client and network path. Confirm whether authentication packets reach the RADIUS node.

   * No users have authentication logs: Check the integration configuration between the AC (wireless controller) and RADIUS, and check the intermediate network path. Confirm whether RADIUS receives authentication requests.

3. If authentication records exist, check the `connResult` field and follow the corresponding status check below.

   The following example shows RADIUS authentication logs for a single user. The logs include the authentication result, issued permissions, and VLAN information.

   ```text
   INFO  2025/06/25 21:08:38.614049 engine.go:68: conn [::]:1812 192.0.2.10:37351
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:38.614123 eap.go:163: [EapMethodSelect] Calling sub-mod EAP_PEAP to process, stage INITIATE
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:38.948459 peap.go:259: [PeapProcess ] handshakeEnd: true
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:38.983047 eap.go:169: [EapMethodSelect] Calling sub-mod EAP_MSCHAPV2 to process, stage INITIATE
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:38.983084 eap_mschapv2.go:71: [MS-CHAPv2]  Session Init
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:39.015018 eap_mschapv2.go:196: [MS-CHAPv2]  getting user info with username user@example.com
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:39.015047 rest.go:253: get user info: user@example.com employee
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:39.039932 rest.go:223: user attributes: user@example.com group:{"tunnel_private_group_id":"100"} tunnel-private-group-id map[string]interface {}{"Service-Type":"Framed-User", "Tunnel-Medium-Type":"IEEE-802", "Tunnel-Private-Group-ID":"100", "Tunnel-Type":"VLAN"}
    Downgrade:false
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:39.040045 eap_mschapv2.go:345: [MS-CHAPv2] MSCHAP Success map[Service-Type:Framed-User Tunnel-Medium-Type:IEEE-802 Tunnel-Private-Group-ID:100 Tunnel-Type:VLAN]
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:39.103106 rest.go:317: user approved: user@example.com {"tunnel_private_group_id":"100"} tunnel-private-group-id employee Framed-User 02:00:00:00:00:01 02-00-00-00-00-02:feilian-radius-employee-dot1x false authAccountType: FEILIAN
   INFO session-cd0e6dc92da65912 2025/06/25 21:08:39.108817 rest.go:526: user conn report, session-id = cd0e6dc92da65912 username = user@example.com, groupID = {"tunnel_private_group_id":"100"}, serverName = employee, serviceType = Framed-User, authType = FEILIAN, callingStationID = 02:00:00:00:00:01, calledStationID = 02-00-00-00-00-02:feilian-radius-employee-dot1x, connResult = 1, authDuration = 488 ms, remark = 
   ```

### connResult = 1: Authentication succeeded

If the endpoint still cannot access the network after successful authentication, continue checking the network side. The permission information in the logs has the following meanings.

* `groupID`: The permission issued after successful authentication. If this field is empty, the default permission is used. Authentication is performed only, and no permission information is issued.

* `tunnel_private_group_id`: The issued VLAN ID.

### connResult = 2: Authentication failed

The authentication process may be interrupted due to insufficient user permissions, authentication timeout, or EAP protocol negotiation failure. Check the specific error information in the logs and continue troubleshooting. For common errors and handling methods, see [Interpret RADIUS authentication logs (in Chinese)](https://help.feilian.cn/help-center/employee-8021x-wireless-authentication-networking-failure-troubleshooting-guide#4bda8a0d).

### connResult = 3: Authentication downgraded

RADIUS applied restricted network access based on a Dynamic Control policy, such as issuing another VLAN ID. Authentication has succeeded in this case, but permissions are restricted. Check the dynamic access control policies in the SealSuite Admin Console. Confirm whether a restrictive policy was triggered, such as by a failed endpoint compliance check.

## Step 3: Capture client packets

If the issue can be reproduced, use Wireshark on the affected device to record the network access process. Follow these steps to capture packets. Then compare the packets with the packet interaction flow and troubleshooting table to identify the authentication stage where the process stalls.

1. Install and open Wireshark on the affected macOS device. Select the network interface card used to connect to the enterprise Wi\-Fi network, and start packet capture.

2. Repeat the previously failed Wi\-Fi network access operation. Stop packet capture after the issue occurs.

3. Use the `eapol` filter to view authentication packets. Check which step the interaction stalls at.

The SealSuite client only writes 802.1X authentication credentials to macOS. After the credentials are written, SSID association, EAPOL, PEAP/TLS, EAP\-MSCHAPv2, EAP\-Success reception, and DHCP, ARP, DNS, and service access after successful authentication are all handled by native macOS networking and authentication components.

The following figure shows the packet interaction flow for 802.1X authentication. Compare it with the packet capture results step by step.

![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/feilian/borders-20261021/97277c9a7561d0cf.png)

Based on the packet capture symptoms, use the following table to select the next check. The causes in the table are provided for troubleshooting reference. Verify them against actual logs and network configuration.

|**Packet capture symptom** |**Filter/characteristic** |**Possible cause and next step** |
|---|---|---|
|**No EAPOL frames are sent**. |No packets appear under the `eapol` filter. |Possible causes include an SSID without 802.1X authentication, a failure to write the authentication configuration, or a wireless driver or interface issue. First check whether the 802.1X configuration for the SSID exists in macOS "Network Settings". |
|**EAPOL\-Start is sent, but no AP response is received**. |Only EAPOL\-Start (0x888E) from the client → broadcast is observed. No AP response is observed. |802.1X is not enabled on the port by the AP/AC, or the CAPWAP tunnel between the AP and AC is not established. Contact the network team to confirm the authentication configuration and port status of the SSID. |
|**After the client sends Identity Response, no subsequent EAP\-Request is received**. |The flow stalls after the client sends Identity Response. |The AC did not forward the request to RADIUS, or RADIUS did not respond. Also capture `radius` packets on the RADIUS node to confirm whether Access\-Request is received. |
|**EAP Failure is received after the TLS handshake completes**. |TLS ServerHello/Certificate/Finished is normal, but EAP Code=4 (Failure) is then received. |In a PEAP\-MSCHAPv2 scenario, check the logs to determine whether inner authentication failed. Possible causes include incorrect credentials, unauthorized account, and RADIUS backend query failure. Use the connResult value and error details in RADIUS logs to locate the issue. |
|**RADIUS authentication succeeds, but the Endpoint still reports failure**. |EAP Success is returned normally (connResult=1), but the client\-side network is still unavailable. |Check whether the Tunnel\-Private\-Group\-ID (VLAN ID) issued by RADIUS exists and is configured on the AC. If the VLAN has not been created locally, the AC cannot place the controlled port into it after receiving the dynamic VLAN instruction. As a result, the port is actually in an isolated or drop state. Confirm on the AC whether the VLAN ID issued by RADIUS, such as 100 or 200, is globally created and associated with the corresponding service. Also check whether the Tunnel\-Type/Tunnel\-Medium\-Type attributes returned by RADIUS match the AC configuration. |

## Step 4: Analyze SealSuite client logs

If the issue occurs intermittently and packets cannot be captured in real time, use client logs to trace credential writing, connection triggering, and connection results. Follow these steps to check operation records and connection status codes. If the cause is still unclear, continue with Step 5.

1. Open the client log `/usr/local/corplink/logs/corplink.log` and view the records that correspond to the network access operation.

   The following example shows, in sequence, the process of clicking one\-click authentication, deleting the old configuration, creating a new configuration, triggering the connection, and recording the connection result.

   ```text
   # Manually click one-click authentication
   CorpLink 2026/07/08 10:26:36.285565 token.go:97: client(127.0.0.1:50042) method(/server.CorpLink/ConnectWiFi)
   
   # Delete old Wi-Fi network access templates and authentication credentials
   CorpLink 2026/07/08 10:26:36.292887 wifi_darwin.go:337: eapolcfg: [removeProfile --SSID XXX]  <nil>
   
   CorpLink 2026/07/08 10:26:36.312754 wifi_darwin.go:343: Remove security wlan user.item ...
   
   # Create new Wi-Fi network access templates and authentication credentials
   CorpLink 2026/07/08 10:26:36.353074 wifi_darwin.go:315: eapolcfg: [createProfile --SSID XXX --authType PEAP --securityType WPA2 --trustedCertificate /usr/local/corplink/selfsign.0.cer --trustedCertificate /usr/local/corplink/selfsign.1.cer] 3B4E5CA7-E43B-4AB9-8277-CADCE2013C6C <nil>
   
   CorpLink 2026/07/08 10:26:36.378730 wifi_darwin.go:198: wifi save: [save peap XXX username password] 0 <nil>
   
   # Trigger connection
   CorpLink 2026/07/08 10:26:40.014244 wifi_darwin.go:208: wifi connect: [/Applications/CorpLink.app/Contents/MacOS/wifihelper connect peap XXX username password] 0 <nil>
   
   # Connection result display
   CorpLink 2026/07/08 10:26:40.014358 availability.go:89: track event: {"event_time":1783477596,"event_name":"wifi_connection_status","dimension":{"ssid":"Learnings","status":"0"},"metric":{"duration":3728},"need_aggregation":false}
   ```

2. Run the following command in the macOS terminal to obtain the latest network access connection status in the logs.

   The following command queries the last connection status record. Check whether the output time corresponds to this failure. This avoids using the result of another connection attempt as the basis for diagnosis.

   ```bash
   grep 'wifi_connection_status' /usr/local/corplink/logs/corplink.log | tail -n 1
   ```

   The following example shows the command output. In the example, `status` is `2` (`WIFI_OUT_SCOPE`), indicating that the SSID is outside the device connection range, such as outside signal coverage or not configured on the device.

   ```text
   CorpLink 2026/09/19 21:22:50.282902 availability.go:91: track event: {"event_time":1789824168,"event_name":"wifi_connection_status","dimension":{"caller":"corplink_fe","sn":"XXXXXX","ssid":"XXXXXXX","status":"2"},"metric":{"duration":1609},"need_aggregation":false}
   ```

3. Check the `status` value in the output and compare it with the following status codes to determine the connection result.

   The following defines the `wifi_connection_status.status` status codes reported by the SealSuite client.

   ```text
           WIFI_SUCCESS           = 0  //Operation succeeded
           WIFI_FAILED            = 1  //Operation failed
           WIFI_OUT_SCOPE         = 2  //Out of range
           WIFI_ALREADY_CONNECTED = 3  //Already connected to this SSID
           WIFI_CONFIG_ERROR      = 4  //Configuration error
           WIFI_CANT_CONNECT      = 5  //Cannot connect
           WIFI_SYS_NOT_SUPPORT   = 6  //Unsupported system
           WIFI_NEED_PERMISSION   = 8  //Location permission required
           WIFI_NO_INTERFACE      = 9  //No wireless network adapter
           WIFI_POWER_ON_FAILED   = 10 //Failed to power on Wi-Fi
   ```

   If the status code is `5` (`WIFI_CANT_CONNECT`), the connection failed. Continue with Step 5. Check macOS system authentication logs to troubleshoot system\-side or network\-side causes.

## Step 5: Analyze macOS system logs

If the client status code does not sufficiently explain the failure, collect and analyze macOS authentication logs by following these steps. The query time range must cover the failure time. For more complete information, collect system diagnostic logs when the failure occurs.

1. Open the macOS terminal and run the following command to export authentication logs from the last 30 minutes.

   ```bash
   log show --style syslog --last 30m --predicate '(processImagePath contains "eapolclient" AND subsystem contains "com.apple.eapol") OR (processImagePath contains "SecurityAgent" AND subsystem contains "com.apple.SecurityAgent")' > ~/Desktop/eapolclient.log
   ```

   This command filters macOS Unified Logging records from the last 30 minutes that are related to 802.1X/EAPOL authentication and SecurityAgent. It saves the records to the `eapolclient.log` file on the desktop.

   The following table describes the parameters and filter conditions in the command. Adjust the query range based on the failure time.

   |Parameter |Description |
   |---|---|
   |`log show` |Queries saved historical logs in macOS Unified Logging. |
   |`--style syslog` |Displays logs in the traditional syslog style, which is suitable for manual review and saving. |
   |`--last 30m` |Queries only the last 30 minutes. You can adjust this parameter, such as to the last 1 hour. |
   |`--predicate '...'` |Sets log filter conditions. |
   |`processImagePath contains "eapolclient"` |Filters logs generated by eapolclient\-related processes. |
   |`subsystem contains "com.apple.eapol"` |Further restricts results to the Apple EAPOL/802.1X subsystem. |
   |`OR` |Matches either set of conditions. |
   |`processImagePath contains "SecurityAgent"` |Filters SecurityAgent\-related logs. |
   |`subsystem contains "com.apple.SecurityAgent"` |Restricts results to the SecurityAgent subsystem. |
   |`>` |Redirects command output to a file instead of displaying it in the terminal. |
   |`~/Desktop/eapolclient.log` |Outputs to eapolclient.log on the current user's desktop. |

2. To collect complete macOS system diagnostic logs, run `sudo sysdiagnose` in the terminal when the failure occurs.

3. Analyze the system authentication process together with the collected `eapolclient.log`. Automated analysis tools can also assist troubleshooting. If the cause remains unclear, contact Apple Support with the complete log package for further analysis.

## Reference documents

For more information about the protocols and macOS 802.1X configuration covered in this document, see the following standards and official documentation.

**IEEE 802.1X\-2020** — Port\-based network access control standard. It defines the Uncontrolled/Controlled Port, EAPOL frame format, and authentication state machine. [View the official page](https://1.ieee802.org/security/802-1x/)

**RFC 3748 (EAP)**  — Extensible Authentication Protocol framework. It defines EAP request, response, success, and failure message formats, and specifies that the Peer must wait for EAP\-Success. [View the RFC](https://www.rfc-editor.org/rfc/rfc3748.html)

**RFC 2865 (RADIUS)**  — Remote Authentication Dial\-In User Service. It defines the Access\-Request/Challenge/Accept/Reject packet structures and attribute encoding. [View the RFC](https://www.rfc-editor.org/rfc/rfc2865.html)

**RFC 2868 (RADIUS VLAN)**  — Defines Tunnel\-Type / Tunnel\-Medium\-Type / Tunnel\-Private\-Group\-ID, which are attributes for dynamic VLAN assignment. [View the RFC](https://www.rfc-editor.org/rfc/rfc2868.html)

**Apple official deployment guide** — Connect Apple devices to 802.1X networks: PEAP/EAP\-TLS configuration profiles, credential management, and trusted certificates. [View Apple documentation](https://support.apple.com/zh-cn/guide/deployment/depabc994b84/web)
