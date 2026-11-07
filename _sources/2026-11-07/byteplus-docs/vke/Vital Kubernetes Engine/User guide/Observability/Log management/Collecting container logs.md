---
title: "Collecting container logs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Collecting-container-logs"
---

VKE clusters allow you to collect container logs, including standard output logs and file path logs, by using TLS of BytePlus. This topic describes how to configure and view container logs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic describes log collection methods for standard containers. For log collection methods for Vital Container Instance (VCI), see <a href="https://docs.byteplus.com/en/docs/vke/Collecting-VCI-container-logs-using-Torch-Log-Service">Collecting VCI container logs by using TLS</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

To collect logs in JSON format, you need to upgrade the log\-collector add\-on to v1.2.5 or later. For details, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/log-collector).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* TLS has been activated. To activate this service, log in to the [TLS console](https://console.byteplus.com/tls) and activate the service based on the on\-screen prompts.

* A **log project** and a **log topic** have been created in TLS. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics) of .

* The log\-collector add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the add\-on is not installed, you will be prompted to install the add\-on on the <strong>Log management</strong> page. Install the log\-collector add\-on based on the on\-screen prompts.   </div>
   

<span id=".6YWN572u5pel5b-X6YeH6ZuG"></span>
## Procedure

VKE allows you to collect standard output (Stdout), standard error (Stderr), and text logs of containers. Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to its management page.

3. In the left navigation bar, click **Log management**. Then, click the **Log collection rule** tab.

4. Click **Create collection rule** to configure a container log collection rule.

   * **Select ** **log space**: Specify the **IAM project**, **Project**, and **Topic** parameters. After you complete the configuration, click **Next step: Collection rule**.

   * **Collection rule**: Configure a collection rule for container logs, including log collection type and collection target. After you complete the configuration, click **Next step: Check the index configuration**.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This topic only describes the commonly required parameters when you configure collection rules. For more parameter descriptions, see <a href="https://docs.byteplus.com/en/docs/tls/collecte_stdout_daemonset">Collecting container standard output</a> and <a href="https://docs.byteplus.com/en/docs/tls/collecte_text_logs_daemonSet">Collecting container text logs</a>.   </div>
   

   
   <Tabs>
   <Tab zoneid="HkPwLxWwxc" title="Standard output logs">
   <TabTitle>Standard output logs</TabTitle>
   
   VKE allows you to collect standard output (Stdout) and standard error (Stderr) logs of containers.
   
   
   |Parameters |Description |
   |---|---|
   |**Configuration basic information** ||
   |Regular alias |Specify a name for the collection rule.<br><br>Click **Import other collection configurations** to import other created collection configurations. |
   |Container log collection |Select **Enable** to enable container log collection. |
   |Acquisition type |Select the container log collection type. **K8s container standard output and K8s container text log** are supported. In this example, select **K8s container standard output**. |
   |Collection information |Select container log collection information. Valid values: **Standard output \- stdout** and **Standard error \- stderr**. |
   |Common container collection rule |Specify the log collection target and content by using the general information of the container. For specific parameter descriptions, see [Collecting container standard output](https://docs.byteplus.com/en/docs/tls/collecte_stdout_daemonset).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not specify a general container collection rule, logs from all containers in the cluster will be collected.</div><br> |
   |K8s collection rules |Specify the log collection target and content by using Kubernetes container information. For specific parameter descriptions, see [Collecting container standard output](https://docs.byteplus.com/en/docs/tls/collecte_stdout_daemonset).<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not specify a Kubernetes collection rule, logs from all containers in the cluster will be collected.</div><br> |
   |**Configure Log Format** ||
   |Collection mode |Select a log file parsing mode. You can select an appropriate collection mode based on your business scenarios and configure a log parsing rule in the specified mode. For details of different modes, see the following topics:<br><br><br>* [Single-line full text mode](https://docs.byteplus.com/en/docs/tls/single_line_full_text_mode)<br><br>* [JSON mode](https://docs.byteplus.com/en/docs/tls/json_mode)<br><br>* [Separator mode](https://docs.byteplus.com/en/docs/tls/delimiter_based_mode)<br><br>* [Multi-line full text mode](https://docs.byteplus.com/en/docs/tls/multi_line_full_text_mode)<br><br>* [Single-line complete regex mode](https://docs.byteplus.com/en/docs/tls/full_regex_based_single_line_mode)<br><br>* [Multi-line complete regex mode](https://docs.byteplus.com/en/docs/tls/full_regex_based_multi_line_mode)<br><br>* [NGINX configuration mode](https://docs.byteplus.com/en/docs/tls/nginx_based_mode) |
   
   
   
   </Tab>
   <Tab zoneid="uvC0Yp6Pgq" title="Container text logs">
   <TabTitle>Container text logs</TabTitle>
   
   VKE allows you to collect text logs under specified paths of containers.
   
   
   |Parameter |Description |
   |---|---|
   |**Configuration basic information** ||
   |Regular alias |Specify a name for the collection rule.<br><br>Click **Import other collection configurations** to import other created collection configurations. |
   |Container log collection |Select **Enable** to enable container log collection. |
   |Acquisition type |Select the container log collection type. **K8s container standard output and K8s container text log** are supported. In this example, select **K8s container text log**. |
   |Common container collection rule |Specify the log collection target and content by using the general information of the container. For specific parameter descriptions, see [Collecting container text logs](https://docs.byteplus.com/en/docs/tls/collecte_text_logs_daemonSet).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not specify a general container collection rule, logs from all containers in the cluster will be collected.</div><br> |
   |K8s collection rules |Specify the log collection target and content by using Kubernetes container information. For specific parameter descriptions, see [Collecting container text logs](https://docs.byteplus.com/en/docs/tls/collecte_text_logs_daemonSet).<br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not specify a Kubernetes collection rule, logs from all containers in the cluster will be collected.</div><br> |
   |Acquisition path |Specify the log path in the target container, such as `/user/tomcat/*.log`. |
   |**Configure Log Format** ||
   |Collection mode |Select a log file parsing mode. You can select an appropriate collection mode based on your business scenarios and configure a log parsing rule in the specified mode. For descriptions and details of different modes, see the following topics:<br><br><br>* [Single-line full text mode](https://docs.byteplus.com/en/docs/tls/single_line_full_text_mode)<br><br>* [JSON mode](https://docs.byteplus.com/en/docs/tls/json_mode)<br><br>* [Separator mode](https://docs.byteplus.com/en/docs/tls/delimiter_based_mode)<br><br>* [Multi-line full text mode](https://docs.byteplus.com/en/docs/tls/multi_line_full_text_mode)<br><br>* [Single-line complete regex mode](https://docs.byteplus.com/en/docs/tls/full_regex_based_single_line_mode)<br><br>* [Multi-line complete regex mode](https://docs.byteplus.com/en/docs/tls/full_regex_based_multi_line_mode)<br><br>* [NGINX configuration mode](https://docs.byteplus.com/en/docs/tls/nginx_based_mode) |
   
   
   
   
   
   </Tab>
   </Tabs>
   

   * **Check the index configuration**: Specify or update indexes based on the on\-screen prompts as needed. You can also click **Import existing index configuration** to import indexes from other log topics.

      * If no indexes are configured for the current log topic, configure one based on the instructions in [Configuring indexes](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2).

      * If an index is already configured for the current log topic, determine whether to update the index based on the log fields parsed in the collection rule.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can query and analyze the collected log data only if you enable the index.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The updated index settings only take effect on subsequently written data. For other usage instructions and limitations about query and analysis, see <a href="https://docs.byteplus.com/en/docs/tls/Query-overview-2">Query overview</a> and <a href="https://docs.byteplus.com/en/docs/tls/Analysis-overview">Analysis overview</a>.   </div>
   

5. Click **Submit** to complete the configuration.


<span id="PJiGnGmg"></span>
## Validating results


1. In the left navigation bar of the cluster management page, click **Log management**.

2. Click the **Container log** tab and specify a log project and log topic to view the container logs of the current cluster.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For log query and analysis syntax, see <a href="https://docs.byteplus.com/en/docs/tls/Log-query-syntax-2?lang=en">Query syntax</a> and <a href="https://docs.byteplus.com/en/docs/tls/Analyzing_Grammar?lang=en">Analysis syntax</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For chart analysis syntax, see <a href="https://docs.byteplus.com/en/docs/tls/chart_overview?lang=en">Query and analysis charts</a>.   </div>
   

3. Enter the index content, such as `__pod_name__ : "log-collector-lptnx"`, select the query time range, and then click **Search** to view the logs of the specified container.


<span id=".566h55CG6YeH6ZuG6KeE5YiZ"></span>
## Other configurations

<span id="xQP42QTD"></span>
### Filtering collected data

During log collection, a large number of less significant or irrelevant logs (such as logs at the DEBUG/INFO level) exist, which wastes storage resources, increases costs, and affects query efficiency. Therefore, you can achieve efficient and secure log collection by using fine\-grained filtering policies.


<Tabs>
<Tab zoneid="lpEGEsaw" title="Filter by collection rule">
<TabTitle>Filter by collection rule</TabTitle>

You can specify collection conditions by using the container metadata (such as container name, container label, and container environment variables) or Kubernetes container information (such as namespace, workload type, and workload name) when you configure a collection rule. This specifies specific containers from which the logs are to be collected. Procedure:

When you configure the collection rule, enable **Common container collection rule** or **K8s collection rules** based on your business requirements, and configure the details of the collection rule.


|Collection rule |Configuration description |
|---|---|
|Common container collection rule |* Container name: Specify the name of the container whose logs are to be collected. Regular expression matching is supported. For example, if you set the container name to `^(container-demo)$`, the logs of all containers named `container-demo` are collected.<br><br>* Container label allowlist and blocklist: You can specify containers whose logs are to be collected using container labels.<br><br>* Container environment variable allowlist and blocklist: You can specify containers whose logs are to be collected by using container environment variables. |
|K8s collection rules |* Namespace: Specify containers from which the logs are to be collected by namespace. Regular expressions are supported. For example, if you set the namespace name to `^default$`, the logs of all containers in the default namespace are to be collected.<br><br>* Workload type: Specify the workload types of the containers from which to collect logs, including Deployment, StatefulSet, DaemonSet, Job, and CronJob.<br><br>* Workload name: Specify containers from which the logs are to be collected by workload name. Regular expression matching is supported. For example, if you set the workload name to `^(http.*)$`, the logs of all containers in workloads whose names start with http are to be collected.<br><br>* Pod label allowlist and blocklist: You can specify specific containers whose logs are to be collected by using pod labels.<br><br>* Pod annotation allowlist and blocklist: You can specify containers whose logs are to be collected by using pod annotations.<br><br>* Pod name matching rule: Specify the names of pods whose logs are to be collected. Regular expression matching is supported. For example, if you set the pod name to `^(container-test)$`, the logs of all pods named `container-test` are collected. |





</Tab>
<Tab zoneid="gByDIk1W" title="Filter by content">
<TabTitle>Filter by content</TabTitle>

You can filter data by using log content fields. For example, only collect logs at the WARNING or ERROR level. Procedure:


1. When you configure a collection rule, enable **Filter** in the **Advanced settings** section.

2. Configure the filtering rule by using a regular expression. In this example, set the Key parameter to `__content__` and the Filter rule parameter to `WARNING`. This indicates that only logs containing the WARNING field will be collected. That is, logs at the WARNING level will be collected.


</Tab>
</Tabs>


<span id=".566h55CG6YeH6ZuG6KeE5YiZ"></span>
### Managing collection rules


1. In the left navigation bar of the cluster management page, click **Log management**. On the page that appears, click the **Log collection rule** tab to view collection rules.

2. In the collection rule list, click **Edit** or **Delete** in the **Actions** column to update or delete the corresponding collection rule.

   
   |Actions |Description |
   |---|---|
   |Edit |Update an existing log collection rule. |
   |Delete |Delete an existing log collection rule.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If the log\-collector add\-on has been upgraded to v1.1.0 or later, after you delete a log collection rule, the associated collection rule in the <a href="https://console.byteplus.com/tls">TLS console</a> will be automatically deleted. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the log\-collector add\-on has not been upgraded, after you delete a log collection rule, the content in the TLS console will not be affected.</div><br> |
   


&nbsp;

&nbsp;
