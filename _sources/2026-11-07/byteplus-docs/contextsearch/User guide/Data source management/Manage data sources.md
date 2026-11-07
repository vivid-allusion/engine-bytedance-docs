---
title: "Manage data sources"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Manage_data_sources_new"
---

After adding a data source, you can manage it, including viewing, editing, and deleting the data source. This topic describes how to manage data sources.

## Prerequisites

Added a data source. For more information, see [Add a data source](https://docs.byteplus.com/en/docs/contextsearch/Add_a_data_source_new).

## View data source

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **Data source** in the left navigation bar to view added data sources. Support searching data sources by name or filtering data sources by type.

## Edit data source

> **tip**

> When editing a data source, only modify Instance information if the data source type is Volcengine database; only modify Feishu Application information if the data source type is Feishu Documentation.

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **Data source** from the left navigation bar, then click **Edit** on the target data source card.

4. In the **Edit data source** panel, modify the data source description as needed, then click **OK**.

## Delete data source

> **warning**

* > Cannot delete data source when it is referenced by a scene. Disassociate the scene referencing this data source before deleting the data source. For more information, see [Scenario management](https://docs.byteplus.com/en/docs/contextsearch/Manage_scenario_development).

* > Data sources cannot be recovered once deleted; proceed with caution.

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **data synchronization** in the left navigation bar, then click **Delete** on the target data source card.

4. In the popup dialog, click **OK**.
