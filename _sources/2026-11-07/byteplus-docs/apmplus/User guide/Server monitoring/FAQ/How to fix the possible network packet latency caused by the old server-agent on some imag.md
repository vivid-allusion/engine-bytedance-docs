---
title: "How to fix the possible network packet latency caused by the old server-agent on some images?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_can_old_server_agent_affecting_network_latency_on_some_images_be_fixed"
---

<span id="abf01ca3"></span>
## Issue description

Old server\-agent (below v1.0.31) may cause host network packet latency on non‑default VKE images.

<span id="438d4fba"></span>
## Cause analysis

On those images, server\-agent enables many protection rules, increasing logs and CPU scheduling delays, which may occasionally impact packet transfer.

<span id="059d429c"></span>
## Solutions

The server\-agent collects host metrics, logs, and traces. For performance, it must run as a privileged container, so existing agents need privilege elevation.

Select one of the two solutions below based on your actual server\-agent deployment method.

<span id="dc01f9a3"></span>
### Method 1: Manually modify the YAML configuration

If you deployed server\-agent manually via YAML, edit its YAML file to set it as a privileged container.


1. Run the kubectl command in your cluster to open the server\-agent editing page.


```Bash
kubectl -n {{your_namespace}} edit daemenset server-agent 
```



2. Add `privileged: true` under `securityContext` to make server\-agent a privileged container.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99990bcb2bb24ad9b25466712894e013~tplv-goo7wpa0wc-image.image) </span>

<span id="dc01f9a3"></span>
### Method 2: Upgrade the VKE APMPlus add\-on

If you deployed server\-agent via the VKE console, upgrading the add\-on to the latest version can fix the issue.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The add\-on defaults to the latest version. This issue has been fixed in v1.0.31.</div>



1. Log in to the VKE console, select **Cluster** in the left navigation pane, and click the target cluster.

2. In the cluster management page, select **Addons** in the left navigation pane, and find the apmplus\-server\-agent add\-on in the Monitoring tab.

3. Click **Upgrade** in the upper\-right corner of the add\-on card to upgrade the add\-on to the latest version.


<span id="c0e4b8db"></span>
## Validate results


1. Go to the VKE console and check whether server\-agent has been successfully started in your cluster. Expected result: All instances of the server\-agent daemon set are in the running state.

2. Go to the APMPlus console and check for anomalies in host, Docker, and process monitoring data. Expected result: Monitoring data returns to normal.
