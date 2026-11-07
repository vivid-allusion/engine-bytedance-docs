---
title: "Direct Connect health check overview"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Direct_Connect_health_check_overview"
---

When you transmit business data between cloud/on\-premises BytePlus and the third\-party cloud via a Direct Connect (DC) connection, and any significant network fluctuations or unstable transmission links occur, you can use the DC health check to identify and detect network issues. The health check sets source and destination IPs in the DC connection to form probes, and provides real\-time feedback on network health by actively sending detection requests. This helps you quickly identify network issues and take appropriate actions to ensure stable business operation.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Health checks may consume some network resources. We recommend configuring the packet size of health check data reasonably based on your business requirements.</div>


* <div data-tips="true" data-tips-type="warning">Health checks do not provide fault route switching capability. For such business needs, see <a href="https://docs.byteplus.com/en/docs/directconnect/Detection_methods">Line health check</a>.</div>



<span id="O73J2OZ9"></span>
## <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25e7719af7ad7944ab92a8b167db0fd1.png) </span>

<span id="O73J2OZ9"></span>
## Terms


|Name |Notes |
|---|---|
|Health Check |DC health check is a mechanism for monitoring the quality of the network link from VPC to the remote. Test network connectivity by actively sending Probe requests. As the health check integrates with CloudMonitor metrics and alerts, you will receive notifications when network exceptions occur. |
|Probe |A probe consists of a set of cloud source IPs and on\-premises destination IPs. The source IPs continuously send data packets (ICMP) to the destination IPs to collect latency and packet loss rate data for the link, with the data updated in real time. |


<span id="cPKKPQJR"></span>
## Usage process


1. [Create health check instance](https://docs.byteplus.com/en/docs/directconnect/Creating_a_health_check)

2. [Add network link probe](https://docs.byteplus.com/en/docs/directconnect/Adding_a_probe)
