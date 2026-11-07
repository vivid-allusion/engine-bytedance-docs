---
title: "Managing custom domain names"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Manage_custom_domain_names"
---

This topic describes how to manage custom domain names.

<span id=".5p-l55yL6Kej5p6Q6YWN572u"></span>
## View resolution configuration

You can navigate to TrafficRoute to view resolution records by clicking **Resolution configuration**.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Domain name management**. On the **Domain name management** page, click **Resolution configuration** in the **Actions** column of the target domain name.

3. On the [DNS Domain management page](https://console.byteplus.com/TrafficRoute/dns/publiczone/zones) or [PrivateZone Domain management page](https://console.byteplus.com/TrafficRoute/dns/privatezone/zones) of TrafficRoute, view the corresponding resolution records.


<span id=".5pu05paw6Ieq5a6a5LmJ5Z-f5ZCN"></span>
## Update a custom domain name


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Domain name management**. On the **Domain name management** page, click **Modify** in the **Actions** column of the target domain name.

3. On the **Modify custom domain name** page, update the certificate and Referrer.

4. After the update is complete, click **Check and submit**.


<span id=".5Yig6Zmk6Ieq5a6a5LmJ5Z-f5ZCN"></span>
## Delete a custom domain name


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Domain name management**. On the **Domain name management** page, click **Delete** in the **Actions** column of the target domain name.

3. On the secondary confirmation page, click **Delete**.


<span id=".QVBJIOaWh-ahow=="></span>
## API Documentation

[ListDomains](https://docs.byteplus.com/en/docs/cr/ListDomains): Queries the domain names of a Container Registry instance.
