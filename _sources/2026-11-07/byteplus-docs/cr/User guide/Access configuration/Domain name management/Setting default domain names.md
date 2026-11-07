---
title: "Setting default domain names"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Set_the_default_domain_name"
---

CR allows you to change the default domain name from the system domain name to a custom domain name. This helps reduce the workload of modifying domain names in relevant business code.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the custom domain name specified as the default domain name is deleted, the default domain name is automatically updated to the system domain name.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A custom domain name has been created. For operation details, see [Creating custom domain names](https://docs.byteplus.com/en/docs/cr/Create_a_custom_domain_name).

* Only BytePlus root users or IAM users granted full read/write permissions for CR (the CRFullAccess policy) can create custom domain names. For information about how to grant full read/write permissions for CR to an IAM user, see [Authorizing IAM users](https://docs.byteplus.com/en/docs/cr/authorize-iam-users).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **list of instances**and select the entry according to the instance type:

      * Standard instance: Click **standard instance**, find the target instance, and click **enter instance**.

      * Proxy repository: Click **proxy repository**, and click the target domain name to enter the instance details page.

2. In the left navigation bar, click **Domain name management**.

3. On the **Domain name management** page, click the Edit icon.

4. Select the created custom domain name.

5. Click **confirm** to complete the operation.
