---
title: "Observability diagnosis"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Observability_diagnosis_agentkit"
---

Observability diagnosis allows you to manage diagnosis tasks for all sessions in AgentKit. This topic describes how to view diagnosis reports and manage diagnosis tasks.

<span id="fl8ZSnwM"></span>
## Prerequisites

A session diagnosis has been triggered, for example, the session diagnosis described in [AgentKit Session analysis](https://docs.byteplus.com/en/docs/Observability_Platform/Session_analysis).

<span id="yyXJxLs0"></span>
## View the diagnosis report


1. Log in to [the AI application monitoring console](https://console.byteplus.com/observe/apmplus-server/region:apmplus-server+cn-beijing/server/trace/llmanalysis), and select the project and region in the top menu bar. 

2. In the left navigation bar, select **AgentKit Application Observability**. 

3. Select the ** Observability and Diagnostics ** tab. In the Actions column to the right of the target diagnosis task, click **View report** to view the diagnosis report details. The report includes the AI comprehensive diagnosis conclusion, core metric statistics, identified issues, optimization suggestions, and details such as the issue severity, symptom, action, and expected result.

   * Diagnosis tasks support three task statuses: **Running** indicates the diagnosis task is in progress; **Finished** indicates the diagnosis is finished and the report is generated normally; **Failed** indicates the diagnosis task failed and was aborted. You can click the red warning tip on the right side of "Failed" to view the failure cause.

   * Diagnosis reports support four health levels: **OK** indicates that no exceptions were found during diagnosis. **Warning** indicates that potential risks were identified. **Critical** indicates that exceptions were found. We recommend that you resolve the exceptions immediately. **Unknown** indicates an unknown state, usually caused by a diagnosis or report generation failure.


<span id="TroIkOyG"></span>
## Manage diagnosis tasks

To delete a diagnosis task and the corresponding diagnosis report, click **Delete** in the Actions column of the target task.
