---
title: "Analyzing a flow log"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Analyzing-a-flow-log"
---

<span id="fPxzryxc"></span>
## Prerequisites


* Flow logs are active. If not, see [Starting/Stopping a flow log](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-a-flow-log).

* The index for the log topic has been correctly configured. For detailed operations, see [Configuring index](https://docs.byteplus.com/en/docs/vpc/Configuring-an-index).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Flow Log**.

3. In the top menu bar, select the target project and region.

4. Click the topic name under the **Log topic** column of the target flow log.

5. Click the search and analysis icon to the right of the target log topic.

6. Input the search and analysis statement, and click **Search** to view the analysis results.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A search and analysis statement consists of a search statement and an SQL analysis statement, separated by a pipe symbol (|). This syntax indicates that data statistics and analysis are performed on the results that match the search conditions.    </div>
   

   * Query Results Section: Displays essential information or an overview of the current log analysis. 

   * View Raw Data: Click the **Raw log** tab to view the raw data retrieved from your search and analysis.

   * View Chart Analysis: Click the **Chart analysis** tab to view the chart analysis results. Query analysis results are displayed in a tabular format by default. You can also choose to present them as other types of statistical charts and configure the corresponding chart settings. 


<span id=".5L2_55So56S65L6L"></span>
## Usage example

For scenarios and example statements of flow log search and analysis, see [Usage example](https://docs.byteplus.com/en/docs/vpc/Use-cases).
