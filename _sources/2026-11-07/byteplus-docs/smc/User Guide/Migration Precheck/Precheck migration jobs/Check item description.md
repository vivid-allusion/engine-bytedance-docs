---
title: "Check item description"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Precheck_item_description"
---

This topic provides a summary of the check items supported by the pre\-check feature for migration tasks, corresponding repair solutions, and related information.

<span id=".572R57uc5qOA5rWL"></span>
## Network check

<span id=".572R57uc6L-e6YCa5oCn5qOA5p-l"></span>
### Network connectivity check


|Exception type |Check item/CheckCode |Description |Repair suggestion |
|---|---|---|---|
|Severe |Port check/PortCheck |Checks whether the security group rule of the target instance allow network requests from the source instance. |Check IP connectivity and security group configuration of the target instance by following the guidance in the [solution](https://docs.byteplus.com/en/docs/smc/Solutions_to_network_issues#.5qOA5p-l572R57uc6L-e6YCa). |
||Proxy check/ProxyCheck |Checks whether the proxy service can access the target instance when the proxy mode is enabled. |Check and modify the source server variables `http_proxy` and `https_proxy` by following the guidance in the [solution](https://docs.byteplus.com/en/docs/smc/Solutions_to_network_issues#.5qOA5p-l572R57uc5Luj55CG). |
||Service connectivity/ServiceCheck |Checks service connectivity between the source server and the target server. |Check whether the dependent network services are running properly as indicated. |


<span id=".572R57uc6LSo6YeP5qOA5p-l"></span>
### Network quality check


|Exception type |Check item/CheckCode |Description |Repair suggestion |
|---|---|---|---|
|Warning |Network bandwidth/ThroughputCheck |Checks the current migration bandwidth. An alert is triggered when the bandwidth falls below 5 Mbit/s. |It is recommended to increase the target bandwidth or check the transmission speed limit. |
||Network latency/LatencyCheck |Checks the current network latency.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the network latency exceeds 50 ms, this item will be diagnosed as <strong>Warning</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the network latency exceeds 100 ms, this item will be diagnosed as <strong>Serious</strong>.</div><br> |Reduce the network latency by following the guidance in the [solution](https://docs.byteplus.com/en/docs/smc/Solutions_to_network_issues#.5qOA5p-l572R57uc6LSo6YeP). |
||Network latency standard deviation/StdDevRttCheck |Checks the current network jitter (standard deviation round\-trip time). |Switch to an ISP type offering higher quality to reduce network jitter by following the guidance in the [solution](https://docs.byteplus.com/en/docs/smc/Solutions_to_network_issues#.5qOA5p-l572R57uc6LSo6YeP). |
||Network packet loss rate/PacketsLossCheck |Checks the current network packet loss rate.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the network packet loss rate exceeds 0.1% but not higher than 1%, this item will be diagnosed as <strong>Warning</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the network packet loss rate exceeds 1%, this item will be diagnosed as <strong>Serious</strong>.</div><br> |Switch to an ISP type offering higher quality to reduce the packet loss rate by following the guidance in the [solution](https://docs.byteplus.com/en/docs/smc/Solutions_to_network_issues#.5qOA5p-l572R57uc6LSo6YeP). |
