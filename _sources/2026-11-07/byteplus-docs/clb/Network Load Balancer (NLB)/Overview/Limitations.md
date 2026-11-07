---
title: "Limitations"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Constraints"
---

This article introduces default limits on resources related to Network Load Balancer (NLB).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* When client address preservation is enabled for the server group, if the client simultaneously accesses multiple VIPs/EIPs of CLB and NLB instances mounted on the same backend server, 5\-tuple conflicts may occur on the backend server.

* In scenarios where NLB instances use the LIP (Local IP) address as the source address for traffic forwarding, it supports approximately 120,000 concurrent connections by default for a single backend server (unique combination of IP+port). Exceeding this threshold increases the likelihood of port allocation errors. It is recommended to add more backend servers to the server group at this time.

* Each certificate bound to a listener can associate with a maximum of 64 domain names, with the total length of domain names (Common Name + Subject Alternative Names) not exceeding 16,384 bytes.


<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota limitations

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The adjustable quota items in the table below can be increased at BytePlus <a href="https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=CLB">Quota Center</a> if the default quotas are insufficient.</div>



|Network resource |Quota parameter |Description |Maximum |Support adjustment |Adjustable quota limit |
|---|---|---|---|---|---|
|&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>&nbsp;<br><br>NLB instance |NLBInstanceNumber |The number of NLB instances that can be created per account per region |60 |&nbsp;<br><br>&nbsp;<br><br>Yes<br><br> |120 |
||NLBListenerNumberEachInstance |Number of listeners that can be added to a single NLB instance<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Includes single\-port and full\-port listeners</div><br> |50 ||100 |
||None |Number of full\-port listeners per NLB instance |5 |If the default quota does not meet your needs, contact customer service support |\-\- |
||None |The number of security groups that can be associated with a single NLB instance (including the system's default entrusted security group) |5 |Yes |\-\- |
|&nbsp;<br><br>&nbsp;<br><br>Certificate |NLBAdditionalCertificateNumberEachListener |Number of additional certificates per TLS listener |25 |Yes |50 |
||None |Number of CA certificates per TLS listener |1 |&nbsp;<br><br>No<br><br> |\-\- |
||None |Number of default certificates per TLS listener |1 ||\-\- |
|&nbsp;<br><br>&nbsp;<br><br>Server Group |NLBServerGroupNumber |Number of server groups a single account can create in a single region |3000 |Yes |4000 |
||NLBServerNumberEachServerGroup |The number of backend servers that can be added to a single server group |400 |&nbsp;<br><br>Yes<br><br> |600 |


&nbsp;

&nbsp;

&nbsp;

&nbsp;
