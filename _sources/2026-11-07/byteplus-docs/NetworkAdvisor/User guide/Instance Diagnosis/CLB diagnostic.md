---
title: "CLB diagnostic"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/CLB_diagnostic_items"
---

This topic introduces diagnostic items for Classic Load Balancer (CLB).


|**Module** |**Item Category Name** |**Item Name** |**Abnormal Result** |**Item Status** |**Recommendation** |
|---|---|---|---|---|---|
|Instance Information Diagnosis |Resource status |Check instance status |Active |Pass |\-\- |
||||Inactive |Fatal |Resource is in intermediate state. Please try again later. |
||||Creating、Configuring、Deleting |Hint ||
||||Creation failed |Normal ||
||Arrears alert |Check if instance is in arrears |Not overdue |Pass |\-\- |
||||Instance overdue and suspended |Fatal<br><br> |Account overdue, please recharge promptly to ensure normal resource usage. [Cost Center - Account Recharge](https://console.byteplus.com/finance/fund/recharge) |
||||*Instance overdue and reclaimed* |Fatal ||
||Expiration warning |Check if instance is expired |Instance expiration \> 7 days |Pass |\-\- |
||||3 < Instance expiration <= 7 days |Hint |Instance expiring soon. Please renew promptly to ensure normal resource usage. [Cost Center - Renewal Management](https://console.byteplus.com/finance/renew/) |
||||Instance expires in < 3 days |Normal ||
||||Instance expired and suspended |Fatal |Instance expired, please recharge promptly to ensure normal resource usage. [Cost Center - Renewal Management](https://console.byteplus.com/finance/renew/) |
||||Instance expired and reclaimed |Fatal ||
||Quota check |Check maximum number of listeners addable per CLB instance |CLB listener quota utilization <=80% |Pass |\-\- |
||||CLB listener quota utilization \>80% |Normal |Increase quota promptly to avoid business impact. [CLB - Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=CLB) |
||||CLB listener quota 100% allocated |Serious ||
|||Check per CLB instance backend server group quota |CLB backend server group quota utilization <=80% |Pass |\-\- |
||||CLB backend server group quota utilization \>80% |Normal |Increase quota promptly to avoid business impact. [CLB - Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=CLB) |
||||CLB backend server group quota 100% allocated |Serious ||
|||Check maximum backend server associations per CLB instance |CLB backend server association quota utilization <=80% |Pass |\-\- |
||||CLB backend server association quota utilization \>80% |Normal |Increase quota promptly to avoid business impact. [CLB - Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=CLB) |
||||CLB backend server association quota 100% allocated |Serious ||
|Health Check Diagnosis |Check health check configuration status |Check if health check is configured for CLB listener |CLB listener has health check configured |Pass |\-\- |
||||CLB instance currently has no listener configured |Pass ||
||||CLB listener has no health check configured<br><br> |Hint |Configure health checks for CLB listeners to avoid impact from backend failures.  |
||Health check anomaly detection |Check if CLB listener health check is abnormal<br><br> |CLB listener health check normal |Pass |\-\- |
||||CLB instance currently has no listener configured |Pass ||
||||CLB listener health check abnormal |Hint |Backend server groups are abnormal. Adjust and fix promptly.<br><br><br>* No\-target listeners: No servers configured in associated backend server groups. Configure promptly.<br><br>* Abnormal listeners: See [Health check troubleshooting guide](https://docs.byteplus.com/en/docs/clb/Troubleshooting-health-check-exceptions) |
|Configuration Diagnosis |Listener configuration check |Check if CLB instance has listeners configured<br><br> |CLB instance has listeners configured |Pass |\-\- |
||||CLB instance currently has no listener configured |Hint |Configure listeners for CLB instance to ensure proper traffic distribution |
||Backend server configuration check |Check if CLB instance has backend servers configured |CLB instance has backend servers configured |Pass |\-\- |
||||CLB instance has no backend server configured |Hint |Configure backend servers for CLB listeners to ensure proper traffic distribution |
|Specification Exceedance Diagnosis |CLB Bandwidth Utilization<br><br> |Check CLB Instance Bandwidth Utilization |CLB instance inbound and outbound bandwidth utilization <=80% |Pass |\-\-<br><br> |
||||CLB instance inbound and outbound bandwidth utilization \>80% |Serious |\-\- |
||||This instance is an exclusive cluster instance and shares the cluster's network performance. No instance\-level specification limit is currently applied. |Pass |\-\- |
||Maximum supported connections |Check if the CLB instance is dropping connections or new connection count exceeds 85% of the limit |Connection drops on CLB instance or new connections <=85% |Pass |\-\- |
||||CLB instance concurrent connections \>85% |Serious |High new connection usage may cause random connection drops. To ensure normal operation, consider upgrading specs promptly. |
||||This instance is an exclusive cluster instance and shares the cluster's network performance. No instance\-level specification limit is currently applied. |Pass |\-\- |
||Maximum queries per second<br><br> |Check if the CLB instance is dropping connections or if query request watermarks exceed 85% of the limit<br><br> |CLB instance query request watermark <=85% |Pass |\-\- |
||||CLB instance query request watermark \>85%<br><br> |Serious |High query request watermark may cause random connection drops. To ensure normal operation, consider upgrading specs promptly. |
||||This instance is an exclusive cluster instance and shares the cluster's network performance. No instance\-level specification limit is currently applied. |Pass |\-\-<br><br> |
|Security Policy Diagnosis |EIP security lock check |Check Whether CLB Instance Bind EIP Is Locked Due to Blocking<br><br> |EIP bound to CLB instance is not security\-blocked |Pass |\-\- |
||||CLB instance not bound to EIP |Pass ||
||||EIP bound to CLB instance is security\-blocked<br><br> |Fatal |EIP bound to CLB instance is security\-blocked due to violations. Operations prohibited. Monitor service status promptly. |
|Listening Diagnosis<br><br> |Listener status check<br><br> |Check listener status |Listener not configured |Pass |\-\- |
||||Listener running |Pass ||
||||Listener disabled |Hint |Listener disabled. Stopped listeners will no longer receive or forward client requests. Enable promptly. |


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For some CLBs of specific beta specifications, the Network Advisor (NA) cannot perform diagnostics on items such as CLB inbound/outbound bandwidth utilization, maximum supported connections, maximum new connections per second, and maximum queries per second. The diagnostic report will indicate Diagnostic Item Execution Exception. Please navigate to the monitoring page to view relevant data. For specific steps, see <a href="https://docs.byteplus.com/en/docs/clb/Viewing-monitoring-data">Viewing the monitoring data</a>.</div>
