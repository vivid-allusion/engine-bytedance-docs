---
title: "Billing items and prices"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/charge_items_and_price"
---

This topic introduces billing items and price details for RDS for PostgreSQL.

<span id=".6K6h6LS56aG5"></span>
## Billing items

Billing items for RDS for PostgreSQL include instance specification fees and storage space fees.


|Billing items |Note |
|---|---|
|Primary and secondary node specification |Cost of PostgreSQL primary, secondary, or Read\-only node specification. The billing method is subscription or pay\-as\-you\-go. |
|Storage space |Cost for PostgreSQL instance storage space. Billing methods include subscription or Pay\-as\-you\-go. |
|Backup storage space (optional) |Cost for the space occupied by backup files. Backup storage space has a 0% discount and incurs no cost. |
|Public network traffic (optional) |PostgreSQL supports applying for a public network address and accessing the instance using the public network address. The public network address will bind a [public network IP](https://docs.byteplus.com/en/docs/eip/What-is-EIP) (Elastic IP Address, abbreviated as EIP). Using EIP incurs charges. For more information about public IP billing, see [Public IP Billing Overview](https://docs.byteplus.com/en/docs/eip/Billing-overview). |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information on billing method, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/price_overview">Overview</a>.</div>


<span id=".5Lu35qC86K6h566X5pa55byP"></span>
## Price calculation method

PostgreSQL local disk type instances use a high\-availability architecture, supporting one primary, one secondary, and up to ten read\-only nodes. Charges are based on node specification and storage space.


* Subscription

   One\-time prepaid price = (node specification unit price + storage space unit price × storage space size) × number of nodes × number of months

* Pay\-as\-you\-go

   Hourly postpaid price = (node specification unit price + storage space unit price × storage space size) × number of nodes


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on price calculation, refer to <a href="https://www.byteplus.com/en/pricing?product=RDS+for+PostgreSQL&tab=2">PostgreSQL price calculator</a>.</div>


<span id=".6LSt5Lmw56S65L6L"></span>
## Purchase example


* **Subscription**

   * **Usage scenario**:

      Purchase a high\-availability edition instance with a 4C16G node specification and 500GB storage space (including one primary and one secondary node) for a duration of 1 year.

   * **Total annual cost (excluding participation in 1\-year discount promotions)** :

      (USD 720.00/month + 500GB × USD 0.60/GB/month) × 2 (number of nodes) × 12 months = USD 24480.00

* **Pay\-as\-you\-go**

   * **Use case**:

      purchase a High\-availability Edition instance with a 4C16G node specification and 500GB storage space (including primary and secondary nodes), billed on a pay\-as\-you\-go basis.

   * **Cost per hour**: (USD 1.50/hour + 500GB × USD 0.00125/GB/hour) × 2 (number of nodes) × 1 hour = USD 4.25

   * **Annual cost**: USD 4.25/hour × 8760 hours = USD 37230.00
