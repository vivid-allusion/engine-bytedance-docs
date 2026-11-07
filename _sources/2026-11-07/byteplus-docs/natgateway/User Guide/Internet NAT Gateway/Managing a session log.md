---
title: "Managing a session log"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing_a_session_log"
---

<span id="TQaB1Q8y"></span>
## Application scenarios

Session logs are used to record traffic information passing through the NAT Gateway. After you create a SNAT entry for a NAT Gateway, an Elastic Compute Service (ECS) instance can share an Elastic IP Address (EIP) associated with the SNAT entry to access the Internet. Record SNAT sessions that pass through the NAT Gateway in log form and save logs in Torch Log Service (TLS), making it easier for you to trace and monitor.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The session log feature is available only for <strong>Pay\-by\-CU Internet NAT Gateways</strong>.</div>


<span id="dduiMG3V"></span>
## Instructions


* Currently, obtaining DNAT session log information is unsupported.

* Each NAT Gateway instance supports creating only one session log.

* The following table lists the parameters contained in the session logs.

   
   |Parameter |Description |
   |---|---|
   |instance_id |ID of the NAT Gateway |
   |src_ip |Source IP address |
   |src_port |Source port |
   |protocol |Protocol |
   |dst_ip |Destination IP address |
   |dst_port |Destination port |
   |nat_eip |The EIP associated with the Internet NAT Gateway |
   |nat_ip |* For a non\-direct Internet NAT Gateway, it is a private IP address.<br><br>* For a VPC NAT Gateway, it is a NAT IP address. |
   |nat_port |* For an Internet NAT Gateway, it is an EIP port.<br><br>* For a Virtual Private Cloud (VPC) NAT Gateway, it is a NAT IP port. |
   |pkts_from_src |Packet out: Packets egressed from the NAT Gateway<br><br><br>* For an Internet NAT Gateway, it measures the count of packets sent to the Internet.<br><br>* For a VPC NAT Gateway, it measures the count of packets sent to another VPC. |
   |pkts_from_dst |Packet in: Packets ingressed to the NAT Gateway<br><br><br>* For an Internet NAT Gateway, it measures the count of packets received from the Internet.<br><br>* For a VPC NAT Gateway, it measures the count of packets received from another VPC. |
   |bytes_from_src |Outbound traffic: Traffic from the VPC to the NAT Gateway |
   |bytes_from_dst |Inbound traffic: Traffic from the NAT Gateway to the VPC |
   |start_time |The time when logging starts |
   |end_time |The time when logging ends. |
   


<span id="Lzczkh8u"></span>
## Prerequisites


* You have enabled BytePlus [TLS](https://docs.byteplus.com/en/docs/6470/).

* You must configure the cross\-service permission over TLS for your target account.

   * Initial authorization: When enabling session logs, follow the interface guidance to complete the cross\-service authorization over TLS.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After deleting the authorized role, you must re\-authorize to continue using the session log features.      </div>
      

   * Re\-authorization: In the **IAM \> Permission policy** page, [grant ](https://docs.byteplus.com/en/docs/6257/65058)**NatAccessTLSRolePolicy** to the account to enable cross\-service access.


<span id="Lzczkh8u"></span>
## Enable a session log


1. Log in to [the Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **Session log** tab.

5. Click **Enable**.

6. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Name of the session log. |SNAT\-TLS |
   |Log project |Create or select a project for managing NAT Gateway session logs. You cannot modify session logs upon creation.<br><br>A [log project](https://docs.byteplus.com/en/docs/tls/Managing_projects) is a fundamental unit for resource management, enabling log resource isolation and access control between multiple users, projects, or products.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only support selecting a log project in the same region as the Internet NAT Gateway.</div><br> |TLS\-Natproject |
   |Log topic |Create or select a log topic for storing NAT Gateway session logs. You cannot modify session logs upon creation.<br><br>A [log topic](https://docs.byteplus.com/en/docs/tls/Managing_topics) is a fundamental unit for TLS to manage logs. Features such as log ingestion, search and analysis, and consumption are performed at the granularity of log topics. |TLS\-Natsubject |
   |Log index |TLS supports log search and analysis. You can only query and analyze logs after configuring the index. After enabling, TLS will automatically configure the required index, and charge traffic fees for it.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can download raw log data or analyzed query results locally for data viewing or further analysis. <a href="https://docs.byteplus.com/en/docs/tls/Download-logs-2">Prerequisite</a></div><br><br><br>* <div data-tips="true" data-tips-type="default">Once enabled, disabling is unsupported. If the log index is no longer needed, <a href="https://docs.byteplus.com/en/docs/51/79159#46jG5i32">delete the session log</a> and create another.</div><br> |Not selected |
   

7. Click **Enable** to complete the action.


<span id="QoNs3hsJ"></span>
## Disable a session log

You can suspend session log collection at any time to meet changing business needs. After you disable a session log, the system will stop generating new log data.


1. Log in to [the Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **Session log** tab, and click **Disable** to the right of the target session log.

5. Click **Disable** to complete the action.


<span id="ZvJn6asi"></span>
## Start a session log

You can start a session log in the status of **Disabled** at any time. After starting, SNAT session collection resumes. That is, the system resumes generating new log data.


1. Log in to [the Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target NAT Gateway.

4. Select the **Session log** tab and click **Start** to the right of the target session log.

5. Click **Start** to complete the action.


<span id="46jG5i32"></span>
## Delete a session log

After you delete a session log, the system will no longer collect SNAT log data. Your existing log data remains stored in TLS. To delete it, see [Delete a topic](https://docs.byteplus.com/en/docs/tls/Managing_topics).


1. Log in to [the Internet NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the list of Internet NAT Gateways, click the name of the target Internet NAT Gateway.

4. Select the **Session log** tab, and click **Delete** to the right of the target session log.

5. Click **Delete** to complete the action.


<span id="ETVTsgJT"></span>
## Related documents


* [CreateNatLog](https://docs.byteplus.com/en/docs/natgateway/CreateSessionLog): Create a session log

* [DescribeNatLog](https://docs.byteplus.com/en/docs/natgateway/DescribeSessionLogs): Query session logs that meet specified conditions

* [ActiveNatLog](https://docs.byteplus.com/en/docs/natgateway/EnableSessionLog): Start a session log

* [DeactiveNatLog](https://docs.byteplus.com/en/docs/natgateway/DisableSessionLog): Disable a session log

* [DeleteNatLog](https://docs.byteplus.com/en/docs/natgateway/DeleteSessionLog): Delete a session log
