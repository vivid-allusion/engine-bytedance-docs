---
title: "Instance diagnosis and network topology"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Instance-diagnosis-and-network-topology"
---

Through the Network Advisor, you can conduct diagnosis on Classic Load Balancer (CLB) instances to check for configuration omissions or identify network issues; you can also view the resource topology of CLB instances to clearly understand the resources associated with the CLB instances.

<span id=".5a-5Q0xC5a6e5L6L6L-b6KGM6K-K5pat"></span>
## Conduct diagnosis on CLB instances

The Network Advisor has organized the errors and omissions easily made during the configuration and operation of CLB into diagnosis items, such as resource status, health check configuration, listener configuration, etc. For more, please refer to [Classic Load Balancer diagnosis items](https://docs.byteplus.com/en/docs/NetworkAdvisor/Instance-Diagnostic-item).

For example, after configuring the Cloud Load Balancer, perform instance diagnosis on it. If a health check exception is found, locate the issue and discover that the Elastic Compute Service (ECS) in the newly added Server Group has not deployed services. Deploy the services and re\-diagnose; all diagnosis items pass.

For the procedure, please refer to [Creating instance diagnosis](https://docs.byteplus.com/en/docs/NetworkAdvisor/Managing-an-Instance-Diagnostics#.5Yib5bu65a6e5L6L6K-K5pat).

<span id=".5p-l55yLQ0xC55qE6LWE5rqQ5ouT5omR"></span>
## View the resource topology of the CLB

For the topology relationship between the CLB instance and its listeners and Server Groups, you can clearly and intuitively view it through the Network Advisor, as shown in the following figure.

For the procedure, please refer to [Viewing the resource topology of CLB](https://docs.byteplus.com/en/docs/NetworkAdvisor/Viewing-network-topology).
