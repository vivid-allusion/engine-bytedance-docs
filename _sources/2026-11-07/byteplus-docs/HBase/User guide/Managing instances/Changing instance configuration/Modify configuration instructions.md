---
title: "Modify configuration instructions"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Modify_configuration_instructions"
---

Yes. You can flexibly change the configuration of your HBase instance based on your business volume, including horizontal scaling (adding nodes) and vertical scaling (upgrading or downgrading node specifications).

<span id=".5Y-Y6YWN5pa55qGI"></span>
## Changing the configuration plan

The configuration items that support changes for HBase instances are shown in the following table.


|Change type ||Change description |Impact of change |
|---|---|---|---|
|**Upgrade configuration** |Master |* Supports upgrading node specifications.<br><br>* Increasing the number of nodes is not supported and is fixed at 2 nodes. |During the node specification upgrade process, the instance may be disconnected for 1 to 3 minutes. Please proceed with caution. It is recommended to perform conversion operation during off\-peak hours, and ensure clients are configured with proper retry mechanisms. |
||Region Server |* Supports upgrading node specifications.<br><br>* Supports increasing the number of nodes, up to 100 nodes. |Upgrading node specifications and increasing the number of nodes has no impact on instances and services. |
||Storage space |Supports expanding storage space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default storage space limit supported by each instance is 20,000 GiB, with a step size of 10 GiB. You can contact technical support to raise the limit by <a href="https://console.byteplus.com/workorder/create/">submitting a ticket</a>.</div><br> |None |
|**Lower the configuration** |Master |* Supports reducing node specifications.<br><br>* Reducing the number of nodes is not supported and is fixed at 2 nodes. |When downgrading the node specifications, the instance may be disconnected for 1 to 3 minutes. Please proceed with caution. It is recommended to perform conversion operation during off\-peak hours, and ensure clients are configured with proper retry mechanisms. |
||Region Server |* Supports reducing node specifications.<br><br>* Supports reducing the number of nodes to at least 2 nodes. |* Reducing the node specifications has no impact on instances or services.<br><br>* When reducing the number of Region Server nodes, the instance may experience minute\-level jitter. Please proceed with caution. It is recommended to perform configuration changes during off\-peak hours. |
||Storage space |Supports reducing storage space.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When scaling down, the target storage space cannot be less than 140% of the currently used storage space. Please make a reasonable choice based on your actual business situation.</div><br> |None |


<span id=".5Y-Y6YWN6K6h6LS56KeE5YiZ"></span>
## Change billing rules

 To change instance configuration billing rules, see [Billing Rules for Resource Subscription Change](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change).
