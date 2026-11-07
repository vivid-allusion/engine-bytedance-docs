---
title: "Viewing allowlist information"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Viewing_allowlist_information"
---

You can view the details of a target allowlist and its associated instances in the console. This article describes how to view allowlist information.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An allowlist has been created. For details, see [Creating an allowlist](https://docs.byteplus.com/en/docs/HBase/Creating_an_allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Allowlists** page, click the name of the target allowlist.

4. On the target allowlist information page, you can view the following information.

   
   |Classification |Description |
   |---|---|
   |**Allowlist information** |You can view the target allowlist, description, IP addresses, and whether it is the default allowlist.<br><br>You can click **Edit** to modify the allowlist information. For more details, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist). |
   |**List of associated instances** |View information for all instances associated with this allowlist.<br><br>You can also click **Associate Instance** in this area to associate an instance to the allowlist. Or click **Disassociate instance** to disassociate the instance from the allowlist. For details, see [Associating allowlist and instance](https://docs.byteplus.com/en/docs/HBase/Associating_allowlist_and_instance) and [Disassociating instance and allowlist](https://docs.byteplus.com/en/docs/HBase/Disassociating_instance_and_allowlist).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After disassociating the instance from the allowlist, the allowlist can no longer access the instance. Proceed with caution.</div><br> |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/HBase/DescribeAllowListDetail) |Call the DescribeAllowListDetail API to view the details of a specified allowlist, including its IP addresses and associate instances. |
