---
title: "Creating Mock routes"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating-Mock-routes"
---

A route is used to match incoming requests and apply the corresponding traffic handling policy. It supports forwarding requests to multiple target Upstreams based on weight, returning a custom Mock response, or redirecting requests directly to a specified address. It is suitable for scenarios such as multi\-version traffic management and API joint debugging. This topic describes how to create Mock routes.

## Background information

A Mock route is a type of route that returns a preset response directly from API Gateway. After a request matches the matching rules of a Mock route, API Gateway does not forward the request to the backend Upstream. Instead, it directly returns the pre\-configured response status code and response body to the client.

Mock routes are suitable for scenarios where the backend API is still under development, the backend service is temporarily unavailable, or you need to simulate a specific status code and response content. With Mock routes, frontend, client, and test engineers can perform API joint debugging and feature verification without waiting for the actual backend service or deploying a temporary Mock service. This helps reduce frontend\-backend dependency and shortens the joint debugging cycle.

## Prerequisites

A service has been created. For details, see [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

## Limits

* When multiple routing rules exist, they are sorted in descending order of priority: ** custom priority** \> ** path ** \> **header \> request parameter (Query) ** \> **creation time**. If multiple routing rules have overlapping path configurations with the same priority, requests from the overlapping paths are forwarded to the route that was created first. For details about route matching priority, see [Route overview](https://docs.byteplus.com/en/docs/apig/Priority_of_route?lang=en#mLNoepXu).

* When the usage scenario is set to "Mock", the advanced setting supports only CORS configuration.

## Procedure

When creating a route, you can create one route for a service on the service configuration page. You can create routes in a batch for multiple services in the route list.

1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. Select the target instance from the ** Instance management ** drop\-down list. In the left navigation pane, select **Service list (Domain name)** . On the service list page, click **Add route** in the **Actions** column of the target service.

4. On the **Add route** page, configure the route information.

   * **Basic information, usage scenarios, and matching rule(s)**

      |Parameter |Description |
      |---|---|
      |Route name |The custom name of the route. The route name must be unique within the same service. |
      |Service |Configure the service to which the route belongs. You can select multiple services to quickly create multiple routes. |
      |Application scenarios |Select the execution scenario of the route. The values are as follows. In this example, select **Mock, ** which indicates that a Mock route is configured.<br><br>> **tip**<br><br><br>> The usage scenario can be selected only when a single route is created for a service on the service configuration page.<br> |
      |Matching rule |Configure matching rules. Only requests that match the rules can be forwarded to the target Upstream.<br><br><br>* **Request method**: Allows access only to requests that match the specified method. The following methods are supported.<br><br>   * **GET**: Queries resource information and is used to obtain resource details.<br><br>   * **POST**: Submits request data. It is typically used to add or create business resources, and can also be used to trigger various business operations such as pausing a task or applying a configuration.<br><br>   * **PUT**: Replaces the specified resource in full.<br><br>   * **DELETE**: Deletes the target resource.<br><br>   * **HEAD**: Queries resource information and returns only the response headers, not the response body.<br><br>   * **OPTIONS**: Queries metadata such as the HTTP request methods supported by the target endpoint and its CORS policy.<br><br>   * **PATCH**: Performs an incremental update on a resource, modifying only the changed fields.<br><br>   * **CONNECT**: Establishes a TCP network tunnel, which is commonly used for HTTPS proxy tunneling.<br><br>* **Path**: Specifies the request path allowed for access. Three matching methods are supported. For matching examples, see [Path matching examples](https://docs.byteplus.com/en/docs/apig/Creating_a_route?lang=en#tWzDOik1).<br><br>   * **Exact match**: The request is forwarded only if the request path is the same as the configured path.<br><br>   * **Regex Match**: The request is forwarded only if the request path matches the configured regular expression.<br><br>   * **Prefix**: The request is forwarded if the request path starts with the configured path.<br><br><br>> **tip**<br><br><br>> Priority order of path matching: exact matching \> prefix matching \> regular expression matching.<br><br><br><br>* **Request header**: Allows access only to requests that contain the specified header. You can add multiple request headers.<br><br>   * **Header key**: Supports English letters, numbers, hyphen (`-`), and underscore (`_`).<br><br>   * **Match type**: Specifies the matching method of the Header. **Exact match**, **Regex Match**, and **Prefix** are supported.<br><br>   * **Header value**: Validates the ASCII code range.<br><br>* **Request QueryString**: Only requests that include the specified parameter are allowed access. You can add multiple request parameters.<br><br>* **Priority**: Specifies the priority of the route matching rule. The value is an integer. Valid values: 0 to 100. The smaller the number, the higher the priority. A more exact matching rule has a higher priority.<br><br>   For example, `path:/abc`, `header:version=v1` has a higher priority than `path:/abc`, regardless of the creation time. |

   * **Mock configurations**

      After a request matches the Mock routing rules, the gateway directly returns the pre\-configured status code and response content.

      > **tip**

      > In the current usage scenario, requests are not forwarded to the backend Upstream. Ensure that the matching rules and the response configuration meet your expectations.

      |Parameter |Description |
      |---|---|
      |Response status code |Configure the response status code. The value ranges from 100 to 599. |
      |Response body |Configure the response body. Do not enter sensitive content such as keys, tokens, or personal sensitive information. The input is a string, for example,` Success` or `{"code":0,"message":"success"}`  |

   * **Advanced** ** settings**

      For advanced settings of routing policies, see [Routing policies](https://docs.byteplus.com/en/docs/apig/Routing_policy).

5. Click **Confirm** to complete the route creation.

## Path matching examples

Path matching examples are as follows.

|<br>Matching method<br> |<br>Request path<br> |<br>Configured path<br> |||
|---|---|---|---|---|
|||<br>/apig/test.jpg<br> |/apig |/apig[^\s]\* |
|<br>Exact matching<br> |<br>/apig/test.jpg<br> |<br>√<br> |\- |\- |
|<br>Regular expression matching<br> ||<br>√<br> |\- |√ |
|<br>Prefix match<br> ||<br>√<br> |√ |\- |

## Validate results

### Validation example

After creating the Mock route, access the service domain name and route path from a terminal to verify whether API Gateway returns the pre\-configured status code and response body. In this example, the response status code of the Mock route is set to `200`, and the response body is set to `Success`.

1. Execute the following command. Replace <service domain name\> with the actual domain name of the target service.

   ```Bash
   curl -i https://<service domain name>
   ```

2. The expected response is as follows. The actual response protocol and response headers may vary depending on the access environment. Refer to the actual displayed response status code and response body.

   ```Bash
   HTTP/1.1 200 OK
   content-length: 7
   content-type: text/plain
   date: Thu, 08 Oct 2026 07:01:55 GMT
   server: istio-envoy
   
   Success
   ```

### View settings

You can view the basic information, matching rules, and Mock configuration of a route.

1. Select the target instance from the ** Instance management** drop\-down list, and then click **Route list**.

2. In the route list, you can search for the target route and view basic information.

   * From the **Instance ** and **Service** dropdown menus, select filter items to filter routes based on the selected items.

   * The route list displays the basic information of each route, such as the name/ID, status, priority, usage scenarios, domain name, and route path.

   > **tip**

   > A logical **AND** relationship applies to multiple filter conditions. This indicates that only routes meeting all specified conditions are displayed.

3. Click the name of the target route to go to the route overview page. You can view the basic information, matching rules, Mock configuration, and other details of a route.
