---
title: "Flow Log FAQ"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Flow-log-FAQ"
---

## How are flow logs billed?

At the VPC level, only VPC Flow Logs generation fees apply. The Virtual Private Cloud (VPC) delivers VPC Flow Logs data to the Torch Log Service (TLS) for storage, retrieval, and analysis. TLS will charge relevant fees for these operations. For details, refer to [Billing notes for Flow Logs](https://docs.byteplus.com/en/docs/vpc/Flow-log-billing).

## How many flow logs can a single account create?

A single account can create up to 10 flow logs per region.

## Do flow logs support recording IPv6 traffic?

Yes, supported.

## Why did flow log creation fail?

Possible causes:

|Cause |Description |
|---|---|
|Exceeded quota limits |Reached the maximum number of flow logs allowed under your main account. For more details, see [Limits](https://docs.byteplus.com/en/docs/vpc/Limits#HX6RRU8r). |
|Log project name conflict |Flow log creation fails if the name you entered for the new log project duplicates an existing log project name under your main account. Recreate the flow log and ensure the new log project name is unique. To delete flow logs that failed to create, [submit a ticket](https://console.byteplus.com/workorder/create/). |

##
