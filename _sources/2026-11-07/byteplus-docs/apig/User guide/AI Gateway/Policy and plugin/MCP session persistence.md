---
title: "MCP session persistence"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/MCP_session_persistence"
---

The MCP session persistence Plugin supportsmulti\-instance session persistence based on the MCP protocol. This article describes how to configure the MCP session persistence Plugin.

<span id="bEYOwdTS"></span>
## Background Information

When using MCP protocol version 2024\-11\-05 based on SSE in the production environment, the following issues exist:


* **Connect and bind instances**

   * SSE is a persistent HTTP connection, and the server needs to maintain the connection status in memory.

   * A connection can only be held by the instance that created it.

* **No built\-in session sharing mechanism**

   * Native SSE does not support session rebinding or distributed routing as WebSocket does.

* **Randomly forwarding requests to other instances can result in message loss, incorrect responses, or connection failures.** 

   * If subsequent client requests are routed to ServerB instead of the original ServerA, the client cannot access the SSE connection status.

   * If Instance B cannot find the Session, it will respond with an error or re\-establish a connection, resulting in status inconsistency or duplicate connections.


The MCP session persistence Plugin provides session persistence capability. When connecting to multiple MCP Server instances on the backend, it uses MCP\-Session\-Id to maintain session persistence, ensuring that MCP calls always remain on the same instance.

<span id="tL7HKfAv"></span>
## Prerequisites


* An APIG instance has been created. For details, refer to [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* APIG instances have been upgraded to version 3.2.0 or later. For details, refer to [Version Management](https://docs.byteplus.com/en/docs/apig/Version_Management).

* The service has been created. For details, refer to [Create Service](https://docs.byteplus.com/en/docs/apig/Creating_a_service#.5Yib5bu65pyN5Yqh).

* The route has been created. For details, see [Create a route](https://docs.byteplus.com/en/docs/apig/Creating_a_route).


<span id="d8JeCqiE"></span>
## Limi


* The same Plugin can only be bound once to the same resource.

* The MCP session persistence feature must be used together with the Function Service product.

* Within the same route, the LLM load\-aware routing Plugin, the LLM Session affinity routing Plugin, and the MCP session persistence Plugin are mutually exclusive and cannot be enabled at the same time.


<span id="T5rwkqdn"></span>
## Procedure


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the left navigation bar, select **Plugin management \> MCP Session Hold Plugin**, click **Create Plugin**, and configure the Plugin parameters.

   
   |**Parameter** |Description |
   |---|---|
   |Effective level |Select the effective level for the MCP session persistence Plugin; currently, only the **route level** is supported. |
   |Instance |Select the APIG instance associated with the Plugin from the dropdown menu. |
   |Service |Select the service to which the Plugin belongs from the dropdown menu. |
   |owning route |In the dropdown menu, select an Plugin, then select the route it belongs to. |
   |Notes/comments |You may choose whether to edit the notes/comments according to your business needs. For example, you can specify the purpose of the Plugin or other relevant information. This will make it easier to identify later. |
   

3. Click **OK** to complete the configuration.


<span id="S9VUrs4g"></span>
## View configuration

After completing the configuration, view the configured Plugins in the Plugin list. If the Plugin status is **Enabled**, the Plugin is effective.
