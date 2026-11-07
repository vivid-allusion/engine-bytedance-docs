---
title: "Modifying address prefix and port"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_address_prefix_and_port"
---

MySQL provides public and private network addresses for you to access MySQL instances. This topic describes how to modify the prefixes of public and private network addresses and modify the public and private ports.

<span id="prerequisites"></span>
## Prerequisites


* An instance has been created and is in the **Running** status. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* If you must modify the prefix of a public address, you must enable internet access for the connection endpoint.For the steps to enable internet access, refer to [Enabling internet access](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access).


<span id="precautions"></span>
## Precautions


* You can only modify the prefix of an address. A private address can only end with the suffix `.rds.ibytepluses.com`, and a public address can only end with the suffix `.rds.ibytepluses.com`.

* The new address becomes valid after the modification is confirmed. The old address will become invalid 3 minutes after the new address takes effect. Please modify the link configuration of the application synchronously, otherwise the business may be affected. Please be careful.

* Once the new port takes effect, the old port will be closed immediately. Please modify the connection configuration of the application simultaneously, otherwise it may affect the business, so please operate with caution.

* When creating a new connection endpoint or opening a new address, the real\-time configuration of the private network port of the default connection endpoint will be automatically used as its default port. For example, the default private network port of the connection endpoint is configured as 3307. When a new connection connection endpoint is created, the private network port of the new connection connection endpoint will also be configured as 3307 by default; when a new public network connection is opened, the port will also be configured as 3307. If the private network port of the default connection endpoint is configured as 3308, when a new connection connection endpoint is created, the private network port of the new connection connection endpoint will also be configured as 3308 by default; when a new public network connection is opened, the port will also be configured as 3308.


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>All resources</strong> at this step.</div>



3. Click **Instances** in the left\-side navigation bar.

4. Go to the **Instances** page and click on the target instance name to open the **Summary** page.

5. Click **Connectivity** at the top of the page to go to the **Connectivity** tab.

6. You can hover the cursor over the target connection endpoint in the **Instance topology** area on the **Connectivity** page, and then click **Edit** to go to the **Modify endpoint** page.

   * Modify the connection address

      Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5e1aa6ae2ea88883e71f0a7fd839661.png) </span> to the right of the public or private address in the **Connection information** area on the **Modify endpoint** page, and fill in the new public or private address in the pop\-up **Modify private network address** or **Modify the public address** window. Each public address and private address must meet the following rules:

      * The prefix of the address must contain at least 8 characters, and the total length of the address (including the suffix) shall not exceed 63 characters.

      * It starts with a lowercase letter and ends with a lowercase letter or a digit.

      * It consists of lowercase letters, digits, and hyphens ( \- ).

   * Modify the port

      Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5e1aa6ae2ea88883e71f0a7fd839661.png) </span> to the right of the private address port in the **Connection information** area on the **Modify endpoint** page, and enter the new port number. Port number range: 1000 to 65534.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">After clicking <strong>OK</strong>, the instance status changes to <strong>Network changing</strong>. After the modification is executed, the instance status changes to <strong>Running</strong>.</div>


<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBEndpointAddress](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpointaddress) |Call the ModifyDBEndpointAddress interface to modify the prefix or port of the address. |


&nbsp;
