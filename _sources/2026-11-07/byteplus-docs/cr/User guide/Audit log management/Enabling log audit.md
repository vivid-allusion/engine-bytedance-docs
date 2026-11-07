---
title: "Enabling log audit"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Turn_On_Audit_log"
---

CR supports image push and pull logs via log audit, helping you understand the status of image push and pull operations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This operation is only applicable to Standard Edition instances.</div>


* <div data-tips="true" data-tips-type="warning">After enabling log audit, you are billed for TLS based on your usage. For details about TLS charges, see <a href="https://docs.byteplus.com/en/docs/tls/billable_items">product billing</a>.</div>


* <div data-tips="true" data-tips-type="warning">You cannot delete, edit, or configure indexes for created resources (log project and topic) specific to CR audit logs in the TLS console. To delete created resources specific to CR audit logs in the TLS console and stop the associated billing, use the <strong>Close associated logs</strong> feature in the CR console.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the[ CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance in the **List of instances** area, and click **Enter instance**.

2. On the instance page, in the left navigation bar, click **audit log**.

3. On the **Audit log** page, click **Get started with audit log**.

4. On the secondary confirmation page, click **Confirm** to complete the operation.


<span id=".5ZCO57ut5pON5L2c"></span>
## FAQ

<span id="S738mnPa"></span>
### Error QuotaExceeded.TLS.Project occurs during the audit log enabling

When the error `QuotaExceeded.TLS.Project` occurs when log audit is being enabled, this indicates that the **TLS\-side quota** has been reached. Clean up projects or apply for the project quota. Enable the audit log service again after you obtain the TLS project creation quota. To apply for the TLS project quota, see [Applying for resource quota](https://docs.byteplus.com/en/docs/tls/Apply_for_resource_quota).
