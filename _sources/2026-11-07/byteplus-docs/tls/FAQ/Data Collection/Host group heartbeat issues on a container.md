---
title: "Host group heartbeat issues on a container"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/host_group_heartbeat_issues_on_a_container"
---

When you use LogCollector to collect container text logs or standard output logs, the heartbeat status of LogCollector in the host group may be abnormal, resulting in issues such as log collection failures. This topic introduces how to troubleshoot such issues and restore the LogCollector heartbeat status.

<span id="背景信息"></span>
## Background

LogCollector is a self\-developed log collection client of Torch Log Service (TLS), which can be used to quickly report container log data. After you install LogCollector on a container, LogCollector periodically sends heartbeat packets to the server. if the status of certain IP addresses is **abnormal** on the host group configuration page in the TLS console, it means a client\-server connection failure occurs.

<span id="问题现象"></span>
## Issue description

On the host group details page in the TLS console, if the status of certain IP addresses is **abnormal** in the **Heartbeat status** area, the LogCollector heartbeat status of the container is abnormal. This means the LogCollector client on the container fails to be connected to the server.

When the heartbeat status is abnormal, the LogCollector client on the container cannot report the collected log data to the server. As a result, the logs cannot be collected into topics, and you cannot search or query new log data in real time in the TLS console.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6df9f33e016a431aa92b37d54b31984d~tplv-goo7wpa0wc-image.image) </span>

<span id="注意事项"></span>
## Precautions

LogCollector reads the IP address of the first network interface of its pod, and reports it to the host group as the pod IP address through a heartbeat.

After you perform a rolling upgrade for a DaemonSet or restart it, the existing pods are deleted and the existing LogCollectors stop running. This causes the status of the IP addresses of these existing pods to become **abnormal**. This is because new pods are created, new LogCollectors start running, and the IP addresses of these new pods are reported to the host group through heartbeats.

If you want to delete the IP addresses of old pods, click **Clear abnormal hosts** on the host group details page.

<span id="排查方案"></span>
## Troubleshooting

This topic uses installing LogCollector in a Kubernetes cluster through a DaemonSet as an example to explain the troubleshooting steps.

<span id="_1-检查-logcollector-状态"></span>
### Step 1: Verify the LogCollector status

Log on to the Kubernetes cluster, then run the following command to view the LogCollector status:

```Bash
kubectl -n ${namespace}  get pods  | grep ${Daemonset}
```


In the following example, the name of the DaemonSet is log\-collector, and its namespace is tls\-log.

```Bash
kubectl -n tls-log  get pods  | grep log-collector
```


Response description:


* If no pod named log\-collector\-xxxxx is returned for the NAME field in the response, it means LogCollector is not installed in the Kubernetes cluster. To solve this issue, refer to [No status information](https://docs.byteplus.com/docs/tls/abnormal_logcollector_status_on_a_container#%E6%B2%A1%E6%9C%89%E7%8A%B6%E6%80%81%E4%BF%A1%E6%81%AF).

* If one of the values of the `STATUS` field is not Running in the response, it means LogCollector is installed on the container but LogCollector on the pod is not running properly. To solve this issue, refer to [Abnormal LogCollector status on a container](https://docs.byteplus.com/docs/tls/abnormal_logcollector_status_on_a_container).

* If all values of the `STATUS` field are Running in the response, it means LogCollector is installed in the Kubernetes cluster and is running properly.

   If the LogCollector heartbeat status is still **abnormal** in the console, perform the following steps for further troubleshooting.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_43bdcb7a2aac2d566677fff4e4f30728.png) </span>


<span id="_2-检查鉴权参数配置"></span>
### Step 2: Verify the authentication parameter settings

Before you install LogCollector using a DaemonSet, create a ConfigMap, and add the required TLS configuration to the `output.tls` field in the `logcollector_config.yaml` file for authentication and connecting to TLS. Incorrect parameter settings may cause LogCollector heartbeat errors.

Run the following command to open the `filebeat.yml` file and verify the authentication parameters configured when you create a ConfigMap: In the following example, the name of the DaemonSet is log\-collector, and its namespace is tls\-log.

```Bash
kubectl -n tls-log describe configmaps log-collector-config
```


The following table describes the authentication parameters:


|Parameter |Example |Description |How to Get |
|---|---|---|---|
|endpoint |https://tls\-ap\-southeast\-1.bytepluses.com |The endpoint of TLS, that is, the service URL. |Log on to the BytePlus console, and view the endpoint on the project details page. |
|secret_id |AKLY\*\*\*\*\*\*\*\*\* |The AccessKey ID of a BytePlus account. |The AccessKey ID of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey ID as prompted. |
|secret_key |TUdZ\*\*\*\*\*\*\*\* |The AccessKey secret of a BytePlus account. |The AccessKey secret of a BytePlus account or an IAM user.<br><br>On the [Access Key Management](https://console.byteplus.com/iam/keymanage) of the BytePlus console, view and copy the AccessKey secret as prompted. |
|region |ap\-southeast\-1 |The Region where a project is deployed. |In the top menu bar of the TLS console, view the Region where the project resides. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In <code>output.tls</code>, you cannot configure the ip and label parameters at the same time. Otherwise, heartbeat errors occur.</div>


An example of a configuration file is offered as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a703e05889111cf73c35b726d160e33.png) </span>

If the authentication parameters are incorrectly configured, modify them, restart the DaemonSet, and view the status of the host group later. If the LogCollector heartbeat status is still **abnormal** in the console, perform the following steps for further troubleshooting.

<span id="_3-检查-logcollector-是否为最新版本"></span>
### Step 3: Verify whether the latest LogCollector version is used

LogCollector supports host groups since v 1.0.1. If the version of LogCollector installed on the container is not v 1.0.1 or later, the LogCollector heartbeat status may be abnormal, and the server cannot recognize this LogCollector. Therefore, if the LogCollector heartbeat status is abnormal, verify whether the LogCollector version meets the requirements.

Run the following command to view the LogCollector version. In the response, the image URL of the currently installed LogCollector is displayed in the Image field. If the LogCollector version is not v 1.0.1 or later or not the latest, upgrade LogCollector to its latest version. For more information, refer to [Upgrade LogCollector in a Kubernetes cluster](https://docs.byteplus.com/docs/tls/upgrade_logcollector_in_a_kubernetes_cluster).

```Bash
kubectl -n tls-log describe daemonsets.apps log-collector
```


A response similar to the following example is returned:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04bb1e0d77ce6874738f771985147212.png) </span>

If the LogCollector heartbeat status is still **abnormal** in the console after you upgrade LogCollector, perform the following steps for further troubleshooting.

<span id="_4-检查机器标识配置"></span>
### Step 4: Verify the host label settings

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If a label\-based host group is used, refer to this step for troubleshooting.</div>


* <div data-tips="true" data-tips-type="tip">When you use LogCollector to collect container text logs or standard output logs, we recommend that you create a label\-based host group.</div>



In a label\-based host group, the host label must be consistent with that configured in the LogCollector configuration file. Otherwise, the LogCollector heartbeat status cannot be found in the host group.

Run the following command to view the LogCollector configuration file:

```Bash
kubectl -n tls-log describe configmaps log-collector-config
```


In the following response, the value of `label` is the host label configured in LogCollector. If this value is inconsistent with the host label configured in the host group, modify the host group setting and verify the host status later.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2561b8077b2985d9b3f760b99f11ef44.png) </span>

<span id="_5-检查机器组-ip-地址配置"></span>
### Step 5: Verify the IP address settings of a host group

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If an IP address\-based host group is used, refer to this step for troubleshooting.</div>


By default, LogCollector reads the IP address of the first network interface of its pod, and records the IP address in the `agent_info.json` file as the IP address of the pod. When you create an IP address\-based host group in the console, type the IP address recorded in the `agent_info.json` file into the host group, to add LogCollector on the specified pod to the host group.

If the IP address configured in the host group is inconsistent with that in the `agent_info.json` file, the console displays that the LogCollector heartbeat status of this container is abnormal and logs cannot be collected.

Run the following command to view the `agent_info.json` file and verify whether the IP address in the `ip` field is consistent with that in the console.


1. View the `agent_info.json` file.

   ```Bash
   kubectl -n tls-log exec -it log-collector-9ph8j -- bash
   
   cat agent_info.json
   ```
   

   In the following response, the `ip` field indicates the current pod IP address obtained by LogCollector.

   ```Bash
   {
       hostname :  C02G64T1MD6R ,
       ip : 10.*.*.* ,
       logcollect_version :  1.0.2 ,
       update_time :  2022.01.07 18:38:12 
   }
   ```
   

2. View the IP address configured in the console.

   On the details page of the host group, view the IP addresses of all pods in the host group. If the IP address configured in the console is inconsistent with that in the `agent_info.json` file, modify the host group setting and verify the host status later.
