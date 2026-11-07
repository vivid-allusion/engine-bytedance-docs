---
title: "The observation deployment process"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/The_observation_deployment_process"
---

During application deployment, the system will automatically navigate to the current environment's **Change Record** tab to display the details of this deployment. 


|Feature |Descriptions |
|---|---|
|Basic Information |Display information about the current deployment environment, the deploy resource(s) being used, and other relevant details. |
|Summary |Displays basic information about the current deployment task, such as deployment record ID, trigger source, orchestration record, associated configuration, operator, time, and other details.<br><br><br>* Click the details link of the orchestration record to view the application orchestration details used in this deployment.<br><br>* Click the version link associated with the configuration to view the environment configuration details used for this deployment. |
|Progress |Displays the deployment progress of the current application in real time.<br><br><br>* For K8s YAML applications, only single\-component, single\-stage deployment is supported, and the deployment progress is displayed directly. |
|Details |Select the target component and click **details** in the actions column to view deployment details for the current component, including the resources contained in the component and their YAML configurations. For Deployment resources, the deployment details area displays information about new and old version Pods, and allows you to view real\-time Pod logs to monitor the running status of each Pod. |
|Continue |* For multi\-stage deployment, after each stage is deployed, you must manually click **Continue** to trigger deployment of the next stage.<br><br>* When using the Deployment batch release strategy, within the same deployment stage, after each batch is successfully deployed, you must manually click **Continue** to trigger the deployment of the next batch. As shown in the figure: In deployment stage one, both components show that batch 1 has been successfully deployed, while batch 2 is pending. You need to click **Continue deployment** in the upper right corner to start deploying batch 2. |
|Cancel |You can click **Cancel** at any time during the deployment process to immediately revert the environment to its state before this deployment. Applicable in scenarios where the current deployment version is not functioning as expected and a quick restoration of the environment to its last known good state is required. |
