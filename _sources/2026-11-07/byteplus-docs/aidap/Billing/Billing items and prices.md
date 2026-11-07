---
title: "Billing items and prices"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Billing_items_and_prices"
---

AI Native BaaS for Supabase relies on the AI Native Database Platform (AIDAP) and provides services through three database engines: Supabase, PostgreSQL, and veDB MySQL. This topic introduces the billing items and prices of the AI Native Database Platform.

Billing items vary for workspaces using different engines, as shown in the table below.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">veDB MySQL engine is currently in beta testing and free of charge. Billing items and prices for veDB MySQL engine are not explained at this time.</div>



|**Engine type** |**Billing items** |**Decscription** |**Billing unit** |**Price** |
|---|---|---|---|---|
|PostgreSQL Engine |Compute |Cost for workspace compute resources, billed in CU. 1 CU is equivalent to compute resources with 1 core CPU and 4 GiB of memory. |USD/CU/Hour |0.108538 |
||Storage space |Workspace data storage cost. |USD/GiB/Hour |0.000271 |
|Supabase Engine<br><br> |Database compute |Cost for workspace compute resources, billed in CU. 1 CU is equivalent to compute resources with 1 core CPU and 4 GiB of memory. |USD/CU/Hour |0.108538<br><br> |
||Database storage capacity |Workspace data storage cost. |USD/GiB/Hour |0.000271 |
||Object storage capacity |The cost of object storage capacity used by the Supabase service. |USD/GiB/Hour |0.000072 |
||Edge Function execution count |Cost incurred by the Supabase service calling Edge Function. |USD/10,000 times |0.030391 |
||Supabase common component compute |The cost of computing resources for the Supabase service common components. |USD/CU/Hour |0.108538 |
||Storage vector bucket capacity |The storage space occupied by vector data stored in the vector bucket, used to measure your actual storage resources used. |USD/Hour/GiB |0.00018 |
||Storage vector bucket data query |Query resources consumed when performing read operations such as search and query on vector data in the vector bucket, used to measure resource usage caused by query requests. |USD/Hour/vCU |0.00009 |
||Storage vector bucket data update |Resource usage consumed when writing, updating, or deleting vector data in the vector bucket, used to measure resource usage caused by data modification operations. |USD/Hour/vCU |0.00002 |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can bind an <a href="https://docs.byteplus.com/en/docs/eip/What-is-EIP">Elastic IP Address</a> (EIP) to workspaces using the Supabase engine to enable access to the Workspace over the public network. The use of EIP incurs charges, which are billed by EIP. For more information about EIP billing, see <a href="https://docs.byteplus.com/en/docs/eip/Billing-overview">EIP billing overview</a>.</div>
