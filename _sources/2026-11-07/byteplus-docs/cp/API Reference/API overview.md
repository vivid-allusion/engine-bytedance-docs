---
title: "API overview"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/API_list"
---

This document provides a detailed list of all APIs for the CP Product.

## Workspace

|API |Description |
|---|---|
|[CreateWorkspace](https://docs.byteplus.com/docs/cp/CreateWorkspace) |Create a workspace. |
|[UpdateWorkspace](https://docs.byteplus.com/docs/cp/UpdateWorkspace) |Update a workspace. |
|[ListWorkspaces](https://docs.byteplus.com/docs/cp/ListWorkspaces) |Query the list of workspaces. |
|[DeleteWorkspace](https://docs.byteplus.com/docs/cp/DeleteWorkspace) |Delete a workspace. |

## Code source

|API |Description |
|---|---|
|[CreateResource](https://docs.byteplus.com/docs/cp/CreateResource) |Create a code source in the specified workspace. |
|[ListResources](https://docs.byteplus.com/docs/cp/ListResources) |Obtain the code source list. |
|[UpdateResource](https://docs.byteplus.com/docs/cp/UpdateResource) |Update a code source. |
|[DeleteResource](https://docs.byteplus.com/docs/cp/DeleteResource) |Delete a code source. |

## Pipeline

|API |Description |
|---|---|
|[ListPipelines](https://docs.byteplus.com/docs/cp/ListPipelines) |Obtain the pipeline list. |
|[DeletePipeline](https://docs.byteplus.com/docs/cp/DeletePipeline) |Delete the specified pipeline under the specified workspace. |
|[CreatePipeline](https://docs.byteplus.com/docs/cp/createpipeline) |Create a pipeline. |

## Pipeline run

|API |Description |
|---|---|
|[RunPipeline](https://docs.byteplus.com/docs/cp/RunPipeline) |Run a pipeline. |
|[ListTaskRuns](https://docs.byteplus.com/docs/cp/ListTaskRuns) |Obtain the run record list of a task in a specific pipeline. |
|[ListPipelineRuns](https://docs.byteplus.com/docs/cp/ListPipelineRuns) |Obtain the run record list of a specific pipeline. |
|[CancelPipelineRun](https://docs.byteplus.com/docs/cp/CancelPipelineRun) |Cancel pipeline run. |

## Trigger

|API |Description |
|---|---|
|[CreatePipelineWebhookURL](https://docs.byteplus.com/docs/cp/CreatePipelineWebhookURL) |Create the pipeline's WebhookURL. |
|[CreateTrigger](https://docs.byteplus.com/docs/cp/CreateTrigger) |Create a trigger. |
|[ListTriggers](https://docs.byteplus.com/docs/cp/ListTriggers) |Obtain the trigger list of the current pipeline. |
|[UpdateTrigger](https://docs.byteplus.com/docs/cp/UpdateTrigger) |Update a trigger. |
|[DeleteTrigger](https://docs.byteplus.com/docs/cp/DeleteTrigger) |Delete a trigger. |

## Custom steps

|API |Description |
|---|---|
|[CreateComponentStep](https://docs.byteplus.com/docs/cp/CreateComponentStep) |Create a custom step. Only one custom step can be created at a time. |
|[ListComponentStep](https://docs.byteplus.com/docs/cp/ListComponentStep) |Obtain the custom steps under the current BytePlus root user. |
|[UpdateComponentStep](https://docs.byteplus.com/docs/cp/UpdateComponentStep) |Update custom steps. This action allows updating part of the descriptive fields, such as description, the defaultvalue of inputs, ... Suggestions: Use in compatibility upgrade scenes. |
|[UpgradeComponentStep](https://docs.byteplus.com/docs/cp/UpgradeComponentStep) |Upgrade custom steps. This action does not impact existing pipelines using historical version steps. |
|[DeleteComponentStep](https://docs.byteplus.com/docs/cp/DeleteComponentStep) |Delete custom steps. |

## Log

|API |Description |
|---|---|
|[GetTaskRunLog](https://docs.byteplus.com/docs/cp/GetTaskRunLog) |Obtain a task run log. |
|[GetTaskRunLogDownloadURI](https://docs.byteplus.com/docs/cp/GetTaskRunLogDownloadURI) |Obtain the download link for the task run log. |

## Service connection

|API |Description |
|---|---|
|[CreateServiceConnection](https://docs.byteplus.com/docs/cp/CreateServiceConnection) |Create service connection |
|[GetServiceConnection](https://docs.byteplus.com/docs/cp/GetServiceConnection) |Obtain service connection details |
|[ListServiceConnections](https://docs.byteplus.com/docs/cp/ListServiceConnections) |Obtain the service connection list |
|[UpdateServiceConnection](https://docs.byteplus.com/docs/cp/UpdateServiceConnection) |Update service connection |
|[DeleteServiceConnection](https://docs.byteplus.com/docs/cp/DeleteServiceConnection) |Delete service connection |

## Deployment resource

|API |Description |
|---|---|
|[CreateDeployResource](https://docs.byteplus.com/docs/cp/CreateDeployResource) |Create a deployment resource. |
|[ListDeployResources](https://docs.byteplus.com/docs/cp/ListDeployResources) |Obtain the deployment resource list. |
|[UpdateDeployResource](https://docs.byteplus.com/docs/cp/UpdateDeployResource) |Update a deployment resource. |
|[DeleteDeployResource](https://docs.byteplus.com/docs/cp/DeleteDeployResource) |Delete a deployment resource. |

## Managed app

|API |Description |
|---|---|
|[CreateManagedApp](https://docs.byteplus.com/docs/cp/CreateManagedApp) |Create a managed app. |
|[TriggerManagedAppDeploy](https://docs.byteplus.com/docs/cp/TriggerManagedAppDeploy) |Trigger managed app deployment. |
|[TriggerManagedAppScaling](https://docs.byteplus.com/docs/cp/TriggerManagedAppScaling) |Trigger app scaling. |
|[TriggerManagedAppRollback](https://docs.byteplus.com/docs/cp/TriggerManagedAppRollback) |Trigger app rollback. |
|[ListManagedAppChangeRecords](https://docs.byteplus.com/docs/cp/ListManagedAppChangeRecords) |List app change log. |
|[CancelManagedAppChangeRecord](https://docs.byteplus.com/docs/cp/CancelManagedAppChangeRecord) |Terminate an app change. |
|[ListManagedAppPods](https://docs.byteplus.com/docs/cp/ListManagedAppPods) |Obtain the managed app list of pods. |
|[GetManagedAppPodLog](https://docs.byteplus.com/docs/cp/GetManagedAppPodLog) |Obtain a managed app instance log. |
|[DeleteApp](https://docs.byteplus.com/docs/cp/DeleteApp) |Delete an app. |
