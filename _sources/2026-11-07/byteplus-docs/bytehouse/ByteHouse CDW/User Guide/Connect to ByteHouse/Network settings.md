---
title: "Network settings"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/network-settings"
---

To ensure connection security, ByteHouse supports linking VPC/EIP to build tenant\-level private networks and public domain name access, and allows configuration of IP white lists to manage access permissions. This document introduces the configuration methods for public networks, private networks, and IP white lists.

<span id="49395d39"></span>
# Usage restrictions

Only users with the AccountAdmin role can configure private domain, public domain, and set IP whitelists. Other users can only view private and public network information and apply the configured IP whitelists.

<span id="15d71e04"></span>
# Configure private domain

<span id="04ab01a2"></span>
## Bind private network


1. Log in to the ByteHouse Console, go to **Tenant management**\-\>**Basic information**\-\>**Network information** module, click the **Go to Bind** button after the private domain name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ddd3a6eafb04d4a9ab6b0a51ceba135~tplv-goo7wpa0wc-image.image) </span>

2. On the Bind Private Network page, select the created private network, subnet, and security group, and click **Submit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e399cd8899c44aa9cfd6826a9d8cf92~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the IPv4 CIDR conflicts with the IP address of the private network environment, the subnet will not be displayed. Since the private network CIDR ranges and IP addresses vary across different environments, please refer to the IP addresses displayed on the actual interface.   </div>
   

   If there are no available options in your list or you need to create new options, click the **Create** button corresponding to the item, complete creation, then return to this page to configure binding information. For related operations details and cost information, refer to the following documents:

   * [Create a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC)

   * [Create a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet)

   * [Create a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group)

   * [Private Network Billing](https://docs.byteplus.com/en/docs/vpc/Billing)

3. (Optional) After binding is complete, you can click the **Details** button next to the private network domain name to view detailed information about the currently bound private network, subnet, security group, and private network IP address.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e04a85f9fe744370ab2b8f4b6e903099~tplv-goo7wpa0wc-image.image) </span>


<span id="f20a8bd6"></span>
## Rebind private domain name

<span id="25ba22e8"></span>
### Prerequisites

If you have already linked a public domain name, first [Unbind public domain](https://docs.byteplus.com/docs/bytehouse/network-settings#b3f6baa5) then perform the operation of changing to a private domain name.

<span id="371c721c"></span>
### Steps


1. Click the **Rebind** button behind the private domain name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc8d686375df49a9ac07abc2e3e41f33~tplv-goo7wpa0wc-image.image) </span>

2. On the private domain change page, select private network, subnet, and security group, and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ade42ca7dd664412915ea39f91eb3363~tplv-goo7wpa0wc-image.image) </span>


<span id="f1dd09e9"></span>
## Activate/terminate public domain resolution

The public domain resolution function supports resolving the current private domain name in a public network environment, which is suitable for connections in scenarios like dedicated lines.

Click the **Public Domain Resolution** followed by the **Go to enable** button, and click **Confirm**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac8ec1a69c9c4377813857ed6934679d~tplv-goo7wpa0wc-image.image) </span>

After activation, if you need to terminate public domain resolution, click the **Public Domain Resolution** followed by the **Go To** **Disable** button, and click **Confirm**.

<span id="824d43ce"></span>
# Configure public domain

<span id="7f4f345e"></span>
## Bind public domain


1. Click the **Go to Bind** button after the public Domain Name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07bd1262e3e6407c9142d6acf949e568~tplv-goo7wpa0wc-image.image) </span>

2. On the Bind Public IP Page, select an available public IP and click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5cb95774ea143f194a6af635282b624~tplv-goo7wpa0wc-image.image) </span>

   If there are no available public IPs in your list, click **Create IP** to create a new public IP, then return to this page to configure the binding information. The operation details and costs of creating a public IP can be referred to in the following document:

   * [Apply for a public IP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP)

   * [Public IP - Billing Overview](https://docs.byteplus.com/en/docs/eip/Billing-overview)

3. (Optional) After binding is complete, you can click the **Details** button next to the public domain name to view the currently bound public name and IP address.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6855dacc738463db25d3b05ed66a502~tplv-goo7wpa0wc-image.image) </span>


<span id="b3f6baa5"></span>
## Unbind public domain

Click the **Go to Unbind** button after the public Domain Name, and click **Confirm**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2cb6923c88749fcaff3ef9b1e9ac433~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Unbound public network IP resources will continue to incur charges. If you no longer use this resource, please go to the <a href="https://console.byteplus.com/eip/eips">EIP Console</a> to release it.</div>


<span id="d00810e1"></span>
# Set IP whitelist

<span id="c0a781c1"></span>
## Add whitelist


1. Click the **Whitelist Configuration** button of the \*\*Network information \*\*module.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78d80388320d4fa3afb52f8cb9bda240~tplv-goo7wpa0wc-image.image) </span>

2. Enter the IP address or range to be added to the text box on the White List Configuration page, and click**Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c159b7c9816c4981a39480d1d12a1473~tplv-goo7wpa0wc-image.image) </span>

   The requirements for setting IP addresses are as follows:

   * Setting '0.0.0.0/0' allows access from all addresses, setting '127.0.0.1/32' prohibits access from all addresses.

   * If both '0.0.0.0/0' and '127.0.0.1/32' are set, it means that access from all addresses is allowed.

   * Only IP ranges are supported for input, not individual IP addresses, and ranges are separated by commas, spaces or newline characters in English and Chinese.

   * After removing an IP from the Whitelist, established connections with that IP will be immediately disconnected.

   * Up to 300 IP ranges can be set.

      If the IP address you enter does not meet the requirements, the system will notify you that the entry cannot be processed. Please modify according to the above requirements, or click **Click to Clear**, and the system will automatically clear the unprocessable IP addresses.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c56a316354d84fabae92d206c656bf58~tplv-goo7wpa0wc-image.image) </span>


<span id="1e5ff5ea"></span>
## Edit whitelist

Click the **Whitelist Configuration** button after the public domain name, adjust the IP address in the text box on the whitelist configuration page, and click **Save**.

<span id="f3596920"></span>
## Delete whitelist

Click the **Whitelist Configuration** button after the public domain name, delete the IP address in the text box on the whitelist configuration page, and click **Save**.
