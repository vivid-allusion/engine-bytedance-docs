---
title: "Deleting skills spaces"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Deleting_Skills_spaces"
---

You can delete unused skills spaces. After deletion, the association between this space and skills will be synchronously removed.

> **warning**

> **Deleted skills spaces cannot be restored**. If any **agent** relies on this space to search for or call skills, deleting it may make related capabilities unavailable or cause the **agent** to fail during operation. Before deleting any space, we recommend confirming its usage status and removing related business dependencies.

## Prerequisites

You have confirmed that the target skills space is not used by **agents** or other businesses.

## Procedure

1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the left\-side navigation pane, select "Skills".

3. Select the "Skills spaces" tab. In the "Actions" column of the target skills space, click the "Delete" button.

4. After you confirm that the space to be deleted is correct, click the "Delete" button to complete the operation.
