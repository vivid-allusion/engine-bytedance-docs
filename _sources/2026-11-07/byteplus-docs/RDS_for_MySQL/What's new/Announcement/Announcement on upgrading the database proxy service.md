---
title: "Announcement on upgrading the database proxy service"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Announcement_on_upgrading_the_database_proxy_service"
---

To meet the need to improve the performance of the database proxy service, we will upgrade the instances of the database proxy service that are in the basic state.

<span id="fZoVYlXj"></span>
## Background

Billing for the database proxy service for RDS for MySQL started at 00:00:00 (UTC+8) on November 20, 2024. Instances that had the database proxy service enabled before billing started, and have not since been disabled and re\-enabled, are still in a free, basic state. The proxy configuration for these instances cannot be modified, preventing them from obtaining a higher\-performance database proxy service.

<span id="OJcAnipo"></span>
## Upgrade details

Instances with the database proxy service in a basic state are upgraded to provide the ability to change the proxy configuration for the instances.

<span id="K981sMOj"></span>
## Upgrade time

Upgrades will be rolled out by region, starting from April 7, 2026.

<span id="wxsImvmY"></span>
## Business impact and response


* **Scope of impact**

   All instances where the database proxy service was enabled before 00:00:00 on November 20, 2024 (UTC+8) and has not since been disabled and re\-enabled.Enabled

* **Business impact**

   This upgrade does not affect the running of instances.

* **Solutions**

   Not involved.


<span id="cfKnKFRI"></span>
## Next steps

None. If you have any questions or need further support during use, you can contact our customer support team at any time.
