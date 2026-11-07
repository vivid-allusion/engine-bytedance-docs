---
title: "Manage Inbound Endpoints"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Manage_Inbound_Endpoints"
---

This document describes how to create, update, or delete inbound endpoints.

<span id="create-an-inbound-endpoint"></span>
## Create an inbound endpoint

Follow these steps to add an inbound endpoint.


1. Open the [Resolver](https://console.byteplus.com/dns-suite/privatezone/resolver) page. Select the **Inbound endpoint** tab.

2. Click **Create inbound endpoint**. On the **Create inbound endpoint** page, configure the parameters for the inbound endpoint. See [Step 3: Create an inbound endpoint](https://docs.byteplus.com/docs/byteplus-dns-suite/EddkeA).

3. After configuring the parameters, click **OK**.


After adding, it takes about 30 seconds for the inbound endpoint to be fully created.

<span id="update-an-inbound-endpoint"></span>
## Update an inbound endpoint

Follow these steps to update an inbound endpoint.


1. Open the [Resolver](https://console.byteplus.com/dns-suite/privatezone/resolver) page. Select the **Inbound endpoint** tab.

2. Find the inbound endpoint you want to update. Click **Edit** in the **Actions** column.

3. On the **Edit inbound endpoint** page, update the parameters of the inbound endpoint. See [Step 3: Create an inbound endpoint](https://docs.byteplus.com/docs/byteplus-dns-suite/EddkeA).

4. After updating the parameters, click **OK**.


<span id="delete-an-inbound-endpoint"></span>
## Delete an inbound endpoint

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Before deleting an inbound endpoint, you need to confirm that the rules of external DNS servers are no longer using this inbound endpoint. If an inbound endpoint is deleted, but it is still included in the rules of external DNS servers, the forwarding of DNS queries will fail.</div>


Follow these steps to delete an inbound endpoint.


1. Open the [Resolver](https://console.byteplus.com/dns-suite/privatezone/resolver) page. Select the **Inbound endpoint** tab.

2. Find the inbound endpoint you want to delete. Click **Delete** in the **Actions** column. Click **OK** in the pop\-up window.
