---
title: "Create a route"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_a_route"
---

By using the add route feature, requests that meet the rules can be distributed to multiple target upstreams according to the configured traffic weight, supporting scenarios such as application multi\-version management. This article describes how to create a route.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Performing scale\-in operations on the VKE side may cause transient traffic fluctuations lasting for several seconds in routes of  Service type upstreams. Please proceed with caution.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A service has been created. For details, refer to [Create Service](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

* An upstream has been created. For details, refer to [Upstream management](https://docs.byteplus.com/en/docs/apig/Upstream_Management).

* To manage multiple versions of  Service type upstreams, configure upstream versions in advance. For details, refer to [Manage  Service type upstream versions](https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* Each route supports connecting to up to 10 upstreams.

* If multiple route rules have overlapping paths, requests from overlapping paths will be forwarded to the earliest created route.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5Yib5bu65Y2V5Liq5pyN5Yqh55qE6Lev55Sx"></span>
### Create a route for a single service

When creating a route, you can create a single route for the service on the service configuration page.


1. Log in to [API Gateway Console ](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. After selecting the target instance from the **Instance management** dropdown, click **Route list**. 

4. In the route information area, click **Create route** and configure the route information.

   * **Basic Information**

      
      |Parameter |Description |
      |---|---|
      |Route name |Custom route name. Route names must be unique within the same service. |
      |Service |Displays the service name to which the current route belongs. Modification is not supported. |
      |Matching rules |Configure matching rules. Only requests that meet the rules can be forwarded to the target Upstream.<br><br><br>* **Request method**: Only requests that match the specified method are allowed to access. Supports GET, POST, PUT, DELETE, HEAD, OPTIONS, and more request methods.<br><br>* **Path**: Specify the request path that is allowed to access. Supports three matching methods. For example, please refer to [Path matching example](https://docs.byteplus.com/en/docs/apig/Creating_a_route#.6Lev5b6E5Yy56YWN56S65L6L).<br><br>   * **Equal to**: The request path must be exactly the same as the configured path for the request to be forwarded.<br><br>   * **Regular Expression Match**: The request path must match the configured path's regular expression for the request to be forwarded.<br><br>   * **Prefix matching**: The request path will be forwarded as long as it matches the beginning of the configured path.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The priority of Path, from highest to lowest, is: exact matching \> prefix matching \> regular expression matching.</div><br><br><br><br>* **Request header Header**: Only requests containing the specified request header Header are allowed. Supports adding multiple request headers.<br><br>   * **Header key**: Supports English letters, numbers, hyphens`-`, and underscores`_`.<br><br>   * **Matching type**: Specifies the matching method for the Header. Supports **exact matching**, **regular expression matching**, and **prefix matching**.<br><br>   * **Header value**: Validates the ASCII code range.<br><br>* **Request parameter QueryString**: Only requests containing the specified request parameter are allowed. Supports adding multiple request parameters.<br><br>* **Priority**: Enter the priority of the route matching rule. The value is an integer. Valid values: 0 to 100. The smaller the number, the higher the priority. The higher the accuracy of the matching rule, the higher the priority.<br><br>   For example, `path:/abc`, `header:version=v1` has a priority higher than `path:/abc`, regardless of creation time. |
      |Edit request header |Supports editing the original request header during forwarding, and forwards the modified header to the backend service connected to the gateway. Supports the following three modification modes. After selecting the corresponding mode, please fill in the required key and value as prompted by the interface. The value cannot be empty.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Duplicate Header keys are not supported. If a request contains multiple identical keys, multiple values can be merged into one and separated by a comma (;).</div><br><br><br><br>* **Overwrite (set)** : If the client sends a request header without the corresponding key, a new header will be added; if the corresponding key is already present, the value of that key will be overwritten by the value configured on the API Gateway side.<br><br>* **Add (add)** : If the client does not include the corresponding key in the request header, add a new Header; if the corresponding key is already included, append the value configured on the API Gateway side to the value of this key.<br><br>* **Remove (remove)** : If the client includes the corresponding key in the request header, delete this field. After choosing the remove mode, only the corresponding key needs to be entered. |
      

   * **Upstream traffic distribution**

      Traffic distribution is used to route data streams to different upstreams based on traffic weight. Click  **+**  to add an upstream. You can add up to 10 upstreams.

      
      |Parameter |Description |
      |---|---|
      |Upstream type |Choose the Upstream type to connect; currently supports function services, Cloud Service, , fixed domain name, and registry. |
      |Choose Upstream |Choose the specific Upstream to connect to. |
      |Weight |Configure the traffic weight of the current Upstream. Integer format, value range is 1–1000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The system displays traffic allocation proportionally according to the total weight configured for the Upstream and the percentage of each Upstream's overall proportion, with percentage values accurate to two decimal places.</div><br> |
      |Canary label |For Upstream of  type, routing to a specific version of the application is supported. Workload on the  side supports distinguishing different canary versions through configured Labels, which is used to meet the application's multi\-version management requirements. If no canary label is selected, routing to the specific version of the current application will be determined according to the load balancing strategy. For specific usage, please refer to [Managing versions of Upstream for  type](https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types). |
      |Fallback |After the fallback capability is enabled, if the original backend returns a 4xx or 5xx HTTP status code, the gateway will automatically forward the original request to the fallback upstream and return its response to the client. |
      

6. Click **Confirm** to complete route creation.


<span id=".5om56YeP5Yib5bu66Lev55Sx"></span>
### Batch create routes

When creating routes, you can batch create routes for multiple services in the route list.


1. Log in to [API Gateway Console ](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **Route management \> Route list**. Click **Create route** and configure the route information.

   * **Basic Information**

      
      |Parameter |Description |
      |---|---|
      |Route name |Custom route name. The route name must be unique within the same service. |
      |Associated service |Configure the service to which the route belongs. Multiple selection is supported, allowing quick creation of multiple routes. |
      |Matching rules |Configure matching rules; only requests that meet the rules can be forwarded to the target Upstream.<br><br><br>* **Request method**: Only requests that match the specified method are allowed to access. Supports GET, POST, PUT, DELETE, HEAD, OPTIONS, and many other request methods.<br><br>* **Path**: Specify the request path that is allowed to access. Supports three matching methods; for example, refer to [Path matching examples](https://docs.byteplus.com/en/docs/apig/Creating_a_route#.6Lev5b6E5Yy56YWN56S65L6L).<br><br>   * **Exact matching**: The request path must be exactly the same as the configured path for the request to be forwarded.<br><br>   * **Regular Expression Match**: The request path must match the configured path's regular expression for the request to be forwarded.<br><br>   * **Prefix matching**: The request path will be forwarded as long as it matches the beginning of the configured path.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The priority of Path is, from high to low: Exact matching \> Prefix matching \> Regular Expression Match.</div><br><br><br><br>* **Header**: Only requests that include the specified request Header are allowed to access. Supports adding multiple request Headers.<br><br>   * **Header key**: Supports English letters, numbers, hyphens`-`, and underscores`_`.<br><br>   * **Matching type**: Specify the matching method for the Header; supports **Exact matching**, **Regular Expression Match**, and **Prefix matching**.<br><br>   * **Header value**: Checks the ASCII code range.<br><br>* **Request parameter**: Only requests that include the specified access parameters are allowed to access. Supports adding multiple request parameters.<br><br>* **Priority**: Enter the priority of the route matching rule. The value is an integer. Valid values: 0 to 100. The smaller the number, the higher the priority. The higher the accuracy of the matching rule, the higher the priority.<br><br>   For example, `path:/abc`, `header:version=v1` has a higher priority than `path:/abc`, regardless of creation time. |
      |Modify request header |Supports editing the original request Header during forwarding, and forwards the modified Header to the Backend service connected to the gateway. Supports the following three modification modes. After selecting the corresponding mode, please fill in the required key and value as prompted by the interface. The value cannot be empty.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Duplicate Header keys are not supported. If there are multiple identical keys in the request, you can merge multiple values into one and separate them with a semicolon (;).</div><br><br><br><br>* **Overwrite (set)** : If the client does not include the corresponding key in the request header, a new Header will be added. If the key is already included, the value of that key will be overwritten by the value configured on the API Gateway side.<br><br>* **Append (add)** : If the client does not include the corresponding key in the request header, a new Header will be added. If the key is already included, the value configured on the API Gateway side will be appended to the value of that key.<br><br>* **Remove (remove)** : If the client includes the corresponding key in the request header, this field will be deleted. After selecting the remove mode, only the corresponding key needs to be filled in. |
      

   * **Upstream traffic distribution**

      Traffic distribution is used to route data streams to different Upstreams based on traffic weight. Click  **+**  to add an Upstream. You can add up to 10 Upstreams.

      
      |Parameter |Description |
      |---|---|
      |Upstream type |Choose the type of Upstream to access. Currently supported types are function services, cloud server, , fixed domain name, and registry. |
      |Choose Upstream |Choose the specific Upstream to connect to. |
      |Weight |Configure the traffic weight of the current Upstream. Integer format, value range is 1–1000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The system will display the traffic allocation proportionally according to the total weight configured for Upstream and the percentage of each Upstream stack. The percentage is accurate to two decimal places.</div><br> |
      |Canary label |For Upstream of  type, routing to a specific version of the application is supported. Workload on the  side supports distinguishing different canary versions through configured Labels, which is used to meet the application's multi\-version management requirements. If no canary label is selected, routing to the specific version of the current application will be determined according to the load balancing strategy. For specific usage, please refer to [Managing versions of Upstream for  type](https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types). |
      |Fallback |After the fallback capability is enabled, if the original backend returns a 4xx or 5xx HTTP status code, the gateway will automatically forward the original request to the fallback upstream and return its response to the client. |
      

4. Click **Confirm** to finish creating the route.


<span id=".6Lev5b6E5Yy56YWN56S65L6L"></span>
## Path matching example

Path matching example, as shown in the table below.


|<div style="text-align: center"><br>Matching method</div><br> |<div style="text-align: center"><br>Request path</div><br> |<div style="text-align: center"><br>Set path</div><br> |||
|---|---|---|---|---|
|||<div style="text-align: center"><br>/apig/test.jpg</div><br> |/apig |/apig[^\s]\* |
|<div style="text-align: center"><br>equal to</div><br> |<div style="text-align: center"><br>/apig/test.jpg</div><br> |<div style="text-align: center"><br>√</div><br> |\- |\- |
|<div style="text-align: center"><br>Regular Expression Match</div><br> ||<div style="text-align: center"><br>√</div><br> |\- |√ |
|<div style="text-align: center"><br>Prefix matching</div><br> ||<div style="text-align: center"><br>√</div><br> |√ |\- |
