---
title: "API list"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/API_overview"
---

BytePlus Function Service (FaaS) provides the following API.

## Cloud sandboxes

### Sandbox instances

|API |Description |
|---|---|
|[CreateSandbox](https://docs.byteplus.com/en/docs/faas/CreateSandbox) |Create sandbox instances. |
|[ListSandboxes](https://docs.byteplus.com/en/docs/faas/ListSandboxes) |Obtain an instance list of sandbox applications. |
|[DescribeSandbox](https://docs.byteplus.com/en/docs/faas/DescribeSandbox) |Query the details of sandbox instances |
|[SetSandboxTimeout](https://docs.byteplus.com/en/docs/faas/SetSandboxTimeout) |Modify sandbox instance lifetime. |
|[KillSandbox](https://docs.byteplus.com/en/docs/faas/KillSandbox) |Delete a sandbox instance. |
|[ResumeSandbox](https://docs.byteplus.com/en/docs/6662/2288382) |Resume sandbox instance from paused state to running state. |
|[PauseSandbox](https://docs.byteplus.com/en/docs/6662/2544749) |Pause sandbox instance. |

### Sandbox images

|API |Description |
|---|---|
|[PrecacheSandboxImages](https://docs.byteplus.com/en/docs/faas/PrecacheSandboxImages) |Preheat custom images in batch. |
|[GetSandboxImagePrecacheTicket](https://docs.byteplus.com/en/docs/faas/GetSandboxImagePrecacheTicket) |Obtain details of an image preheating ticket. |
|[ListSandboxImages](https://docs.byteplus.com/en/docs/faas/ListSandboxImages) |Obtain information of preheated images in batch. |
|[DeleteSandboxImage](https://docs.byteplus.com/en/docs/faas/DeleteSandboxImage) |Delete the preheated image. |
|[CreateCustomImageRegistry](https://docs.byteplus.com/en/docs/6662/2600006) |Create custom CR. |
|[GetCustomImageRegistry](https://docs.byteplus.com/en/docs/6662/2600007) |Obtain custom CR information. |
|[ListCustomImageRegistries](https://docs.byteplus.com/en/docs/6662/2600008) |Batch retrieve custom Container Registry (CR) information. |
|[UpdateCustomImageRegistry](https://docs.byteplus.com/en/docs/6662/2600009) |Update custom CR. |
|[DeleteCustomImageRegistry](https://docs.byteplus.com/en/docs/6662/2600010) |Delete custom CR. |

## Functions

|API |Description |
|---|---|
|[CreateFunction](https://docs.byteplus.com/en/docs/faas/CreateFunction) |Create a function, including function configurations and function code. |
|[GetFunction](https://docs.byteplus.com/en/docs/faas/GetFunction) |Obtain function details, including function configurations and code. |
|[UpdateFunction](https://docs.byteplus.com/en/docs/faas/UpdateFunction) |Update a function, including function configurations and code. |
|[DeleteFunction](https://docs.byteplus.com/en/docs/faas/DeleteFunction) |Delete function. |
|[ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) |Obtain function information in batch. Contains only the basic configuration of a function, but not the function code. |
|[CopyFunction](https://docs.byteplus.com/en/docs/faas/CopyFunction) |Copy function. |
|[Release](https://docs.byteplus.com/en/docs/faas/Release) |Release a function. |
|[GetReleaseStatus](https://docs.byteplus.com/en/docs/faas/GetReleaseStatus) |Query the release status of a function. |
|[UpdateRelease](https://docs.byteplus.com/en/docs/faas/UpdateRelease) |Update function release (update release traffic proportion). |
|[AbortRelease](https://docs.byteplus.com/en/docs/faas/AbortRelease) |Cancel function release. |
|[GetRevision](https://docs.byteplus.com/en/docs/faas/GetRevision) |Obtain the version information of a function, including the configuration and code information of the current version. |
|[ListRevisions](https://docs.byteplus.com/en/docs/faas/ListRevisions) |Obtain the version configurations of functions in batch. |
|[ListReleaseRecords](https://docs.byteplus.com/en/docs/faas/ListReleaseRecords) |Query the release history of functions. |
|[GetImageSyncStatus](https://docs.byteplus.com/en/docs/faas/GetImageSyncStatus) |View the function image status, including synchronization and caching status of images. |

## Function instances

|API |Description |
|---|---|
|[ListFunctionInstances](https://docs.byteplus.com/en/docs/faas/ListFunctionInstances) |Query the list of function instances. |
|[GetFunctionInstanceLogs](https://docs.byteplus.com/en/docs/faas/GetFunctionInstanceLogs) |Query the logs of function instances. |
|[GenWebshellEndpoint](https://docs.byteplus.com/en/docs/faas/GenWebshellEndpoint) |Generate a Webshell port for a function instance. |

## Trigger

|API |Description |
|---|---|
|[ListTriggers](https://docs.byteplus.com/en/docs/faas/ListTriggers) |Obtain all triggers in bulk. |
|[GetRocketMQTrigger](https://docs.byteplus.com/en/docs/faas/GetRocketMQTrigger) |Query RocketMQ Trigger details. |

### Timer triggers

|API |Description |
|---|---|
|[CreateTimer](https://docs.byteplus.com/en/docs/faas/CreateTimer) |Call the CreateTimer interface to create a Timer Trigger in the specified function. |
|[GetTimer](https://docs.byteplus.com/en/docs/faas/GetTimer) |Call the GetTimer interface to obtain Timer trigger details. |
|[UpdateTimer](https://docs.byteplus.com/en/docs/faas/UpdateTimer) |Call the UpdateTimer interface to update the configuration of Timer trigger. |
|[DeleteTimer](https://docs.byteplus.com/en/docs/faas/DeleteTimer) |Call the DeleteTimer interface and delete the Timer Trigger. |

### Kafka triggers

|API |Description |
|---|---|
|[CreateKafkaTrigger](https://docs.byteplus.com/en/docs/faas/CreateKafkaTrigger) |Create Kafka trigger. |
|[UpdateKafkaTrigger](https://docs.byteplus.com/en/docs/faas/UpdateKafkaTrigger) |Update the specified Kafka Trigger. |
|[GetKafkaTrigger](https://docs.byteplus.com/en/docs/faas/GetKafkaTrigger) |Obtain detailed information of a Kafka trigger. |
|[DeleteKafkaTrigger](https://docs.byteplus.com/en/docs/faas/DeleteKafkaTrigger) |Delete a specified Kafka trigger. |

## Asynchronous tasks

|API |Description |
|---|---|
|[TerminateAsyncTask](https://docs.byteplus.com/en/docs/faas/TerminateAsyncTask) |Terminate asynchronous tasks. |
|[ListAsyncTasks](https://docs.byteplus.com/en/docs/faas/ListAsyncTasks) |Obtain the list of asynchronous tasks. |

## Dependency installation tasks

|API |Description |
|---|---|
|[CreateDependencyInstallTask](https://docs.byteplus.com/en/docs/faas/CreateDependencyInstallTask) |Create a dependency installation task. |
|[GetDependencyInstallTaskStatus](https://docs.byteplus.com/en/docs/faas/GetDependencyInstallTaskStatus) |View the status of dependency installation tasks. |
|[Terminating dependency installation tasks](https://docs.byteplus.com/en/docs/faas/TerminateDependencyInstallTask) |Terminate the dependency installation task. |
|[GetDependencyInstallTaskLogDownloadURI](https://docs.byteplus.com/en/docs/faas/GetDependencyInstallTaskLogDownloadURI) |View the log download link of dependency installation tasks. |
