---
title: "Announcement on the Deactivation of the Public Network Resolution Function"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Announcement_on_the_Deactivation_of_the_Public_Network_Resolution_Function"
---

To provide you with more reliable and stable services, we plan to deactivate the public network resolution function of RDS for PostgreSQL.

<span id="O5EGCHgP"></span>
## Background

To meet the business needs of enterprise users to build a private network for local resources and BytePlus’s cloud resources, RDS for PostgreSQL launched the public network resolution function in June 2023. Through the public network resolution function, you can connect to the instance's private domain name via DNS resolution in a public network environment, enabling local resources to access BytePlus cloud resources.

<span id="inEU5AyB"></span>
## Reason for deactivation

Due to the iteration of the technical architecture, this function will no longer be provided.

<span id="8JxAWvgJ"></span>
## Deactivation plan

Starting from October 31, 2025, RDS for PostgreSQL will no longer provide the public network resolution function. Instances that have enabled the public network resolution function before October 31, 2025, can continue to use this function normally, but once disabled, it cannot be enabled again.

The Open API for enabling and disabling Public network resolution — ModifyDBEndpointDNS — will also simultaneously discontinue the capability to enable Public network resolution, supporting only the disabling of Public network resolution.
