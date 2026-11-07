---
title: "Monitor jobs using Ray Dashboard"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Monitor_jobs_using_Ray_Dashboard"
---

Jobs are visually monitored in Ray Dashboard. This section describes how to access the Ray Dashboard UI.

<span id="_1-前置条件"></span>
## 1 Prerequisites

The KubeRay service is running normally.

<span id="_2-配置"></span>
## 2 Configuration

<span id="_2-1-方案一（推荐）"></span>
### 2.1 Option 1 (recommended)


1. Install the ingress\-nginx component in the VKE cluster.

   * You can check whether the ingress\-controller is working properly on the following page:

   * If the external endpoint is empty, go to the ingress\-nginx\-controller service details and click "Events" to view specific error logs:

2. Log in to [EMR Console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

   * In the left navigation bar, click to enter the **Cluster List \> on VKE \> Cluster Details \> Access Links** page and open Quick Connect.


<span id="_2-2-方案二"></span>
### 2.2 Option 2

This section covers manual configuration of Ray's web UI.

Select the correct namespace, then install a loadBalancer for the Ray head pod and configure the public address:

Log in to the Ray UI:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c01750f250499dade8ba7fc939b78b28.png) </span>
