---
title: "Modifying a server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Modifying-the-server-group"
---

After creating the server group, you can modify its basic information (including name, scheduling algorithm, session persistence, connection draining, client IP preservation, Proxy Protocol), edit the health check configuration, and manage the backend servers within the server group as needed.

<span id=".5L-u5pS55Z-65pys5L-h5oGv"></span>
## Modify basic information

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After modifying client IP address preservation, it only applies to new connections.</div>



1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation pane, select **Server Group**.

3. In the top menu bar, select the target project and region.

4. Click Edit basic information on the right side of the target server group and modify related information as needed.

   For parameter descriptions, see Creating a server group.

5. Click **OK** to complete the action.


<span id=".57yW6L6R5YGl5bq35qOA5p-l"></span>
## Edit health check


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation pane, select **Server Group**.

3. In the top menu bar, select the target project and region.

4. Click Edit health check next to the target server group, and modify the health check information as needed.

   For parameter descriptions, see Creating a server group.

5. Click **OK** to complete the action.


<span id=".566h55CG5ZCO56uv5pyN5Yqh5Zmo"></span>
## Manage server

<span id=".5L-u5pS55ZCO56uv5pyN5Yqh5Zmo56uv5Y-j44CB5p2D6YeN"></span>
### Modify server port and weight


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation pane, select **Server Group**.

3. In the top menu bar, select the target project and region.

4. Click the target server group name and select the Server tab.

   * **Modify individually**: Click the edit icon to the right of the port or weight.

   * Batch settings: When multiple backend servers provide services with the same port or weight, select the target servers and click Modify port or Modify weight.

      A maximum of 100 backend servers can be modified in a single batch operation.

5. Click **OK** to complete the action.


<span id=".56e76Zmk5ZCO56uv5pyN5Yqh5Zmo"></span>
### Remove server

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Removing a backend server only detaches it from the NLB instance and does not delete the server.</div>



1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the left navigation pane, select **Server Group**.

3. In the top menu bar, select the target project and region.

4. Click the target server group name and select the Server tab.

   * Single removal: Click Remove to the right of the target server.

   * Batch removal: Select the target server and click Remove above the list.

5. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyNLBServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBServerGroupAttributes)

* [ModifyNLBBackendServersAttributes](https://docs.byteplus.com/en/docs/clb/ModifyNLBBackendServersAttributes)

* [RemoveNLBBackendServers](https://docs.byteplus.com/en/docs/clb/RemoveNLBBackendServers)
