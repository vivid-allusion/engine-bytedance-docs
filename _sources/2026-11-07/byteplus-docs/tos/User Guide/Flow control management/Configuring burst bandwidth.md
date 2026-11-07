---
title: "Configuring burst bandwidth"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Configuring_burst_bandwidth"
---

You can enable burst bandwidth when your workload temporarily requires higher performance than the default bandwidth limit. Once enabled, TOS automatically allocates additional temporary bandwidth based on actual usage and the applied burst bandwidth cap. This ensures smooth operation during periods of high usage while keeping bandwidth consumption within the predefined burst limit. This topic describes considerations for using burst bandwidth and provides steps to enable the feature.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">This feature is currently not supported in Asia Pacific (Johor).</div>


<span id="c786df71"></span>
## Notes


|**Category** |**Considerations** |
|---|---|
|Billing |You are charged based on your actual burst bandwidth usage and the duration of your usage. If your actual traffic does not exceed your bandwidth limit, TOS will not provide you with burst bandwidth and you will not be charged any fees for it. For more information, see [Burst bandwidth](https://docs.byteplus.com/en/docs/tos/Burst_bandwidth). |
|Activation criteria |Once enabled, burst bandwidth is provided automatically only when your traffic exceeds the limit. For more information about bandwidth limits, see [Constraints and limitations](https://docs.byteplus.com/docs/tos/docs-restrictions). |
|Effective time |You can enable or disable burst bandwidth at any time. Typically, configuration changes take effect within two minutes. |
|Constraints and limitations |* Burst bandwidth applies to your account's total bandwidth.<br><br>* Each BytePlus account can only configure one burst bandwidth rule per region.<br><br>* Essentially, burst bandwidth is extra bandwidth that becomes available based on the status of TOS online resources and their availability. Since it is provided on a best\-effort basis and does not come with a guaranteed commitment, there is a risk that it may not be available when needed. |


<span id="c6010ad4"></span>
## Use cases

Burst bandwidth responds automatically in real time with no cooldown period. It supports elastic scaling within the set performance limit according to business load and has no usage duration limit. Burst bandwidth is ideal for scenarios with large traffic fluctuations or unpredictable performance peaks.

<span id="727c1d2c"></span>
## Turning on burst bandwidth

Burst bandwidth is set and managed by region. Enabling burst bandwidth in a specific region helps handle sudden surges in service traffic.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **Throughput quota management**.

3. On the **Throughput quota management** page, click **Enable** under the **Burst bandwidth** column of the region you want to manage.

4. In the **Enable burst bandwidth** dialog, set the burst bandwidth limit. Then, click **OK** to save your settings.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The valid range is from 1 to 10 Gbps. <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245">Submit a ticket</a> to technical support if you need more bandwidth.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After enabling burst bandwidth, you can modify the limit by clicking <strong>Modify</strong> under the <strong>Burst bandwidth</strong> column on the <strong>Throughput quota management</strong> page for the corresponding region.   </div>
   


<span id="c69b671c"></span>
## Viewing burst bandwidth configurations


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **Throughput quota management**.

3. On the **Throughput quota management** page, view the **burst bandwidth status** **and limit** for each region.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Burst bandwidth includes both upload and download bandwidth, which have the same limit. For example, if you set the burst bandwidth limit to 10 Gbps, the upload and download burst bandwidths will both be capped at 10 Gbps. The upload and download bandwidths are described as follows:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Upload bandwidth: The bandwidth available for uploading data to TOS.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Download Bandwidth: The bandwidth available for downloading data from TOS.   </div>
   


<span id="7c694192"></span>
## Turning off burst bandwidth


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Flow control management** \> **Throughput quota management**.

3. On the **Throughput quota management** page, click **Delete** under the **Burst bandwidth** column of the region you want to manage.

4. In the box that appears, click **Delete**.


<span id="d55bfec6"></span>
## Next steps

<span id="93c912a6"></span>
### Viewing bandwidth metrics

Cloud Monitor collects and records upload and download bandwidth, as well as bandwidth quotas. In the Cloud Monitor console, you can view the upload and download bandwidth of the private and public networks for each region under your account. This helps you understand actual burst bandwidth usage and optimize resource configurations promptly.


1. Log in to the [Cloud Monitor console](http://console.volcengine.com/cloud-monitor/overview).

2. In the left navigation pane, select **Cloud product monitor**. Then, choose **TOS**.

3. In the top menu bar, select the region you want to check.

4. On the **user profile** tab, click **bandwidth**. Then, specify a time range to view the intranet inflow and outflow bandwidth and the user bandwidth quota for that period.

&nbsp;


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b4cfab68befff161719445abc06d140.png) </span>

&nbsp;
