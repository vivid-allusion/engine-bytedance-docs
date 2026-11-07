---
title: "Use packet capture tools to troubleshoot Network Access Control (NAC) issues"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/troubleshoot-network-access-with-packet-capture"
---

When employees or visitors cannot access the enterprise network, an administrator can use packet capture tools to view authentication requests, responses, and returned results. This helps identify where authentication fails. This article describes how to choose common tools, capture packets, and view results. It applies to scenarios such as SealSuite 802.1X and Portal Network Access Control (NAC).

## Choose a packet capture tool

Choose a tool based on the authentication stage and device system you need to observe. To view authentication interactions between an endpoint and network devices, capture packets on the affected endpoint. To view interactions between network devices and the authentication service, capture packets on the corresponding RADIUS node. After choosing a tool, complete the procedure in the corresponding section below.

|Tool |Applicable system |Purpose |
|---|---|---|
|Wireshark |Windows, macOS, Linux |Captures, filters, and analyzes packets through a graphical interface. It can also open saved packet capture files. |
|Microsoft Network Monitor |Windows |Captures 802.1X EAP authentication packets from Windows wireless adapters. |
|tcpdump |Unix, Linux, macOS |Captures packets from the command line. It is suitable for servers such as RADIUS nodes. After packets are saved as `.pcap`, they can be analyzed in Wireshark. |

Network Access Control (NAC) involves protocols such as EAPOL, VLAN, RADIUS, Portal, DHCP, DNS, and HTTP/HTTPS. During troubleshooting, you may also need to view ARP, ICMP, TCP, TLS, and UDP packets.

## Use Wireshark

Wireshark is an open\-source graphical network protocol analyzer. It parses multiple protocols and displays packet encapsulation structures. It is compatible with `.pcap` and `.pcapng` files. On Windows, it depends on Npcap. On Linux and macOS, it depends on libpcap.

### Install the tool

Visit the [Wireshark download page](https://www.wireshark.org/download.html), download the installer based on your operating system and processor type, and complete the installation wizard. If the tool is already installed, go directly to the packet capture step.

You can also download the Wireshark 4.6.4 offline installer by processor type: [Windows x64](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/network-capture-20261009/Wireshark-4.6.4-x64.exe) or [Windows ARM64](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/network-capture-20261009/Wireshark-4.6.4-arm64.exe).

### Capture packets

Open Wireshark and select the network adapter used for this network access attempt on the start page. For example, when troubleshooting wireless network access issues, select the wireless adapter connected to the target Wi\-Fi network. To observe multiple network adapters at the same time, select them as follows. After selecting the adapters, start packet capture. Then repeat the network connection attempt on the affected endpoint and wait for the issue to recur.

* Windows/Linux: Press and hold **Ctrl**, then click multiple network adapters.

* macOS: Press and hold **Cmd**, then click multiple network adapters.

* Select a contiguous range: Press and hold **Shift**, then click the first and last network adapters.

### Filter and view packets

After capturing packets, enter filter conditions in **Display Filter** to filter traffic related to the issue from the packet list. For example, enter `eapol` to view 802.1X authentication packets. You can also use the following IP and port conditions to narrow the scope. When the input is correct, the input box turns green. Press Enter or click **Apply** to apply the filter. If the input box turns red, correct the syntax first. After selecting a target packet, view its source address, destination address, protocol, and packet details.

```text
# Protocol filters
tcp          # Show only TCP
udp          # Show only UDP
http         # Show only HTTP
icmp         # Show only ICMP (ping)
arp          # Show only ARP
dns          # Show only DNS

# IP address filters
ip.src == 192.168.1.100       # Source IP
ip.dst == 192.168.1.1         # Destination IP
ip.addr == 192.168.1.100      # Source or destination IP
ip.addr == 192.168.1.0/24     # Subnet filter

# Port filters
tcp.port == 80                # TCP port 80 (source/destination)
tcp.srcport == 443            # TCP source port 443
tcp.dstport == 22             # TCP destination port 22
udp.port == 53                # UDP 53 (DNS)

# HTTP/HTTPS filters
http.request.method == "GET"  # GET requests only
http.request.method == "POST" # POST requests only
http.host == "www.example.com" # Specify Host
http.uri contains "login"      # URI contains login
tls                             # TLS/HTTPS traffic
tls.handshake.extensions_server_name == "cn.bing.com" # Specify server_name

# Composite filter
# Source 192.168.1.100 accesses ports 80/443
ip.src == 192.168.1.100 and (tcp.port == 80 or tcp.port == 443)
```

### Save packet capture files

After the issue recurs, stop packet capture and save the captured packets as a `.pcap` or `.pcapng` file. Record the time when the issue occurred, so that you can later locate the corresponding network access operation in the packets. For further analysis, open the saved file in Wireshark and use the filtering methods described above.

To learn more about packet analysis, read [The Art of Wireshark Network Analysis (in Chinese)](https://github.com/anzhihe/Free-Web-Books/blob/master/book/Wireshark%E7%BD%91%E7%BB%9C%E5%88%86%E6%9E%90%E7%9A%84%E8%89%BA%E6%9C%AF.pdf) or [download the PDF](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/network-capture-20261009/Wireshark%E7%BD%91%E7%BB%9C%E5%88%86%E6%9E%90%E7%9A%84%E8%89%BA%E6%9C%AF.pdf).

## Use Microsoft Network Monitor

Microsoft Network Monitor is a graphical packet capture tool for Windows. It parses Windows network events and protocols. In Windows wireless adapter 802.1X authentication scenarios, it can capture EAP packets.

### Install the tool

Visit the [Microsoft Network Monitor 3.4 download page](https://www.microsoft.com/en-us/download/details.aspx?id=4865), download the installer based on your processor type, and complete the installation. If the tool is already installed, go directly to the packet capture step.

You can also download the Network Monitor 3.4 offline installer by processor type: [Windows x64](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/network-capture-20261009/NM34_x64.exe) or [Windows x86](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/feilian/network-capture-20261009/NM34_x86.exe).

### Capture packets

Open Microsoft Network Monitor as an administrator. In **Select Networks**, select the network adapter used for this network access attempt. When troubleshooting wireless 802.1X authentication issues, select the wireless adapter connected to the target Wi\-Fi network. If network adapter information is not displayed, check whether the tool is running as an administrator.

Click **New Capture** to create a packet capture, then click **Start** to start packet capture.

After packet capture starts, repeat the network connection attempt on the affected endpoint. For example, connect to the employee Wi\-Fi network and wait for the issue to recur. To temporarily pause packet capture, click **Pause**. After the issue is reproduced, click **Stop** to stop packet capture, then view and save the captured packets.

### Filter and view packets

After stopping packet capture, enter filter conditions in **Display Filter** to filter packets related to this authentication attempt. To view 802.1X EAP packets from a wireless adapter, enter `eapol` and apply the filter. Select the target packet in the packet list, view its protocol and detailed fields, and then use the authentication result descriptions at the end of this article to determine the observed interaction.

### Save packet capture files

Click **Save As**, select a file location, enter a file name, and save the packet capture result. Also record the time when the issue occurred, so that you can match the packet capture file to the same authentication attempt in RADIUS logs.

## Use tcpdump

tcpdump is an open\-source command\-line packet capture tool based on libpcap. It supports BPF filter syntax. It can display packets in real time or save them as `.pcap` files for analysis in Wireshark.

### Install and verify the tool

Open a terminal on the server where you need to capture packets, and run the installation command for your Linux distribution. After installation, run `tcpdump --version`. If version information is displayed correctly, continue to run packet capture commands. If tcpdump is already installed, check the version directly. You do not need to install it again.

```text
# Debian/Ubuntu series
sudo apt update && sudo apt install tcpdump -y

# RHEL/CentOS/Fedora series
sudo dnf install tcpdump -y
# CentOS 7 uses yum install tcpdump -y

# Verify installation
tcpdump --version
```

### Capture packets

Run commands on the RADIUS node where packet capture is required. First use `-D` to view available network adapters. Then use `-i` to specify the packet capture adapter, and set filter rules based on the target AC address, protocol, and port. The following commands run with `sudo`. Make sure you have the required packet capture permissions.

```text
sudo tcpdump [options] [filter expression]
```

|Option |Description |
|---|---|
|\-D |Lists all available packet capture network adapters on the local host (outputs sequence numbers and names) |
|\-i |Specifies the capture network adapter (such as \-i eth0, \-i any for all adapters, or \-i lo for the loopback interface) |
|\-c |Specifies the number of packets to capture (such as \-c 100, which stops automatically after capturing 100 packets) |
|\-n |Does not resolve IP hostnames and directly displays numeric IP addresses (improves capture speed) |
|\-nn |Does not resolve hostnames, port names, or protocol names at all (numeric output only, most commonly used) |
|\-v/\-vv/\-vvv |Displays detailed packet information (more v characters provide more details) |
|\-w |Writes captured data to a file (such as `-w capture.pcap`) |
|\-r |Reads a saved `.pcap` file (such as `-r capture.pcap`) |
|\-A |Displays packet content in ASCII format (useful for viewing plaintext such as HTTP) |
|\-X |Displays content in both hexadecimal and ASCII formats |
|\-e |Displays data link layer header information, such as source/destination MAC addresses and Ethernet type. |

The following examples cover RADIUS authentication and accounting, Portal authentication, and ICMP packets. Choose the command that matches the issue scenario. Replace the sample AC address, ports, and save path with actual values before running the command. After packet capture starts, repeat the network connection attempt on the affected endpoint and wait for the issue to recur. This captures the request and response for this authentication attempt.

```text
# Capture RADIUS authentication (UDP 1812) and accounting (UDP 1813) traffic that interacts with the AC (10.1.1.1), and display detailed packets in real time (including MAC addresses)
sudo tcpdump -i any  "host 10.1.1.1 and (udp port 1812 or udp port 1813)" -evvnn

# Capture RADIUS authentication and accounting traffic that interacts with the AC (10.1.1.1), and save it to /tmp/a.pcap (for Wireshark analysis)
sudo tcpdump -i any  "host 10.1.1.1 and (udp port 1812 or udp port 1813)" -v -w /tmp/a.pcap

# Capture authentication packets in scenarios that use SealSuite portalserver
# 9100 is the default port for the client to submit authentication information to SealSuite portalserver. 2000 is the port for SealSuite portalserver to submit authentication information to the network access device through the portal protocol. 1812 and 3812 are ports for radius authentication
sudo tcpdump -i any '((tcp port 9100) or (udp port 2000) or (udp port 1812))' -v -w 1.pcap
sudo tcpdump -i any '((tcp port 9100) or (udp port 2000) or (udp port 3812))' -v -w 2.pcap

# Capture ICMP (Ping) packets with a packet length greater than 1000 bytes
sudo tcpdump -i any  "icmp and greater 1000" -evvnn
```

### View and save packets

To view packets in real time, use the preceding example with `-evvnn` and observe the source address, destination address, and protocol details in the terminal output. To save packets, use `-w` to specify a file path before starting packet capture, such as `/tmp/a.pcap`. After the issue is reproduced, press **Ctrl+C** in the terminal running tcpdump to stop packet capture. Then read the file or import it into Wireshark for analysis.

To view a saved packet capture file from the command line, use `-r` to specify the file. The following command reads `/tmp/a.pcap` and displays addresses and ports in numeric form. Replace it with your own file path in actual operations:

```bash
sudo tcpdump -r /tmp/a.pcap -nn
```

## Determine authentication results

After packet capture is complete, first find the corresponding authentication packets based on the time when the issue occurred. Confirm whether requests, responses, and the final result are observed, and then determine the next inspection direction. Packets observable on the endpoint side differ from those observable on the RADIUS node side. Analyze them together with the packet capture location, RADIUS logs at the corresponding time, and network device configurations.

### View 802.1X authentication packets

On the endpoint side, use `eapol` to filter authentication packets and view EAP\-Request, EAP\-Response, and the final EAP\-Success or EAP\-Failure. On the RADIUS node side, view the Access\-Request sent by the network device and the Access\-Challenge, Access\-Accept, or Access\-Reject returned by the server.

EAP\-Success and Access\-Accept indicate successful authentication. EAP\-Failure and Access\-Reject indicate failed authentication. If only some requests or responses are observed, first record the missing interaction stage, and then troubleshoot the cause together with logs.

For specific inspection methods, see [Troubleshoot employee 802.1x wireless authentication network access failures (in Chinese)](https://help.feilian.cn/help-center/employee-8021x-wireless-authentication-networking-failure-troubleshooting-guide).

### View Portal authentication packets

When using SealSuite Portal Server, focus on whether the endpoint submits authentication information to Portal Server, whether Portal Server sends REQ_AUTH to the AC, whether the AC initiates RADIUS authentication, and the subsequent ACK_AUTH and AFF_ACK_AUTH. Example ports include TCP 9100, UDP 2000, and UDP 1812 for employee authentication or UDP 3812 for visitor authentication.

If Wireshark cannot parse the Portal protocol, use the `portal.lua` plugin. If visitor UDP 3812 packets cannot be recognized as RADIUS, use **Decode As** to specify the parsing protocol. For the plugin, configuration steps, and screenshots, see [Portal authentication (employee/visitor) network access failures (in Chinese)](https://help.feilian.cn/help-center/portal-certification-staff-visitor-networking-failure-troubleshooting-guide).

ACK_AUTH with ErrCode=0 indicates successful authentication. Other values require analysis based on the specific error code and logs. If authentication succeeds but the network remains inaccessible, further verify the delivered permissions and network\-side access status.

### Confirm results with logs

In the `radius.event.log` of the corresponding RADIUS node, search for `user conn report` by the time when the issue occurred. Then use information such as the account to confirm whether it is the authentication record for this attempt. Check `connResult`:

* `1` indicates successful authentication. If authentication and permission delivery are normal but the endpoint still cannot access the network, work with the network Administrator or device vendor to check network\-side issues.

* `2` indicates failed authentication. Continue troubleshooting based on the specific error logs for this authentication attempt.

* `3` indicates authentication downgrade. Check Dynamic Control policies and confirm whether restrictive remediation was triggered.

If you still cannot locate the issue, save the issue time accurate to the minute, the impact scope, the checks performed and their results, the corresponding RADIUS logs, and packet capture files, and provide them to technical support.
