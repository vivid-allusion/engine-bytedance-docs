---
title: "Exporting lists"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/exporting-lists"
---

You can use the credential list export feature to export basic information about all credentials in the current account to a JSON file. The exported information can be used for credential inventory, security audits, usage verification, and historical configuration records.

> **tip**

> The exported file contains only credential management information. It does not contain sensitive values such as API Key, Client Secret, Access Token, or Refresh Token.

## Procedure

1. Log in to[ the AgentKit console](https://console.byteplus.com/agentkit).

2. In the left navigation pane, select "Identity and Permission ** \>**  Credential management".

3. At the top of the page, click "Export list".

4. After the export is complete, open the `credentials.json `file locally. Verify fields such as credential name, type, provider, association status, creation time, and update time to confirm that the content is as expected.

   > **tip**

   > Securely store the exported file or delete it promptly to prevent credential names, resource identifiers, association relationships, and other information from being disclosed.
