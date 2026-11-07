---
title: "Viewing all IP addresses associated with the instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Viewing_all_IP_addresses_associated_with_the_instance"
---

This topic describes the procedure to view all IP addresses associated with an RDS for MySQL instance.

<span id="XagXvSpf"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the target instance name.

5. Click the **Security** tab at the top of the page.

6. Under the **Allowlists** sub\-tab, click **View all IPs** in the upper\-right corner of the page. 

7. In the pop\-up **All IPs** page, you can view all the IPs the instances associated with in two methods: **View by allowlist** and **View after merging and deduplication**.

   * Under **View by allowlist**, all allowlists of the instance associates and corresponding IP addresses and IP address segments are displayed. Click the Modify or Copy button of each allowlist to quickly open the edit page of the corresponding allowlist, or copy the IP addresses and IP address segments contained in the corresponding allowlist.

   * Under **View after merging and deduplication**, the collection of all IP addresses and IP address segments in the allowlist to which the instance is associated is deduplicated. However, if an IP address is contained in an IP address segment, both the IP address and the IP address segment will be displayed simultaneously. Click the Copy button on the page to copy all the deduplicated IP addresses and IP address segments.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Under <strong>View by allowlist</strong>, the built\-in allowlist of the system that MySQL instances are added by using the session management function provided by the Database Workshop (DBW) or the Database Transfer Service (DTS) will also be listed, but the system allowlist only supports copying the IP addresses and IP address segments it contains, and does not support editing.   </div>
