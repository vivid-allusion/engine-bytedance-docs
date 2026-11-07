---
title: "Overview"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/billing_Overview"
---

AI Native BaaS for Supabase relies on the AI Native Database Platform (AIDAP) and provides services through  two database engines: Supabase, PostgreSQL.  This topic introduces the billing types and workspace lifecycle information supported by the AI Native Database Platform.

<span id="02Y6xZyB"></span>
## Billing method

The AI Native Database Platform is a database service with second\-level elasticity. Both its data storage space and compute are billed based on usage, following a pay\-as\-you\-go billing method.

Under the pay\-as\-you\-go billing method, a billing order is generated every hour, and fees are deducted from the BytePlus account based on the specifications at the time the order is generated.

<span id="GlhWUCEE"></span>
### Purchase requirements


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).


<span id="NnmaPvvu"></span>
### Billing duration

Under the pay\-as\-you\-go billing method, the billing duration covers the workspace's entire lifecycle. Billing starts when the workspace creation is complete and ends when related workspace resources are fully released.

<span id="fyvUGP5G"></span>
### Payment cycle

Expenses are settled on the hour (in UTC+8 time), followed by the next payment cycle. If your available account balance (including account balance and cash coupons) is less than the bill to be settled, you will receive an SMS or email notification about insufficient balance.

<span id="7kBZuFtW"></span>
### Configuration change pricing

Under the pay\-as\-you\-go billing method, instances are billed on an hourly basis, with charges based on actual usage.

<span id="IOd7MxII"></span>
## Workspace lifecycle

Under the pay\-as\-you\-go billing method, the workspace lifecycle starts upon successful creation and stops when the workspace is released. Release can be either initiated by the user or triggered by a forced shutdown due to account arrears.
