---
title: "Scheduling history"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Scheduling_history"
---

Each time an application is orchestrated, a new orchestration history ID is generated, which uniquely identifies the current orchestration version. This article introduces actions related to orchestration history.

<span id=".5p-l55yL57yW5o6S54mI5pys"></span>
## View the orchestrated version

View all orchestration versions and compare their differences and similarities.


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp). From the left navigation bar, select **Workspace**.

2. Click the target workspace name, and in the left navigation bar of the current workspace, select **Application Delivery \> Application Management**.

3. Click the target application card to open the application. Click **Application Orchestration** and go to the Application Orchestration tab.

4. Click **Orchestration History** in the upper right corner to open the Orchestration History table.

   You can view all orchestration records, including the environment where each record takes effect, the description, the modifier, and additional details.

5. In the table, select the version you want to view, and click **Arrangement History ID** to go to the details page for the arrangement record of the current version.


<span id=".6K6-572u55Sf5pWI546v5aKD"></span>
## Set the effective environment

Set the environment where the orchestration version takes effect.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An orchestration version can be effective in multiple environments, but each environment can have only one effective orchestration version. After updating the orchestration version of the current environment, previous orchestration versions will become invalid.</div>



1. In the orchestration history table, select the orchestration version for which you need to set the effective environment, and click the settings icon in the effective environment column.

2. In the pop\-up dialog box, check the environment instances that you want to take effect. Supports multiple selection.

3. Click **OK**. The system will display the number of environments where the current orchestration version is effective.
