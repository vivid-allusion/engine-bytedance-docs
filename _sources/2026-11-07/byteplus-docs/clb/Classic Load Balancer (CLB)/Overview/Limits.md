---
title: "Limits"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Product-Overview-07"
---

This topic introduces the quota limits for a single bill per region for Classic Load Balancer (CLB). For more information, see Quota overview.

## Limits

When client address is maintained on backend servers, if a client simultaneously accesses multiple VIPs/EIPs of CLB and Network Load Balancer (NLB) instances mounted on the same backend server, five\-tuple conflicts may occur on the backend server.

## Quota limitations

> **tip**

> The quota items in the table below support adjustments. If the default quota cannot meet your needs, you can go to Quota Center to apply for an increase.

## Quota limitations

|Network resource |Quota parameter |Description |Maximum |Support adjustment |Adjustable quota limit |
|---|---|---|---|---|---|
| <br><br> <br><br> <br><br> <br><br> <br><br> <br><br> <br><br>CLB instance |InstanceNumber |Maximum number of CLB instances created per account per region |60 | <br><br> <br><br> <br><br> <br><br> <br><br> <br><br>Yes<br><br> |120 |
||ServerNumberEachInstance |Number of backend servers that can be associated to a single CLB instance<br><br>> **tip**<br><br><br>> If the same backend server is added to multiple backend server groups of a CLB instance, it will occupy multiple backend server quotas.<br> |200 ||400 |
||ListenerNumberEachInstance |Number of listeners supported for addition to a single CLB instance |Please go to Quota Center to view ||100 |
||ServerGroupNumberEachInstance |Number of backend server groups that can be created for a single CLB instance |200 ||300 |
||None |Maximum number of custom tags allowed per CLB instance |50 |No |\-\- |
| <br><br> <br><br>Listener |RuleNumberEachListener |Maximum number of forwarding rules supported per single HTTP or HTTPS listener<br><br>> **tip**<br><br><br>> Default forwarding rules are not included.<br> |Please go to Quota Center to view |Yes |100 |
||none |Number of access control list groups that can be associated with a single listener |5 |No |\-\- |
| <br><br> <br><br>Access control |AclNumber |Number of access control lists that can be created per account per region |Please go to Quota Center to view | <br><br>Yes<br><br> |400 |
||ListenerNumberEachAcl |Number of listeners supported for association with a single access control list |50 ||100 |
||none |Number of IP entries that can be added to a single access control list |300 |No |\-\- |
|Certificate |CertificateNumber |Number of certificates that can be uploaded per account per region |Please go to Quota Center to view |Yes |200 |
|server group |None |Number of backend servers supported for addition to a backend server group in a single operation |40 |No |\-\- |
