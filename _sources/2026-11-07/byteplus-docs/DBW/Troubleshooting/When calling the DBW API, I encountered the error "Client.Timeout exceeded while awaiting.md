---
title: "When calling the DBW API, I encountered the error \"Client.Timeout exceeded while awaiting headers.\" What should I do?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Client_Timeout"
---

**Possible Causes**

When Database Workshop (DBW) calls the API of the RDS for MySQL instance, it uses the API of RDS for MySQL v2, which is not compatible with the allowlist of v1. This causes the allowlist addition to fail, resulting in a timeout.

**Solution**

You can manually add the client's IP address or address range to the whitelist in the RDS for MySQL console. For detailed steps, refer to [Create allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_allowlist_1) and [Bind instance to allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_instances_to_allowlists).
