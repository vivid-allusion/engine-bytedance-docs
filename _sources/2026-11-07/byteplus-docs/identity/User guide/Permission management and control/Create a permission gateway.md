---
title: "Create a permission gateway"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Create_a_permission_gateway"
---

The permission gateway is built on the API Gateway (APIG) and provides a non\-intrusive, end\-to\-end permission management solution. It is specifically designed to address the challenges of permission verification in the `User -> Agent -> Tool` invocation chain, enabling unified and fine\-grained permission control without requiring any changes to your business code.

This guide will walk you through the entire process, from creating a permission gateway service and configuring routing rules to final release, helping you quickly integrate automated and highly secure permission protection for your services.

<span id="69ff031f"></span>
## Core values


* **Non\-intrusive integration**: All requests flowing to your backend services are automatically intercepted by the gateway and subjected to permission verification, with no need to modify your business code or integrate an SDK.

* **Multi\-identity collaborative verification**: The system can simultaneously identify and verify user identities and agent identities in the invocation chain, associate them with the target resource permissions, and achieve end\-to\-end security.

* **Centralized policy management**: By associating with a predefined **permission space**, you can use unified Cedar policies to define access rules for all routes and resources, enabling precise control over "who can do what through whom."


<span id="34b20657"></span>
## How it works


1. **Traffic interception**: You will receive a dedicated **interception domain**. All requests directed to your backend services enter the permission gateway through this domain name.

2. **Policy association**: Each gateway service is bound to a **permission space**, which contains predefined Cedar permission policies.

3. **Automatic verification**: When a request reaches the gateway, the system automatically parses the user identity, agent identity, and requested resource information, and matches them against the policies in the permission space.

4. **Intelligent allow/deny**: If the match is successful and the policy permits, the request is forwarded to your backend service; otherwise, the request is directly denied. The entire process is completely transparent to your business application.


<span id="88a5a33e"></span>
## Prerequisites

You have activated the Intelligent Identity and Permissions Management Platform service and completed authorization. For more information, see [Enable Agent Identity and complete authorization](https://docs.byteplus.com/docs/identity/89601).

<span id="c9d082fe"></span>
## Step 1: Create a permissions gateway service

First, you need to create a permissions gateway service, which will act as a security proxy for your backend service.


1. Log in to the BytePlus Agent Identity Console.

2. In the left navigation bar, select **Permissions Management** \> **Permissions Gateway**.

3. In the upper right corner of the page, click **Create Service**.

4. In the **Create Service** form, configure the following information:

   * **Service name**: Specify a unique name for your service, such as `trip-agent-gateway`.

   * **Backend service type**:

      * **Custom**: If your backend service is any HTTP/HTTPS service, select this option and fill in the **backend service domain name**, port, and timeout.

      * **VikingDB**: If your backend is a built\-in BytePlus service, you can select it directly from the dropdown list.

   * **Associated permissions space**: Select an existing **permissions space**. All requests passing through this gateway will be validated using the policies within that space. You can also click **Create Permissions Space** to quickly create one.

   * **Description/Project/Tag**: Enter optional information to facilitate classification and management.

4. Click **Confirm** to save. At this point, the service status is **Unpublished**.


<span id="56bdde4f"></span>
## Step 2: Configure routing rules

Routing rules define which API requests need to be intercepted and validated by the permissions gateway. You can create routes using either automatic parsing or manual configuration.


1. In the permissions gateway list, click the target service name to go to its details page.

2. On the details page, click **Create a Route**.

3. Configure the route information.

   The system provides two configuration methods: **Automatic Parsing** and **Manual Configuration**.

   
   <Tabs>
   <Tab zoneid="cOTIs4Roow" title="Automatic parsing">
   <TabTitle>Automatic parsing</TabTitle>
   
   By uploading API documentation, the system can automatically generate routing rules for you, greatly improving configuration efficiency.
   
   
   1. In the configuration method, select **automatic parsing**.
   
   2. Select your **document type**, such as OpenAPI/Swagger or natural language descriptions (Markdown/Word/TXT).
   
   3. **Upload file**: Click to upload your API documentation.
   
      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/653c5e082cd547208018feaf49c86519) </span>
   
   
   After the file is uploaded and parsed successfully, the route list will be automatically populated with all API endpoints identified from the documentation.
   
   
   </Tab>
   <Tab zoneid="Q94gHBAinw" title="Manual configuration">
   <TabTitle>Manual configuration</TabTitle>
   
   To define more complex routes or configure routes without API documentation, choose manual configuration.
   
   
   1. In the configuration method, select **manual configuration**.
   
   2. Fill in the route information:
   
      * **Route name**: Specify a unique name for this route, such as `Query Knowledge Base`.
   
      * **Request method**: Select the HTTP request method that matches this route, such as GET, POST, and so on.
   
      * **Endpoint path**: Enter the API path. Path variables are supported, such as `/api/documents/{docId}`.
   
      * **Match type**: Choose **prefix match** (such as `/api/*`) or **exact match**.
   
   3. **Configure associated resource**: This is the core of permission verification. You need to tell the gateway how to extract the resource ID for authorization from the request.
   
      * **Resource type**: Enter the type of resource, such as `knowledge_base` or `document`. This type must be consistent with the resource type defined in the Cedar policy within the permission space.
   
      * **Location**: Select which part of the request contains the resource ID, such as Header, Body, or Path.
   
      * **Field name**: Use JSONPath syntax to specify the exact location of the resource ID, such as `$.data.items[*].id`.
   
      * **Use as authorization object**: Check this option. The gateway will use the extracted resource ID to match the `resource` field in the Cedar policy.
   
   
   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/51d0ebbadfc64fbd8572c0fb4871d6d6) </span>
   
   
   4. Click **Create** to save the route. At this point, the route status is "Disabled", and the overall service status changes to **Draft**.
   
   
   </Tab>
   </Tabs>
   


<span id="e4e2e5ef"></span>
## Step 3: Publish the service

After completing all route configurations, you need to publish the service to make the permissions rules take effect.


1. In the upper right corner of the service details page, click **Publish Service**.

2. In the confirmation dialog that appears, click **Publish** again.

3. After successful publishing, the service status will change to **Running**. At this time, all requests to **interception domains** through this gateway will automatically undergo permission verification.


<span id="5f71500e"></span>
## Results and verification


* **Service list**: On the **Permission Gateway** list page, you can view key information such as the status of all services, interception domains, and associated permission spaces.

* **Service details**: You can enter the service details page at any time to view routing rules, or edit them when the service is in the **Disabled** state.

* **Activation logic**:

   * Only services that are **Running** have permission rules that actually take effect.

   * Services in **Unpublished** or **Draft** status only save the configuration and do not affect online traffic in any way.

   * To modify the routing of a running service, you must first **disable the service**, make changes, and then **publish** it again.


<span id="c49119e8"></span>
## Frequently asked questions

<span id="c2c9d472"></span>
### **Why does automatic route parsing fail?** 

Please check whether the API documentation you uploaded contains clear interface definitions. At a minimum, it must include the **request method (Method)**  and **path (Path)** . If the document format is not standard, it is recommended to switch to **manual configuration**.

<span id="f9a29f5c"></span>
### **The service has been published, but permission verification is not effective?** 


* Please focus on checking the following two points:

   * **Whether the policy exists**: In the associated **permission space**, check whether a `permit` or `forbid` policy has been written for the target resource.

   * **Whether resource mapping is correct**: In the **associated resource** configuration of the route, check whether the **resource type**, **location**, and **field name (JSONPath)**  can accurately extract the resource ID from the request.


<span id="4a3d7693"></span>
### **Unable to publish the service, with the prompt "Permission space not associated"?** 

Each permission gateway service must be associated with a permission space. Please select a previously created permission space in the service configuration. If none exists, please go to the **Permission Policy** module to create one first.
