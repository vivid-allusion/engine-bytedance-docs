---
title: "MCP service"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/MCP_Service"
---

MCP (Model Context Protocol) is an open\-source protocol designed to standardize how applications provide context to large language models (LLMs), enabling models to flexibly and securely connect to various data sources and tools. This article describes how to create an MCP service in API Gateway.

<span id="qOMtbrTU"></span>
## Background information

The MCP protocol is used to simplify interactions between large language models (LLMs) and external tools, APIs, and services. By standardizing interfaces, LLMs can call external APIs, run scripts, access databases, and more, expanding their capability boundaries. The transmission layer of MCP supports multiple protocols, ensuring efficient and secure data transmission. Typical application scenarios include intelligent assistants and agents, enterprise\-level knowledge management, developer tools and IDE integration, multimodal data integration, and many others. In addition, MCP also provides interactive debugging tools to help developers efficiently test and debug related servers and clients.

Meanwhile, there are currently a large number of traditional HTTP applications within enterprises. Although MCP provides the corresponding SDK, adapter development is still required. Converting these applications into an MCP server can rapidly enhance the interaction capabilities between AI agents and applications. To address the above issues, API Gateway provides the MCP Service feature, which offers seamless migration capability from RESTful API to MCP protocol, enabling rapid conversion of existing HTTP applications to MCP Server.

<span id="qOMtbrTU"></span>
## Prerequisites


* Created API Gateway instance. For details, see [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* (Optional) Created service and bound custom domain name. For details, see [Create Service](https://docs.byteplus.com/en/docs/apig/Creating_a_service), [Bind custom domain name](https://docs.byteplus.com/en/docs/apig/Adding_domain_name).

* (Optional) Created consumer and generated credential for authentication and authorization. For details, see [Create consumer](https://docs.byteplus.com/en/docs/apig/Creating_a_consumer), [Generate credential](https://docs.byteplus.com/en/docs/apig/Generating_credentials).

* (Optional) When the backend service is VKE, you need to add the cluster to be connected as an Upstream Source. For specific operations, see [Import container cluster](https://docs.byteplus.com/en/docs/apig/Import_container_cluster).


<span id="VMc9Zlo7"></span>
## Usage limits

When converting HTTP to MCP, only access to the gateway via the Streamable HTTP protocol is supported.

<span id="VMc9Zlo7"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. In the left navigation bar, select **MCP Service**, and click Create **MCP Service**.

   * **Basic Information**

   
   |Parameter |Description |
   |---|---|
   |Instance |Select the APIG instance to which the MCP Service belongs from the drop\-down menu. |
   |Access domain name |Configure the domain name used by the MCP service, including:<br><br><br>* **Use existing**: Use the domain name of an existing service. When you select this option, you need to select an existing service from the pop\-up drop\-down menu.<br><br>* **Create domain name**: Create a new domain name. When you select this option, the system will automatically generate a new domain name. The new domain name will be named `mcp-service-xxxx`, where `xxxx` is a random string. |
   |MCP Service name |Configure the MCP Service name. The system will use this name to create the corresponding route. |
   |MCP Service type |Different types of backend service support different access methods. The following information is included:<br><br><br>* **HTTP to MCP**: If the backend service is an HTTP Server, select this option. The access message from the MCP Client will be converted to an HTTP message, and then the HTTP protocol will be used to access the HTTP Server.<br><br>* **Direct access to MCP**: If the backend service is an MCP Server, select this option. The MCP Client will directly access the backend MCP Server.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">When the access method is set to <strong>Direct access to MCP</strong>, the MCP Service will by default bind the MCP Session persistence add\-on. For details, see <a href="https://docs.byteplus.com/en/docs/apig/MCP_session_persistence">MCP Session persistence</a>.</div><br> |
   |MCP transmission type |When **MCP Service type** is set to **Direct access to MCP**, you need to configure the MCP transmission type. Currently, only **Streamable HTTP** is supported. |
   |MCP service path |Configure the access path of the MCP Service. |
   

   * **Backend configuration**

   
   |Parameter |Description |
   |---|---|
   |Backend service |Configure the backend service connected to Upstream as follows:<br><br><br>* **Select existing Upstream**: Select the cloud resources (container service, function service, cloud servers, and more) where the backend service is located, and an existing Upstream.<br><br>* **Create Upstream**: Configure the specified backend service Upstream. For configuration methods and parameter descriptions of different types of Upstream, see [Upstream Management](https://docs.byteplus.com/en/docs/apig/Upstream_Management). |
   

4. Click **Confirm**.


<span id="K39No00H"></span>
## Subsequent configuration

<span id="IJfFKSYS"></span>
### Obtain access address and examples


1. After MCP Service is created, select the target service in the service list, click the service name, and enter the service details page.

2. Select the **Basic information** tab, and in **Access information**, you can obtain the invocation domain name of the MCP Service, including **public network default domain name** and **custom domain name**.

3. Click **Actions** in the **access address** column, and view invocation details in the pop\-up page, including **invocation address** and **invocation example**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If TRAE is installed, you can click <strong>Go to TRAE CN configuration</strong> to quickly configure in the TRAE console.   </div>
   

<span id="aweTIQpy"></span>
### Enable authentication and authorization


1. After MCP Service is created, select the target service in the service list, click the service name, and enter the service details page.

2. Select the **Basic information** tab, and enable the **authentication and authorization** feature. In the pop\-up configuration page, use the Key Auth add\-on to configure API Key authentication and authorization. For more configuration details, see [API Key authentication and authorization](https://docs.byteplus.com/en/docs/apig/Creating_Key_Auth_plugin).


<span id="zMtRRXmF"></span>
### Add MCP Tools

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">MCP Tools can only be added when <strong>MCP Service type</strong> is set to <strong>HTTP to MCP</strong>.</div>


After the MCP Service is created, you can add MCP Tools based on Swagger files. To do so, follow the steps below:


1. After the MCP Service is created, select the target service in the service list, click the service name, and enter the service details page.

2. Select the MCP Tools tab and click **Upload MCP configuration**.

3. Click or drag the file to the console to upload the MCP Tools file.

4. Click **Confirm**. After the configuration is complete, you can view the details of the uploaded tools on the MCP Tools page.


<span id="IvCbO52U"></span>
## FAQ

<span id="OA4azxgS"></span>
### How to upload the correct MCP configuration file


* Usage limits

   The MCP configuration file must meet the following conditions:

   
   |Type |Description |
   |---|---|
   |Syntax |* No Swagger/OpenAPI 3 syntax error exists in the code.<br><br>* The code must include Swagger/OpenAPI 3 metadata, title, and version.<br><br>* It is recommended to set operationId for each operation. |
   |Request Method |* Only supports GET, POST, PUT, DELETE, and PATCH.<br><br>* Request methods such as CONNECT, HEAD, OPTIONS, and TRACE will be ignored. |
   |Request type |* Supports JSON (application/json) and Form (application/x\-www\-form\-urlencoded) content types.<br><br>* Does not support application/xml, multipart/form\-data, application/octet\-stream, and other content types. |
   |Request parameters |* Swagger<br><br>   * When the parameter location is path, query, header, or formData, array\-type parameters are serialized as comma\-separated values (CSV).<br><br>   * The data type of the parameter does not support file.<br><br>* OpenAPI 3.0<br><br>   * When the parameter location is path, query, header, or cookie, array\-type parameters are serialized as comma\-separated values (CSV). |
   |Response |Only 200, 201, and default are supported for parsing, and only one will be parsed. If multiple exist, the parsing order is 200 \> 201 \> default. |
   

* Sample code

   The following is a sample POST request in JSON format.

   * Swagger

   ```JSON
   {
     "swagger": "2.0",
     "info": {
       "title": "weather",
       "version": "1.0.0"
     },
     "paths": {
       "/weather/{city}": {
         "get": {
           "operationId": "weather",
           "summary": "Check weather status。",
           "consumes": ["application/json"],
           "parameters": [
             {
               "name": "city",
               "description": "City",
               "type": "string",
               "in": "path",
               "required": true
             },
             {
               "name": "body",
               "in": "body",
               "schema": {
                 "type": "object",
                 "properties": {
                   "date": {
                     "description": "Date",
                     "type": "string"
                   }
                 }
               }
             }
           ],
           "responses": {
             "200": {
               "description": "Weather status",
               "schema": {
                 "type": "object",
                 "properties": {
                   "weather": {
                     "description": "Weather",
                     "type": "string"
                   }
                 }
               }
             }
           }
         }
       }
     }
   }
   ```
   

* OpenAPI 3.0

   ```JSON
   {
     "openapi": "3.0.1",
     "info": {
       "title": "weather",
       "version": "1.0.0"
     },
     "paths": {
       "/weather/{city}": {
         "get": {
           "operationId": "weather",
           "summary": "check the weather",
           "parameters": [
             {
               "name": "city",
               "description": "city",
               "type": "string",
               "schema": {
                 "type": "string"
               },
               "in": "path",
               "required": true
             }
           ],
           "requestBody": {
             "content": {
               "application/json": {
                 "schema": {
                   "type": "object",
                   "properties": {
                     "date": {
                       "description": "Date",
                       "type": "string"
                     }
                   }
                 }
               }
             }
           },
           "responses": {
             "200": {
               "description": "weather",
               "content": {
                 "application/json": {
                   "schema": {
                     "type": "object",
                     "properties": {
                       "weather": {
                         "description": "weather",
                         "type": "string"
                       }
                     }
                   }
                 }
               }
             }
           }
         }
       }
     }
   }
   ```
