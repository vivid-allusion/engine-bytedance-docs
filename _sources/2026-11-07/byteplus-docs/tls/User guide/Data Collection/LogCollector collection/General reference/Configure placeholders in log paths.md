---
title: "Configure placeholders in log paths"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/configure_placeholders_in_log_paths"
---

If you collect text logs from containers using a DaemonSet, you can configure a placeholder used for a reserved field specific to the containers in your collection path. This can avoid mismatches between the content of logs collected by LogCollector and the metadata field content of containers due to a wildcard configured in the collection path. This topic describes the use scenarios of placeholders in the collection paths of container logs and their configuration methods.

<span id="应用场景"></span>
## Use scenarios

If you collect text logs from containers using a DaemonSet, you can configure a placeholder in the collection path to prevent mismatches between the content of logs and the metadata field content of containers. Assume that an application is deployed in a container, and its logs are persisted to nodes through HostPath mounting. During a rolling upgrade of the application, the log file paths of new and old pods on the node are identical except for the pod name or other container metadata. Assume that you use a wildcard ( `*` ) in **Collection path** configured in your LogCollector collection rule to dynamically match the pod name or other container metadata. In this case, LogCollector may continue collecting logs from the old pod after the application is upgraded.

For example, the path of an application log file on a node is `/data00/basic_log/mnt_logs/tls_api_autotest-tls/POD_api-autotest-tls-6df9c76bf4-pxxxx/tlsapi/access.log`, where **`POD_api-autotest-tls-6df9c76bf4-pxxxx`** is the pod name. If you use a wildcard (`*`) to specify this part of the collection path, a mismatch issue occurs after a rolling upgrade of the application. Specifically, the wildcard ( `*` ) continues to match and collect log files from the old pod, but the reserved field `__pod_name__` automatically switches to a new pod name. This can lead to a mismatch between a reserved field in the logs and the log content.

<span id="配置方式"></span>
## Configuration methods

After installing LogCollector in the Kubernetes cluster using a DaemonSet and creating a host group, you can create a log collection rule and specify a collection path that includes a placeholder for your container reserved field through the console or API.


|Configuration Method |Instruction |
|---|---|
|Console\-based configuration |Create a collection rule in the console, and specify a collection path that includes a placeholder for a container reserved field in the **Collection path** step.<br><br>For more information on the procedure, refer to [Configure a DaemonSet in the console for collecting text logs from a container](https://docs.byteplus.com/docs/tls/collecte_text_logs_daemonSet) |
|API\-based configuration |Call refer to [CreateRule](https://docs.byteplus.com/docs/tls/api-createrule). to create a collection rule and type a collection path that includes a placeholder for container reserved field into the request parameter **Paths**. |


If you collect text logs from containers using a DaemonSet, you can configure a placeholder for your container reserved field in the collection path. The placeholder format is `{Container reserved field}`. The placeholder is used to dynamically match the container metadata automatically written by LogCollector in a container reserved field. For more information on supported container reserved fields, refer to [Background](https://docs.byteplus.com/docs/tls/collecte_text_logs_daemonSet#%E8%83%8C%E6%99%AF%E4%BF%A1%E6%81%AF).

For example, if your container reserved fields include the field `__pod_name__`, you can configure the collection path as `/var/log/basic_log/POD_{__pod_name__}/tlsapi/access.log`. In this case, `{__pod_name__}` is a placeholder, and LogCollector automatically replaces this placeholder with an actual pod name when it collects logs.
