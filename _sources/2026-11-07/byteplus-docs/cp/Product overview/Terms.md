---
title: "Terms"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Terms"
---

This document summarizes the fundamental concepts involved in using Code Pipeline, making it easy for you to quickly reference and understand them.


|Terminology |Description |
|---|---|
|Workspace |A workspace is an independent R&D project space. The workspace contains the code sources and pipelines associated with this project. Team members collaborate on development in the workspace to fulfill requirements. |
|Code source |Code source is one of the input sources for the pipeline. The code source is used to manage your Repository URL and token information. |
|Pipeline |The pipeline is the carrier of Code Pipeline, connecting the entire workflow of code development, testing, build verification, deployment, and release, helping enterprises deliver their business services with high quality and efficiency. |
|Input source |Pipeline input sources, for example: code repositories, pipeline artifacts, custom files, and more. |
|Stage |A stage is a collection of tasks executed sequentially within a pipeline, with stages executed in series. |
|Task |The specific actions that need to be completed within the stage. Code Pipeline currently includes the following categories of predefined tasks: testing, building, deployment, command execution, image building and pushing, process control, and more.<br><br><br>* In version 1, tasks are executed in parallel.<br><br>* In v2, tasks can be executed either serially or in parallel. |
|Step |The specific steps to be completed within a task, executed in sequence. A step is the core capability at the lowest level of a pipeline, and every pipeline is constructed by organizing and combining steps. |
|Deploy resource |Manage the actual deployment locations of applications, for example, Kubernetes clusters, cloud servers, virtual machines, and physical machines. |
|Application |An application is the smallest unit of development, deployment, or release. It provides external services and can be delivered independently. For example: SSO login application, Web front\-end application, DB database application, and so on. |
|Environment type |The environment type is primarily used for environment classification and permission control to facilitate collaboration among multiple roles in delivering applications. The Code Pipeline system includes four preset environment types: development, testing, staging, and production. |
|Environment |The environment is the platform for running an application. An application can create multiple environments for different scenarios such as development, testing, and production. Each environment is associated with a deploy resource, such as a Kubernetes cluster.<br><br>Each environment belongs to an environment type; an environment type is associated with multiple environments. |
|Workflow |A workflow is used to create a complete application release process. By automating build, integration, validation, and deployment, it accomplishes continuous delivery of the application from development to launch.<br><br>A workflow typically includes rigorous manual approval steps and, during execution, supports notifications, viewing real\-time logs, and rapid rollback. This effectively helps enterprises establish a comprehensive release process and reduce the risk of release. |
|Configuration |Groups of variables used to replace values during deployment to support environment\-specific deployment. For example: Namespace, image, cpu_limit, and more. |
|Artifact |Binary packages for deploying the application. For example, images used for Kubernetes deployment, Helm Chart, and jar packages used for host deployment, and more. |
|Concurrency lock |Set the maximum concurrency limit for pipelines. Each run of the pipeline is considered one unit of concurrency. When a group of pipelines is associated with the same concurrency lock, the maximum concurrency of these pipelines will be restricted by the concurrency lock. Pipelines that exceed the maximum concurrency will be queued in a first\-in, first\-out manner. |
|Host group |A host group is a collection of host instances. Typically, a host group corresponds to a release environment for an application or to a task\-specific execution environment within a pipeline. |
