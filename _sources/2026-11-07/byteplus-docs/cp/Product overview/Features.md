---
title: "Features"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Features"
---

Code Pipeline is committed to providing an open and user\-friendly enterprise\-grade CI/CD platform to help enterprises deliver business value with high quality and efficiency. This document provides a detailed introduction to the features currently supported by Code Pipeline.

<span id=".5qaC6KeI"></span>
## Overview

Introduce the product definition, usage workflow, and commonly used feature entry points of Code Pipeline to help you quickly understand the product.


* Resource overview: Displays the number of workspaces, pipelines, and applications in this account. 

* Getting started with Code Pipeline: Shows the workflow for using Code Pipeline and provides a step\-by\-step beginner guide to help you get started quickly. 

* Displays this account's pipeline tasks that are pending review or have already been reviewed, helping you monitor approval status in real time. 

* Common features: Display guidance for the cost center, product capabilities, and other related guidance. 

* Help documentation: Displays help documentation such as Code Pipeline quick start, best practices, and other help documentation.


<span id=".5bel5L2c5Yy6"></span>
## Workspace

A workspace is a virtual working environment. Each workspace operates independently, allowing enterprises to divide different projects among separate workspaces for management.


* Workspace lifecycle management: create, view, edit, copy, and delete workspaces.

* Workspace permissions: Supports setting the workspace visibility scope for permission management.


<span id=".5Luj56CB5rqQ"></span>
## Service connection

You can register services with the service connections in Code Pipeline in advance to facilitate unified management later. 


* Artifact repository： Register artifact repositories as services. 

* Code repository：Register code sources as services. 


<span id=".5rWB5rC057q_"></span>
## Pipeline

The pipeline is the carrier for Code Pipeline, enabling continuous delivery throughout the entire process from development to production by means of build automation, integration automation, validation automation, and deployment automation.


|Features |Description |
|---|---|
|Pipeline templates |Provides commonly used pipeline templates for Go, Node.js, Java, FaaS and Python. |
|Pipeline management |The pipeline is the vehicle for continuous delivery enabled by Code Pipeline, completing the process from development to launch through build automation, integration automation, validation automation, and deployment automation.<br><br><br>* Pipeline full lifecycle management: including creating, viewing, editing, copying, and deleting pipelines, among other actions.<br><br>* Save pipelines with incomplete configuration to the draft box<br><br>* Run a pipeline: Specify a branch, tag, or commit ID to run the pipeline.<br><br>* Terminate the pipeline: You can terminate the pipeline at any time during its execution.<br><br>* Failure retry: When a pipeline run fails, you can retry from the failed task.<br><br>* Real\-time logs: Provide run logs for each step in the pipeline, allowing users to track the pipeline's execution.<br><br>* Pipeline run details: View detailed information about pipeline runs, including the execution process and results, configuration information (such as basic information, environment variables, cache directory, and notifications), and detailed run information for each task or step (including run results, run logs, configuration information, and artifacts).<br><br>* Pipeline run history: Displays the run records for each pipeline to facilitate traceability.<br><br>* Pipeline notification records: Displays the notification records for each pipeline, including the pipeline run ID, the event that triggered the notification, notification details, trigger time, and more. |
|Pipeline configuration |Configure and orchestrate pipelines, and define your automated delivery process.<br><br><br>* Configure code source: Configure the code repository and branch to be pulled by the pipeline.<br><br>* Build environment: Supports public resource pool (system\-provided public build cluster) .<br><br>* Pipeline trigger rules include manual trigger, Webhook trigger, and scheduled trigger.<br><br>* Supports configuring automatic invalidation rules for Webhook and scheduled triggers to prevent frequent trigger failures in abnormal pipelines.<br><br>* Graphical orchestration: Provides graphical orchestration capabilities, supporting drag\-and\-drop for a three\-layer structure: stages, tasks, and steps. By orchestrating pipelines, you can organically connect tasks across each stage—such as testing, building, and deploying—to define your automated delivery process.<br><br>* Skip failed steps: Supports forcibly skipping failed steps and continuing pipeline execution, to meet requirements where the pipeline must proceed despite step failures.<br><br>* Environment variables: Each step in the pipeline can use environment variables as dynamic parameters, increasing the pipeline's flexibility. Currently supports dynamic, general, predefined, and custom environment variables.<br><br>* Cache directory: Configure the cache directory for build tasks. During the build process, dependencies that need to be downloaded are cached in the project path, improving the efficiency of subsequent builds. Currently supports preset or custom cache directory.<br><br>* Pipeline notification reminders: Pipeline notifications can be delivered via in\-app messages, SMS, email, Webhook, enabling you to quickly learn the results of build and deployment.<br><br>* Task Notification: Supports sending task\-level messages via Webhook to help you stay informed about task updates. |


<span id=".5bqU55So5Lqk5LuY"></span>
## Application delivery

An application\-centric cloud\-native application delivery platform that provides one\-stop, out\-of\-the\-box capabilities such as application access, configuration management, application release, and more, helping enterprises establish a comprehensive Code Pipeline solution.


|Features |Description |
|---|---|
|Member management |Provides dedicated member and permission management for application delivery: supports adding, modifying, and deleting application members, assigning preset role permissions to members, and supports multi\-role collaboration during application delivery. |
|Application management |Provide application\-centric lifecycle management capabilities.<br><br><br>* K8s YAML application management: Supports defining applications using native K8s YAML, enabling application creation, quick application onboarding, editing basic application information, and application deletion. This feature is designed for developers who are familiar with K8s. |
|||
|||
|Environment management |Perform full lifecycle management of Kubernetes environment instances for different categories (development, testing, staging, and production), including create, edit, and delete actions. |
|Deployment and maintenance |Deploy the application to the target environment instance and perform operations and maintenance for the environment.<br><br><br>* Deployment strategies: Supports native deployment and phased release.<br><br>* Manually initiate deployment, trigger via workflow, or trigger via pipeline.<br><br>* Observing the deployment process: During the environment deployment process, you can view deployment details, view real\-time Pod logs, cancel the deployment, and more.<br><br>* Deployment records: Supports tracking environment deployment records, rapid rollback, and more. |
|External integrations |Integrate external image repository services into application delivery Supports adding, editing, and deleting external services. |


<span id=".6LWE5rqQ566h55CG"></span>
## Resource management

Used for unified management of deploy resources required for deploy tasks and build resources required for build tasks.


|Features |Description |
|---|---|
|Deployment resource management |Used to manage the actual deployment locations of applications, such as Kubernetes clusters, cloud servers, virtual machines, physical machines, and more.<br><br><br>* Supports access to multiple types of deployment resources, including VKE clusters and custom clusters (by specifying a kubeconfig file).<br><br>* Supports viewing, editing, and deleting deployment resources.<br><br>* Supports controlling which workspaces can view deploy resources. |
|Build resource management |An environment used for managing and running build tasks.<br><br><br>* Supports public resource pools (system\-provided build clusters) . |


<span id=".5qih5p2_5biC5Zy6"></span>
## Template marketplace

Includes commonly used pipeline step templates and provides a custom steps feature to meet users' personalized build and deployment needs.


|Features |Description |
|---|---|
|Step template |Provide ready\-to\-use step templates for pipelines to meet enterprise requirements for daily build, test, deploy, and more tasks.<br><br><br>* SonarQube code scanning: Supports integration with the SonarQube code analysis platform to enable rapid code detection and effective code quality management.<br><br>* Unit testing: Supports unit testing for Java Maven, Java Gradle, Python, and Go.<br><br>* Command execution: Supports Bash command execution.<br><br>* Manual checkpoint: The pipeline pauses and waits for human intervention, for example during manual testing or security review.<br><br>* Compilation and build: Supports compilation and build for Java (Maven and Gradle), Python, Go, and Node.js.<br><br>* Package and push images to a custom repository: Package the image and push it to a third\-party repository. Support packaging of multi\-architecture images and skipping certificate verification.<br><br>* Package and push container images to the image repository: Package the container image and push it to the BytePlus image repository. Support packaging multi\-architecture images and skipping certificate verification.<br><br>* Kubernetes image upgrade: Supports upgrading images for applications on the Kubernetes cluster.<br><br>* Kubernetes rolling update: Supports batch rolling updates of Deployments on a Kubernetes cluster by instance.<br><br>* Create new Kubernetes applications, tasks, and more using YAML files<br><br>* Custom environment command execution<br><br><br>Supports using a custom environment to execute commands, suitable for scenarios where built\-in tasks do not meet user requirements. |
|Custom steps |Custom steps are used to extend the capabilities of the pipeline to meet the personalized build and deployment needs of enterprises. For example, tools or commands that the team is proficient with can be packaged as custom steps, making it easier for other projects and team members to quickly reuse them.<br><br><br>* Supports creating, updating, enabling, and disabling custom steps, and viewing pipelines associated with custom steps. |
