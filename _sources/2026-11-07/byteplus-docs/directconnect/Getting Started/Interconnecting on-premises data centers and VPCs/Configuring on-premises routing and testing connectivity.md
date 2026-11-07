---
title: "Configuring on-premises routing and testing connectivity"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Configuring-a-local-route-and-testing-connectivity"
---

<span id=".6YWN572u5pys5Zyw6Lev55Sx"></span>
## Configure on\-premises routing

After Direct Connect is configured in the BytePlus console, you must also configure the private network routing locally to truly achieve network interconnection between a data center (private CIDR block: 172.16.0.0/24) and a Virtual Private Cloud (VPC).

Configuration commands may vary across different devices. Please configure according to your specific device during actual operation. Example of on\-premises data center (IDC) route configuration in BGP routing mode:

```Plain Text
bgp 49600
peer 10.0.0.1 as-number 137718
peer 10.0.0.1 password simple 123456
network 172.16.0.0 255.255.255.0
```



|Parameter |Description |
|---|---|
|49600 |BGP Peer ASN of the data center |
|137718 |ASN of BytePlus |
|10.0.0.1 |This IP is typically the local (cloud\-side) interconnect IP address filled in when creating the virtual interface |
|123456 |BGP key of the data center |
|172.16.0.0 |Private CIDR block of the data center |
|255.255.255.0 |Mask of the data center |


<span id=".5rWL6K-V6L-e6YCa5oCn"></span>
## Test connectivity

You can test connectivity to verify whether the network between the on\-premises IDC and the VPC is properly established.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. On the on\-premises IDC side, log in to any server and open a command window.

2. Execute the `ping 10.0.0.1` command to test connectivity from the on\-premises IDC to the DC Gateway network.

   Expected result: Ping successful. The on\-premises data center is properly connected to the DC Gateway network.

3. Execute the `ping 192.168.1.10` command to test connectivity from the on\-premises IDC to the VPC network.

   Expected result: The ping is successful, indicating normal network connectivity from the on\-premises IDC to the VPC side.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">192.168.1.10 is an IP address within the CIDR block (192.168.1.0/24) of VPC\-123.   </div>
