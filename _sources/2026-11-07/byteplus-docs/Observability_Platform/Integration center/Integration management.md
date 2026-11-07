---
title: "Integration management"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Integration_management"
---

After creating an integration task, you can go to the Integration management page to view and manage the task. This topic uses a Go integration task as an example to describe how to view and manage integration tasks.

<span id="3cPsqphb"></span>
## Prerequisites

An integration task has been created. For an example of how to create an integration task, see [Integrating server-side applications in VKE](https://docs.byteplus.com/en/docs/Observability_Platform/Integrating_server-side_applications_in_VKE) or [Integrating server-side applications in a third-party cloud](https://docs.byteplus.com/en/docs/Observability_Platform/Integrating_server-side_applications_from_third-party_clouds).

<span id="BUsLm0Sz"></span>
## View an integration task

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">The categories on the Integration management home page are identical to those in the Integration marketplace, but the Integration management home page displays the cards for existing integration tasks only. This topic uses a Go integration task as an example.</div>


1. Log in to the [Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard).

2. In the left navigation pane, select **Integration center \-\> Integration management**.

3. Select the **Backend Application** category and **Go** in sequence to go to the management page for Go integration tasks.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can check the health of an integration task by its status. "Running" indicates that the integration task is operating normally; "Exception" indicates that the integration task has failed, and you can view the specific cause in the "Exception cause" column.   </div>
   

<span id="Stej0JMH"></span>
## Manage integration tasks

On the integration task management page, click a button in the "Actions" column to the right of the target integration task to perform the corresponding operation.


|Actions |Description |
|---|---|
|Edit |Edit the integration task configuration, including the task name and custom Pod filtering rules.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the Pod filtering rules are updated, make sure to go to the<a href="https://console.byteplus.com/vke"> VKE console</a> and, on the workload management page of the target container cluster, redeploy the workload that corresponds to the application to be integrated.</div><br> |
|Stop/start |Stop or start integration tasks.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Stopping an integration task also stops data collection for the associated service, which affects data monitoring and may affect normal business operations. Proceed with caution.</div><br> |
|Delete |Delete integration tasks that are no longer needed.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><br>* <div data-tips="true" data-tips-type="danger">Deleted integration tasks cannot be recovered. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">Deleting an integration task also stops data collection for the associated service, which affects data monitoring and may affect normal business operations. Proceed with caution.</div><br> |
