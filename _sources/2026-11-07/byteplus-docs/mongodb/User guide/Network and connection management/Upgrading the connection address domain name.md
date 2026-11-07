---
title: "Upgrading the connection address domain name"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Upgrading_the_connection_address_domain_name"
---

Document Database for MongoDB has upgraded its connection address domain name, incorporating region information into the domain name suffix. This domain name can be used across all regions under BytePlus, enhancing the convenience of multi\-region domain name management.

<span id="u8NBxtT4"></span>
## Background information

Starting from March 24, 2025, Document Database for MongoDB has upgraded its connection address domain name. The upgraded connection address domain name suffix will automatically include the region information of the instance. For instances in the following regions, the upgraded connection address domain name enables cross\-region access among these regions. If your instance in other regions requires cross\-region access, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact us.


* China (Beijing)

* China (Shanghai)

* Asia Pacific (Johor)


The differences in addresses before and after the upgrade are shown in the table below.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The table below uses the single\-node connection address of a replica set instance as an example. For more information about MongoDB connection addresses, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/addresses-introduction">Viewing connection address</a>.</div>


* <div data-tips="true" data-tips-type="default">In the example, <code>{Region ID}</code> is the ID of the region where the instance belongs, such as <code>cn-beijing</code>. For more information about MongoDB service addresses, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/request-structure?lang=en#9TeFSOVO"> endpoints endpoints endpoints</a>.</div>




|Address type |Private network address |Public network address |
|---|---|---|
|Before upgrade |`bao43o6s5ofzxec****.mongodb.ivolces.com:3717` |`bao43o6s5ofzxec****.mongodb.volces.com:3717` |
|After the upgrade |`bao43o6s5ofzxec****.mongodb.{Region ID}.ivolces.com:3717` |`bao43o6s5ofzxec****.mongodb.{Region ID}.volces.com:3717` |


<span id="Mg2SSXeq"></span>
## Prerequisite

The instance status must be **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

<span id="wyic1lDC"></span>
## Precautions


* After the connection address domain name is upgraded, the domain name suffix will not revert to the old format even if the corresponding connection address is released and re\-applied.

* After the upgrade, old connections will no longer work. Promptly update your client configuration to use the new connection address. For specific procedures, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).


<span id="HAhPL5yT"></span>
## Procedure

The upgrade procedure for the connection address domain varies depending on the instance creation time.


|Instance creation time |Address type |Upgrade procedure |
|---|---|---|
|**On or before March 24, 2025**<br><br> |Default private network address<br><br> |Trigger an upgrade by [Modifying connection address](https://docs.byteplus.com/en/docs/mongodb/modify-connection-address).<br><br>When the connection address domain name is modified, the domain name suffix automatically includes the instance's region information, and the upgraded domain name takes effect in all regions under BytePlus. |
||Other private or public address |Trigger an upgrade by [Applying for private address](https://docs.byteplus.com/en/docs/mongodb/apply-private-address) or [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For private or public addresses applied on or before March 24, 2025, you must first <a href="https://docs.byteplus.com/en/docs/mongodb/release-private-address">release the private address</a> or <a href="https://docs.byteplus.com/en/docs/mongodb/release-public-address">release the public address</a>, and then reapply to trigger the upgrade.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Newly requested connection addresses will automatically include the instance's region information.</div><br> |
|**After March 24, 2025** |Default private network address |No action required.<br><br>The default private network address for new instances automatically includes the instance's region information, and this domain name is valid across all regions under BytePlus. |
||Other private or public address |Simply [Apply for a private address](https://docs.byteplus.com/en/docs/mongodb/apply-private-address) or [Apply for a public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address). The newly applied connection address will automatically include the instance's region information. |


<span id="KhGoOD39"></span>
## FAQs


<span id="nTRBsP8u"></span>
### Can the old connection address still be used after the upgrade?

No. After the upgrade, old connections will no longer work. Promptly update your client configuration to use the new connection address. For procedures for connecting to an instance, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).



<span id="Wu4vlbmM"></span>
### After upgrading, can I revert to the old address domain by releasing and re\-applying for the address?

No. Even if you release and reapply for the corresponding connection address after the domain suffix of private or public network connection addresses is upgraded, the domain suffix will not revert to its old format.
