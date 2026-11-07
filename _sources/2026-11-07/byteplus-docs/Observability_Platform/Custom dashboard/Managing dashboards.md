---
title: "Managing dashboards"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Managing_dashboards"
---

This topic describes dashboard lifecycle management and other supported operations.


1. Log in to the [Observability Platform ](https://console.byteplus.com/observe/dashboard/dashboard)console, and in the left navigation bar, select **Custom Dashboard**.

2. On the dashboard management page, create new dashboards or manage existing dashboards.

3. Click the name of the target dashboard to view the dashboard. You can customize the data time range and refresh frequency. You can also export or edit the dashboard.

4. Click the **edit ** button in the upper\-right corner to enter edit mode. In this mode, you can modify the basic information of a dashboard, set global variables, and manage panels and groups. After all editing configurations are complete, click **save** and **Quit editing** in sequence.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The system generates a new version record based on the current changes. For details, see <a href="https://docs.byteplus.com/en/docs/Observability_Platform/Version_management?TagIDs=2,405&lang=en">Version management</a>.   </div>
   

   
   |Actions |Description |
   |---|---|
   |Create dashboard |Create a dashboard with a custom name. Three creation methods are currently supported: direct creation, import from JSON, and copying a dashboard. |
   |Move dashboard |Move the target dashboard to another folder. |
   |Copy dashboard |Quickly create a new dashboard based on an existing one. This applies to scenarios where you need to create dashboards quickly within the same platform. |
   |Delete dashboard |Delete dashboards that are no longer needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deleting a dashboard will also remove all related configurations. This action cannot be undone. Proceed with caution.</div><br> |
   |View dashboard |After all configurations are complete, return to the dashboard page to view dashboard data. You can customize the time range and refresh frequency, or manually refresh the data. |
   |Export as JSON file |Export the dashboard as a JSON file. You can use this file to quickly recreate a dashboard on the current platform or on Grafana. Applicable scenarios cover cross\-platform migration or quickly replicating a dashboard from Grafana. The currently supported export formats include Observability JSON and Grafana JSON. |
   |Edit dashboard |Enter dashboard edit mode to modify dashboard information or reorganize its content. This includes: editing basic information such as name and description, setting global variables, viewing the JSON model, adding charts, arranging chart layout, and adding groups. |
