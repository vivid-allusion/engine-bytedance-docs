---
title: "Export report"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Export_report"
---

Support downloading specified domain and module data reports on the security overview page as needed, with a maximum export of overview data reports from the last month. The exported report is in offline HTML format and can be used to store historical data and generate security protection reports.

<span id="77ad242f"></span>
## Notes

The WAF security overview page currently does not support exporting charts added to the custom dashboard; you can go to [Log Service Console](https://console.byteplus.com/tls/)\>Download specified chart information from the ** dashboard**.

<span id="ad589352"></span>
## Requirements

You have connected the website that needs to be protected to the WAF instance. For access\-related operations, please refer to [Comparison of website association methods](https://docs.byteplus.com/en/docs/6511/935149).

<span id="319a7873"></span>
## Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. Select **Security Overview** on the left navigation.

4. Click the download icon.

5. Select time, domain, and module.

   * Time: Support exporting report data for up to the last month.

   * Domain: By default, **All Domain Overview** is checked.

      * All Domain Overview: Download aggregated data reports for all domains.

      * Check one or more domains: Download reports for one or more domains, with each domain corresponding to one data report.

   * Module: This refers to the data paginated report on the Security Overview page, with all checked by default, allowing you to choose to view data from only certain reports.

6. Click **Export**.

   The exported file is in offline HTML format for local data storage and offline browsing.
