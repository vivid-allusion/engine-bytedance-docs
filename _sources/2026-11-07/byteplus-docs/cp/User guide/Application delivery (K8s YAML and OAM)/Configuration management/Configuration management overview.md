---
title: "Configuration management overview"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Configuration_management_overview"
---

This article introduces the contents and purpose of configuration management.

<span id=".5qaC6L-w"></span>
## Overview

Configuration management is used to manage a series of variable groups, with the aim of standardizing and customizing application release processes, environment deployment, and more. Configuration management consists of two parts: configuration items and environment configurations.


* **Configuration item**: A series of variable keys. Configuration items are divided into preset configuration items and custom configuration items.

* **Environment configuration**: Environment configuration is used to manage configuration items and their values in each environment instance. For example, whether a configuration item is enabled in the current environment instance, the value of the configuration item in the current environment, and more.


Create configuration items in configuration item management. In application orchestration, extract environment\-specific configurations as configuration items. In environment configuration, assign different values to configuration items for each environment. This allows a single application orchestration to be deployed differently across multiple environments.

<span id=".6aKE572u6YWN572u6aG5"></span>
## Preset configuration items

System\-defined configuration items. The value passing rules for configuration items are fixed and cannot be modified. Preset configuration items are global configuration items and can be used directly; they do not need to be enabled in environment configuration. The system provides the following preset configuration items for your use.


|Configuration Item |Description |Get value |
|---|---|---|
|AppName |The Application ID of the current application. |The value is the Application ID customized by the user when creating the application. |
|Timestamp |Timestamp, indicating the start time of the deployment action. |The value is the start time of the deployment action for the current application. |
|EnvName |The Environment ID of the current deployment environment. |The value is the Environment ID customized by the user when creating the environment. |


<span id=".6Ieq5a6a5LmJ6YWN572u6aG5"></span>
## Custom configuration items

User\-defined Configuration items Custom configuration items and environments are independent of each other. To use custom configuration items, you must enable them and assign values in the environment configuration.
