---
title: "Alert center"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Alert_center"
---

In Volcano Engine E\-MapReduce (EMR) cluster versions 3.2.1 / 2.2.0 and later, the alarm functionality module is managed by the cloud monitoring product. .

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the cloud monitoring console, when creating an EMR cluster alarm policy, you can use the options in <strong>resource \> Cluster \> section</strong> to specify the target cluster. For some metrics, selecting <strong>All</strong> resources may generate unnecessary alarm content.</div>


The EMR console provides a page for quickly viewing the alarm history of the corresponding cluster. You can go to **Cluster details \>**  **Alert center**the tab to view. The display is as follows:

**Explanation of the parameters in the table:** 


|Parameter item |Note |
|---|---|
|Rule name |Corresponds to the alarm rule name configured in cloud monitoring, and supports hyperlinks. You can click the specific rule name to jump and view the rule definition. |
|Dimension |The dimension classification where the alarm is generated, specific to the service itself. |
|Status |Divided into **In alarm** and **Recovered** types, and supports filtering. |
|Rule description |Indicates the configuration content of the rule. |
|Affected resource |Indicates the resource associated with the alarm, such as a specific host. |
|First alarm occurrence time |Indicates the time when the alarm history entry was generated after the resource triggered the alarm. |
|Duration |* If the alarm status is **Normal**, it indicates the duration from when the resource triggered this alarm history entry to when it returned to normal.<br><br>* If the alarm status is **In alarm**, it indicates the duration from when the resource triggered this alarm history entry until now. |
|Alarm level |Divided into **notice, warning, critical** levels, and supports filtering. |
