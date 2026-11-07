---
title: "Applying for a Vortex IP in VPC mode and testing feasibility"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Apply_for_a_Vortex_IP_in_VPC_mode_and_test_feasibility"
---

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations


* You have [registered a BytePlus account](https://docs.byteplus.com/en/docs/6261/64925) and completed [enterprise real-name authentication](https://docs.byteplus.com/en/docs/6261/64937).

* Ensure that the sum of both your [available balance](https://docs.byteplus.com/en/docs/6269/100429) and coupons applicable for Vortex IP is not less than USD 100.00, and the available balance must be no less than 0. 

* You have created a Virtual Private Cloud (VPC) and subnets, and created an Elastic Compute Service (ECS) instance without any associated Elastic IP address (EIP) in a subnet. For procedures, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Buying ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Step 1: Apply for Vortex IP](https://docs.byteplus.com/en/docs/147/72737#.5q2l6aqk5LiA77ya55Sz6K-3Vm9ydGV4IElQ): Apply for a Vortex IP instance.

2. [Step 2: Generate an endpoint](https://docs.byteplus.com/en/docs/147/72737#.5q2l6aqk5LqM77ya55Sf5oiQ56uv54K5): Configure the endpoint generator to generate endpoint information.

3. [Step 3: Configure ECS instance](https://docs.byteplus.com/en/docs/147/72737#.5q2l6aqk5LiJ77ya6YWN572uRUNT5a6e5L6L): Configure the endpoint information into the ECS instance.

4. [Step 4: Verification](https://docs.byteplus.com/en/docs/147/72737#.5q2l6aqk5Zub77ya6aqM6K-B): Verify whether the proxy IP address of the ECS switches dynamically.


<span id=".5q2l6aqk5LiA77ya55Sz6K-3Vm9ydGV4IElQ"></span>
### Step 1: Apply for Vortex IP


1. Log in to [the Vortex IP console](https://console.byteplus.com/eip/region:eip+ap-southeast-1/vortexips).

2. Click **Apply for Vortex IP** to enter the Apply for Vortex IP page.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Notes |Example value |
   |---|---|---|
   |Billing method |Currently only support Pay\-as\-you\-go. |Pay\-as\-you\-go |
   |Region |Currently only support Asia Pacific (Johor). |Asia Pacific (Johor) |
   |Name |Type a name for Vortex IP. |VortexIP\-1 |
   |Password |Type the authentication password for Vortex IP. The password is used in the [endpoint information](https://docs.byteplus.com/en/docs/gavi-sept-test1/Configure_the_endpoint_generator#.5q2l6aqk5LiA77ya55Sf5oiQ56uv54K5) to authenticate the Vortex IP instance. Keep it secure. |wbV\*\*\*4qL |
   |Service type |Select a service type for Vortex IP. Note that the service type is non\-changeable once created:<br><br><br>* Dynamic data center proxy: The proxy IP address is dynamically assigned from a data center’s public IP address pool. It is commonly used for services requiring frequent IP rotation and higher output speeds.<br><br>* Dynamic residential proxy: A dynamically rotating residential network IP. It is commonly used for scenarios requiring access to complex websites through local IPs, simulating real visitors to view or collect relevant data.<br><br>* Video\-specific proxy: The proxy service focuses on specific video websites and can improve the access success rate for video websites.<br><br>* Lightweight dynamic residential proxy: A lighter version of the dynamic residential proxy, delivering highly cost\-effective residential IP resources ideal for large\-scale offline scenarios. |Dynamic data center proxy |
   |Metering method |Select a metering method for Vortex IP, supporting only Pay\-by\-data\-transfer. |Pay\-by\-data\-transfer |
   |Bandwidth |Set the maximum bandwidth for Vortex IP, measured in Mbps. After application, you can modify the maximum bandwidth as needed at any time. For the specific range, see [Performance limits](https://docs.byteplus.com/en/docs/gavi-sept-test1/Constraints#.5oCn6IO96ZmQ5Yi2). |20 Mbps |
   |Access mode |Select an access mode for Vortex IP.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is shown only when the Internet access mode is enabled. The internet access mode is in the beta stage. If you need a trial, please contact your account manager.</div><br> |VPC |
   |VPC |Select the VPC where the Vortex IP resource is deployed. It is non\-changeable. |VPC\-1 |
   |Subnet |Select a subnet from the dropdown list. The subnet contains at least one available private IP. The system\-generated Vortex IP network interface occupies a private IP address of the subnet. |Subnet\-1 |
   

4. Click **Confirm order** to enter the order page.

5. After confirming that the information is correct, follow the console guidance to review and accept the Legal, and click **Buy now** to complete the action.


<span id=".5q2l6aqk5LqM77ya55Sf5oiQ56uv54K5"></span>
### Step 2: Generate an endpoint


1. Log in to [the Vortex IP console](https://console.byteplus.com/eip/region:eip+ap-southeast-1/vortexips).

2. In the top menu bar, select your target region.

3. In the Vortex IP list, click **Endpoint generator** to the right of the target Vortex IP to pop up the Endpoint generator window.

4. Configure relevant parameters based on the table below.

   
   |Parameter |Notes |Example value |
   |---|---|---|
   |Country/region |Select your target country and region.<br><br><br>* Specify country/region: Use public IPs located in the specified country/region to access the target site.<br><br>* Do not specify country/region: By default, the egress IP is randomly assigned from the global pool. |Random |
   |Session Persistence |Specify whether to enable session persistence.<br><br><br>* Enable: Requests with the same session ID (Security Identifier) will use the same public IP address to access. Idle timeout for access requests is 1 minute.<br><br>* Not enable: The public IP address changes with each request by default. |Not enable |
   |Output format |Select the output format for the egress IP. Supports **Endpoint: Port** and three access protocols: **HTTP**, **HTTPS**, and **SOCKS5**. |HTTP |
   

5. Click **Generate** to automatically generate endpoint information (using the generated endpoint `http://proxy:wbV***4qL@vortex-n0i6m.vortexip_stable.ap-southeast-1.volces.com:8080` as an example).

6. Copy the endpoint information to configure the proxy for the created ECS instance.


<span id=".5q2l6aqk5LiJ77ya6YWN572uRUNT5a6e5L6L"></span>
### Step 3: Configure ECS instance

Log in to the prepared ECS instance, and configure the proxy (using the endpoint `http://proxy:wbV***4qL@vortex-n0i6m.vortexip_stable.ap-southeast-1.volces.com:8080` as an example).

```mixin-react
const list = [
  {
    "lang": "cURL",
    "text": `curl "https://ipinfo.io" -x http://proxy:wbV***4qL@vortex-n0i6m.vortexip_stable.ap-southeast-1.volces.com:8080`,
    "selected": true,
  },
  {
    "lang": "Node.js",
    "text": `#!/usr/bin/env node

require('request-promise')({
    url: 'https://ipinfo.io',
    proxy: 'http://proxy:wbV***4qL@vortex-n0i6m.vortexip_stable.ap-southeast-1.volces.com:8080',
  })
  .then(function (data) {
      console.log(data);
    },
    function (err) {
      console.error(err);
    });`, 
    "selected": true,
  },
  {
    "lang": "Python",
    "text": `import pprint
import requests

proxy_url = http://proxy:wbV***4qL@vortex-n0i6m.vortexip_stable.ap-southeast-1.volces.com:8080

proxies = {
    'http': proxy_url,
    'https': proxy_url
}


url = "https://ipinfo.io"
response = requests.get(url, proxies=proxies)
pprint.pprint(response.json())`, 
    "selected": true,
  },
]
return (<PreCodeTabs list={list} />);
```


<span id=".5q2l6aqk5Zub77ya6aqM6K-B"></span>
### Step 4: Verification


1. Log in to the prepared ECS instance.

2. Execute `curl https://ipinfo.io` or `curl http://ipinfo.io` to verify.

   ```Plain Text
   {
     "ip": "93.***.***.49",
     "city": "Singapore",
     "region": "Singapore",
     "country": "SG",
     "loc": "******",
     "org": "******",
     "postal": "10***",
     "timezone": "Asia/Singapore",
     "readme": "https://ipinfo.io/missingauth"
   }
   ```
   

   When the ECS instance successfully accesses `https://ipinfo.io` and returns the IP information of the access request (i.e., the information of the proxy IP), it indicates a successful configuration.

   > For more information, see [Access code example](https://docs.byteplus.com/en/docs/gavi-sept-test1/Configure_the_endpoint_generator#dMNPpshN).
