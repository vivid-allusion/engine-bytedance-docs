---
title: "Type of address"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/type_of_address"
---

This topic describes the address types supported by RDS for MySQL. You can select the appropriate address to access and manage MySQL instances based on your business needs.


|Type of Address ||**Description** |Precautions |
|---|---|---|---|
|Private access |Private address |Accessing MySQL instances through a private address ensures maximum security and performance. |* The creation of MySQL instances generates a private address by default.<br><br>* Private addresses of MySQL instances cannot be deleted.<br><br>* Private addresses cannot be edited, but private ports can be modified.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information about how to access MySQL instances through a private address, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_address_and_port">Connecting to an Instance via Private Network</a>.</div><br> |
|Internet access |Public address |You can request public addresses for MySQL instances so that devices outside the VPC can access MySQL instances. |* Internet connection has certain security risks, so RDS for MySQL does not enable public addresses by default. You can manually make a request on the console. For more information about how to request a public address, refer to [Accessing a database via internet](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access).<br><br>* We recommend that you release public addresses promptly when devices outside the VPC no longer need to access MySQL instances. For releasing a public address, refer to [Releasing a public network address](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information about how to access MySQL instances through a public address, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access">Accessing a database via internet</a>.</div><br> |


<span id="faqs"></span>
## FAQs

<span id="can-i-obtain-the-ip-address-of-the-public-or-private-connection-to-a-mysql-instance"></span>
### Can I obtain the IP address of the public or private connection to a MySQL instance?

No.MySQL addresses are provided in the form of domain names.
