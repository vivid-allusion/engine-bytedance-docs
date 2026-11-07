---
title: "Manage allowlist entries"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/Manage_allowlist_entries"
---

After a Vortex IP instance in Internet mode is created, it defaults that any Internet client can access the Vortex IP. You can add allowlist entries based on your business requirements to control CIDR blocks for inbound access IPs. The configuration takes effect upon completion.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* Only **active** instances support adding/deleting allowlist entries.

* You can add up to **20** allowlist entries for a single Vortex IP in Internet access mode. If you need to increase the quota, please contact your account manager.


<span id=".5pON5L2c5q2l6aqk"></span>
## Add an allowlist entry


1. Log in to [the Vortex IP console](https://console.byteplus.com/eip/region:eip+ap-southeast-1/vortexips).

2. In the top menu bar, select your target region.

3. In the Vortex IP list, click  **··· \> Configure allowlist** in the Actions column to the right of the target Vortex IP instance in Internet access mode.

4. Click **Add allowlist**.

5. Type in the source address and description.

6. Click **OK** to complete the action.


<span id=".5pON5L2c5q2l6aqk"></span>
## Delete an allowlist entry

You can no longer use the Vortex IP service through this IP CIDR block upon deletion. Proceed with caution.


1. Log in to [the Vortex IP console](https://console.byteplus.com/eip/region:eip+ap-southeast-1/vortexips).

2. In the top menu bar, select your target region.

3. In the Vortex IP list, click  **··· \> Configure allowlist** in the Actions column to the right of the target Vortex IP instance in Internet access mode.

4. Click **Delete** in the Actions column to the right of the target source address.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [AddVortexIPWhiteListEntries](https://docs.byteplus.com/en/docs/gavi-sept-test1/AddVortexIPWhiteListEntries): Add allowlist entries for a Vortex IP in Internet mode.

* [RemoveVortexIPWhiteListEntries](https://docs.byteplus.com/en/docs/gavi-sept-test1/RemoveVortexIPWhiteListEntries): Delete allowlist entries for a Vortex IP in Internet mode.
