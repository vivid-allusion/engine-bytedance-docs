---
title: "Configure service traffic policy"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Configure_service_traffic_policy"
---

<span id="操作步骤"></span>
# Procedure

<span id="分流策略"></span>
## triage strategy

Through the traffic segmentation function, you can implement a variety of service release strategies such as blue\-green release and grey release.

When there are ≥ `2`deployments in the service, you can choose to configure the "offloading policy" on the task details page to implement the traffic distribution of the service across multiple deployments. When the traffic policy is configured and deployed `in the running`state, the `traffic ON`label will appear, otherwise it is the `traffic OFF`label.


|Parameter |Parameter Description |
|---|---|
|API gateway |The API gateway supports only one offloading strategy, "custom offloading".<br><br><br>* Custom offloading: You need to specify a weight for each deployment, the default weight for the first new deployment is `10`, and the default weight for subsequent new deployments is 0. The input range is `"0-10"`. The estimated traffic ratio is calculated as the estimated traffic ratio of deployment A = deployment A weight/SUM (deployment A weight, deployment B weight,...)<br><br>* When the service is not initially configured with an API gateway, select Update to add a configuration API gateway, and the default deployment weight is 1.<br><br>* When switching from the CLB (the offloading policy is "auto offloading by instance") to the API gateway, the default deployment weight is 1. |
|CLB |The CLB (Transport Layer Load Balancer) supports two offloading strategies, Automatic offloading by instance and Custom offloading.<br><br><br>* Automatic offloading by instance: that is, traffic is automatically allocated based on the number of instances in each deployment. Example: If Deployment A has `6`instances running and Deployment B has `4`instances running, `60%`of the request traffic will be sent to Deployment A for processing, and `40%`of the traffic will be processed by Deployment B.<br><br>* Custom offloading: that is, it supports freely specifying the weight coefficient of each deployment, and distributes traffic according to the proportion of the number of instances \* weight coefficient. The detailed calculation formula is: `deployment A = number of running instances * deployment weight`, deployment A estimated traffic ratio = `deployment A/SUM (deployment A, deployment B, deployment... N)`. For detailed weight factor configuration, please go to "Service Details" \- "Diversion Policy" to configure after the service is created.<br><br>   * Note: If the load balance scheduling algorithm of the service selects "weighted minimum number of connections ( `WLC`) " and "source address hash ( `SH`) ", the expected traffic ratio will be different from the actual traffic ratio due to the influence of the number of connections in the policy and the source address IP factors. |


<span id="流量镜像"></span>
## Flow mirror

Before the new deployment (new version) is officially released, you can use the "traffic mirror" function to test and compare the business capacity and performance of the new deployment and the existing deployment. When using the "traffic mirror" function, select a deployment (old deployment) as the source deployment and configure a certain percentage of mirror traffic for testing. Traffic during the mirroring process does not affect the online traffic carried by the source deployment and does not place additional load pressure on it.

After the mirror function is enabled, all you need to do is select any deployment under the service as the source deployment and any deployment as the target deployment. And choose to configure a certain percentage of traffic for mirroring.

For example, if A is deployed as the source and B is deployed as the target, the proportion of the selected configuration mirror traffic is 50%. Then the final A deployment undertakes 100% of the online traffic, and the B deployment undertakes 50% of the mirror test traffic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If traffic mirroring is enabled, the source deployment needs to be adjusted to handle 100% of the live traffic on the line.</div>


* <div data-tips="true" data-tips-type="tip">The source deployment and the target deployment cannot choose the same deployment.</div>


* <div data-tips="true" data-tips-type="tip">If either the source deployment or the target deployment is deleted, the traffic mirroring function is automatically terminated and turned off.</div>
