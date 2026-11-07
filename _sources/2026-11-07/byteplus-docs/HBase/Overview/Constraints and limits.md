---
title: "Constraints and limits"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Constraints_and_limits"
---

To improve the stability and security of instances, Table Storage for HBase has some limitations. The details are as follows.


|Constraints |Usage limitations |
|---|---|
|Data Plane |By default, the maximum data size for each cell in HBase cannot exceed 10 MB.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A cell refers to the total length of the rowKey and Value after serialization.</div><br> |
|Connection Address |HBase provides ZK and Thrift2 connection addresses to access instances. For details, see [Connection address type](https://docs.byteplus.com/en/docs/HBase/Viewing_connection_address#.6L-e5o6l5Zyw5Z2A57G75Z6L). |
|Storage space |Each instance has a default storage limit of 20,000 GiB. To increase this limit, you can [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/) to contact technical support. |
|Capacity storage space |Capacity storage can be used as cold storage. For more information about hot and cold storage separation, see the [About hot and cold data separation](https://docs.byteplus.com/en/docs/HBase/About_hot_and_cold_data_separation).<br><br>The default upper limit of capacity storage supported by each instance is 1,000,000 GiB, in increments of 10 GiB. |
|Add or remove nodes |* The number of Master nodes is fixed at 2 and cannot be changed.<br><br>* The number of Region Server nodes is 2 by default, with a range of 2 to 100. |
|Allowlist Management |* Each account can create a maximum of 100 allowlists in each region.<br><br>* Each allowlist can be associated to a maximum of 200 instances, with up to 50 instances per batch.<br><br>* Each instance can be associated to a maximum of 100 allowlists, with up to 100 allowlists per batch. |
|Instance parameters |Instance parameters can only be modified through the console. For security and stability reasons, only some parameters can be modified. For details, see [List of modifiable parameters](https://docs.byteplus.com/en/docs/HBase/List_of_modifiable_parameters). |
|Restart instance |HBase instances can only be restarted through the console or an API. The console supports batch restarts for up to 100 instances. |
|Instance Deployment |The server where the instance is deployed is not visible. Applications can only access the database using the connection address and port. |
