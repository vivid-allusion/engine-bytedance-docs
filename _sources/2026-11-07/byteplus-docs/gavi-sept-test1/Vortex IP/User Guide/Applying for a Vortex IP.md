---
title: "Applying for a Vortex IP"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Apply_for_a_Vortex_IP"
---

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before applying for a Vortex IP, you need to ensure the following:


* You have [registered a BytePlus account](https://docs.byteplus.com/en/docs/6261/64925) and completed [enterprise real-name authentication](https://docs.byteplus.com/en/docs/6261/64937).

* The total value of both your [available balance](https://docs.byteplus.com/en/docs/6269/100429) and coupons applicable for Vortex IP is not less than USD 100.00, and the available balance must be no less than 0. 

* The limits for Vortex IP with **Dynamic residential proxy** are detailed in [Limits](https://docs.byteplus.com/en/docs/gavi-sept-test1/Constraints#.5L2_55So6ZmQ5Yi2). Confirm before proceeding.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to [the Vortex IP console](https://console.byteplus.com/eip/region:eip+ap-southeast-1/vortexips).

2. Click **Apply for Vortex IP** to enter the Apply for Vortex IP page.

3. Configure relevant parameters based on the table below.

   
   |Parameters |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Billing method |Currently only Pay\-as\-you\-go is supported. |Pay\-as\-you\-go |
   |Region |Currently only support Asia Pacific (Johor). |Asia Pacific (Johor) |
   |Name |Type the name for the Vortex IP. |VortexIP\-1 |
   |Password |Type the authentication password for Vortex IP. The password is used in the [endpoint information](https://docs.byteplus.com/en/docs/gavi-sept-test1/Configure_the_endpoint_generator#.5q2l6aqk5LiA77ya55Sf5oiQ56uv54K5) to authenticate the Vortex IP instance. Keep it secure.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After creating a Vortex IP instance, you can click the icon to the right <strong>Password</strong> in the instance details page <img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8fd5c94b7dea6382dafacc4645080a57.png" />to modify the password.</div><br> |wbV\*\*\*4qL |
   |**Service configuration** |||
   |Service type |Select a service type for Vortex IP. Note that the service type is non\-changeable once created:<br><br><br>* Dynamic data center proxy: The proxy IP address is dynamically assigned from a data center’s public IP address pool. It is commonly used for services requiring frequent IP rotation and higher output speeds.<br><br>* Dynamic residential proxy: A dynamically rotating residential network IP. It is commonly used for scenarios requiring access to complex websites through local IPs, simulating real visitors to view or collect relevant data.<br><br>* Video\-specific proxy: The proxy service focuses on specific video websites and can improve the access success rate for video websites.<br><br>* Lightweight dynamic residential proxy: A lighter version of the dynamic residential proxy, delivering highly cost\-effective residential IP resources ideal for large\-scale offline scenarios.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Vortex IP lightweight dynamic residential proxy is currently in the beta stage. To request a trial, please contact your account manager.</div><br> |Dynamic data center proxy |
   |Metering method |Currently only Pay\-by\-data\-transfer is supported. |Pay\-by\-data\-transfer |
   |Maximum bandwidth |Set the maximum bandwidth for Vortex IP, measured in Mbps. After application, you can modify the maximum bandwidth as needed at any time. For the specific range, see [Performance limits](https://docs.byteplus.com/en/docs/gavi-sept-test1/Constraints#.5oCn6IO96ZmQ5Yi2). |20 Mbps |
   |**Network configuration** |||
   |Access mode |Two access modes are available: Internet and VPC.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The internet access mode is in the beta stage. If you need a trial, please contact your account manager.</div><br> |VPC |
   |VPC |When the access mode is **VPC**, select the VPC where the Vortex IP resource is deployed. Once the Vortex IP instance is created, you cannot modify it. Proceed with caution. |VPC\-1 |
   |Subnet |When the access mode is **VPC**, select a subnet. The subnet contains at least one available private IP. The system\-generated Vortex IP network interface will occupy a private IP address of the subnet. |Subnet\-1 |
   

4. Click **Confirm order** to enter the order page.

5. After confirming that the information is correct, follow the console guidance to review and accept the Legal, and click **Buy now** to complete the action.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the root account grants the permissions of <strong>VortexIPFullAccess</strong> or <strong>VortexIPReadOnlyAccess</strong> to the IAM user, the IAM user can view or use Vortex IP in the console. See <a href="https://docs.byteplus.com/en/docs/6257/64977">User management</a>.</div>


* <div data-tips="true" data-tips-type="tip">After creating a Vortex IP instance in Internet mode, it defaults that any Internet egress IP of Internet clients can access the Vortex IP. To restrict such access, you can <a href="https://docs.byteplus.com/en/docs/gavi-sept-test1/Manage_allowlist_entries#.5pON5L2c5q2l6aqk">add allowlist entries</a> to configure the inbound source allowlist.</div>



<span id=".55u45YWz5paH5qGj"></span>
## What to do next


* [Access target site](https://docs.byteplus.com/en/docs/gavi-sept-test1/Configure_the_endpoint_generator): After creating a Vortex IP instance, you also need to configure a Vortex IP proxy for an Elastic Compute Service (ECS).

* [Manage allowlist entries](https://docs.byteplus.com/en/docs/gavi-sept-test1/Manage_allowlist_entries): After a Vortex IP instance in Internet mode is created, any Internet client can access the Vortex IP by default. You can add allowlist entries based on your business requirements to control CIDR blocks for inbound access IPs. The configuration takes effect upon completion.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateVortexIP](https://docs.byteplus.com/en/docs/gavi-sept-test1/CreateVortexIP): Apply for a Vortex IP.
