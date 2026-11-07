---
title: "Using memory service"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Using_memory_service"
---

This topic introduces information on using the memory service.

## Prerequisites

* A workspace using the Supabase engine is created, and its status is **Running**.

* The memory service status of the target branch is available.

## Precautions

* The memory service function is currently in whitelist mode. If you need to use, [submit a ticket](https://console.byteplus.com/workorder/create) to apply.

* The memory service is only available in workspaces using the Supabase engine.

* Ordinary newly created branches do not inherit memory from the parent branch.

* The initial version does not support importing, exporting, or cross\-branch copying of memory.

* Memory by default does not expire and has no quantity limit. If no longer needed, delete it actively.

* Deleting a business user does not automatically clear the user’s memory; it must be deleted separately.

## User guide

Select a branch in the target workspace, then enter the **User guide** tab of the memory service. The page provides the following operation instructions:

1. Add memory: submit content pending processing and associate User ID, Agent ID, or Run ID according to the business scenario.

2. Search memory: input search content and search relevant memory within the user or agent scope.

3. Get memory: view detailed content of specified memory by memory identifier.

4. Update memory: modify the content of the specified memory.

5. Delete memory: remove the specified memory that is no longer needed.

## Configure memory extraction strategy

Enter the **Configuration management** tab to view and manage memory extraction strategies. Strategies are divided into system strategies and custom strategies.

|**strategy source** |**Tip** |
|---|---|
|system strategy |Built\-in memory extraction strategies in the platform, available for direct viewing and use. |
|custom strategy |Configure extraction rules based on business needs. Custom strategy types include summary, semantic, user preference, and event categories. |

When configuring a custom strategy, select the strategy type based on the business semantics of the information to be extracted, and fill in the strategy name, description, prompt words, and other configurations.

## Search memory

Enter the **Memory search** tab, set the following search criteria, and initiate the search.

|**Field** |**Is it required?**  |**Tip** |
|---|---|---|
|Memory content |Yes |Enter the content to search. |
|User ID |Condition required |Select either Run ID or Agent ID to limit the user scope. |
|Agent ID |Condition required |Either with user ID to limit the Agent scope. |
|TopK |No |Set the number of related memories to return. |
|Run ID |No |Further filter by running identifier. |
|Policy |No |Filter by memory extraction strategy. |
|Creation time |No |Filter by memory creation time. |

Memory content is required; User ID and Agent ID must be selected as the search scope exclusively.
