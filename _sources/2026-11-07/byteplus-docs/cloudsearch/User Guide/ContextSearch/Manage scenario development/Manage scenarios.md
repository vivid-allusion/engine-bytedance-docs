---
title: "Manage scenarios"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Manage_scenarios"
---

After creating a scenario, you can manage it by starting, editing, or deleting the scenario. This article explains how to manage scenarios.

<span id="SwlkuH9P"></span>
## Prerequisites

Scenario created. For detailed steps, see [Quickly create and use scenarios](https://docs.byteplus.com/en/docs/cloudsearch/Quickly_create_and_use_scenarios) and [Create a scenario](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_scenario).

<span id="MFEmNxyg"></span>
## Start a scenario

After creating and completing scenario development, you can start the scenario.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The scenario to be started must be published and in the <strong>Stopped</strong> state.</div>



1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. On the top navigation bar, select the target project and region.

3. In the left navigation bar, select **ContextSearch \> My Scene**, find the target scene card, then select  **... \> Start scene** in the card.


<span id="iriSdvtT"></span>
## Edit a scenario

After creating a scene, you can edit the scene information.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only the scene name and description can be modified.</div>



1. Log in to the[Cloud Search console](https://console.byteplus.com/es).

2. On the top navigation bar, select the target project and region.

3. In the left navigation bar, select **ContextSearch \> My Scene**, find the target scene card, then select  **... \> Edit scene** in the card.

4. In the **Edit scene** panel, configure the following parameters, then click **Save**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Set the name of the knowledge base scenario. Naming rules are as follows:<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Length must be between 1 and 128 characters.<br><br>* Contain letters, digits, underscores (_), and hyphens (\-). |
   |Description (optional) |Set the description of the knowledge base scenario. Length must not exceed 255 characters. |
   


<span id="lBE5P138"></span>
## Stop a scenario

If you do not need to use a scene temporarily, you can stop the scene.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The scene to be stopped must be in <strong>Running</strong> or <strong>Starting</strong> status.</div>


* <div data-tips="true" data-tips-type="default">The scene becomes unavailable after stopping. Restart it if you need to use it again.</div>


1. Log in to the[Cloud Search console](https://console.byteplus.com/es).

2. On the top navigation bar, select the target project and region.

3. In the left navigation bar, select **ContextSearch \> My Scene**, find the target scene card, then select  **... \> Stop scenario** in the card.

4. In the popup dialog, click **OK**.


<span id="lBE5P138"></span>
## Delete scene

If you no longer need a scene, delete it to save resources.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Running scenes must be stopped before deletion.</div>


* <div data-tips="true" data-tips-type="warning">Scenes cannot be recovered after deletion. Proceed with caution.</div>


1. Log in to the[Cloud Search console](https://console.byteplus.com/es).

2. On the top navigation bar, select the target project and region.

3. In the left navigation bar, select **ContextSearch \> My Scene**, find the target scene card, and then select  **... \> Delete scene** on the card.

4. In the popup dialog, click **OK**.
