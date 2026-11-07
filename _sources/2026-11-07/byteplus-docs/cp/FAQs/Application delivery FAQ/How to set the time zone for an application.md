---
title: "How to set the time zone for an application"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/How_to_set_the_time_zone_for_an_application"
---

For Kubernetes applications, the default timezone inside containers is UTC+0. If you want to use a different time zone, you can do so by setting environment variables.

Of these,


* The key is fixed as `TZ`.

* The possible values for value can be found in the [Time zone summary](https://www.zeitverschiebung.net/cn/all-time-zones.html) documentation. For example, the UTC+8 time zone is `Asia/Shanghai`.


Below, we introduce how to set environment variables for different types of applications.

<span id=".5omY566h5bqU55So"></span>
## Managed application

When deploying a managed application, set the time zone environment variable on the Advanced configuration page. After completing the settings, proceed with deployment as usual.

<span id=".b2FtLeW6lOeUqA=="></span>
## OAM applications


1. In the application orchestration tab, select the target component, click **edit**, and configure the time zone environment variable.

2. Set the active environment. Click **Orchestration History**, and on the Orchestration History page, make the recent orchestration effective in the target environment.

3. Switch to the environment tab and deploy to the target environment.


<span id=".azhzLXlhbWwt5bqU55So"></span>
## K8s YAML applications


1. In the application orchestration tab, select the target workload, click **Edit**, and set the time zone environment variable.

2. After completing the settings, click **confirm**, and in the pop\-up dialog box, select the environment in which this configuration will take effect.

3. Switch to the environment tab and deploy to the target environment.
