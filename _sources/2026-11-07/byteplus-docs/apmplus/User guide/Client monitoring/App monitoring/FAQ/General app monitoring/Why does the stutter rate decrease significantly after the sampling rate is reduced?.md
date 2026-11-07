---
title: "Why does the stutter rate decrease significantly after the sampling rate is reduced?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Why_does_the_stutter_rate_decrease_significantly_after_the_sampling_rate_is_reduced"
---

Stutter rate = number of stutters under the filter conditions / total number of PVs under the filter conditions. After adjusting the sampling rate, the total number of PV remains unchanged, and the number of stutter reports is directly proportional to the change in sampling rate. Therefore, if the sampling rate is reduced while PV remains unchanged, the stutter rate will decrease significantly.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For definitions related to PV metrics, refer to: <a href="https://docs.byteplus.com/en/docs/apmplus/App_metric_description">App\-side metrics description</a>.</div>
