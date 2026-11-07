---
title: "Add Maven Setting global configurations"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Add_Maven_Setting_global_configurations"
---

Supports adding a Maven settings configuration file at the global Code Pipeline level, eliminating the need to configure it in each pipeline task and improving the efficiency of pipeline creation and maintenance.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

Custom Maven global configuration is only effective in the system\-provided Java environment.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Maven settings configuration file in `xml` format has been created. The file must be smaller than 1 MB.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Global configurations** \> **Build configurations**. In the central area, either click or drag an existing `xml` file.


<span id=".5pON5L2c57uT5p6c"></span>
## Operation results

After completing the configuration, you can apply the added Maven configuration when subsequently adding a **Java build or Java test** task in the pipeline.

<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


* **View uploaded Maven configuration files**: Click **Preview** to view configuration file details.

* **Re\-upload the Maven configuration file**: After updating the configuration file on your local machine, click **Re\-upload** to update the global configurations.
