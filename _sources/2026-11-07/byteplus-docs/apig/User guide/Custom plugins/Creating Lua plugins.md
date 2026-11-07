---
title: "Creating Lua plugins"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_Lua_plugins"
---

Custom Lua plugins allow you to implement custom features such as request header modification, response body processing, log output, and traffic marking. This way, you can quickly implement lightweight business extensions without compiling or uploading binary files. This topic describes how to create a Lua plugin.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>[Beta · apply for trial]</strong>: This feature is currently in Beta. To use this feature, contact your account manager.</div>


<span id="hEucc5kN"></span>
## Background

Lua is a lightweight and efficient embedded scripting language widely used for gateway proxy extension development. Based on the native Envoy mechanism, Lua plugins allow you to insert custom logic into the request and response processing chains. Lua plugins have the following features:


* Simple development: You can write scripts by referring to the Envoy Lua Filter API directly, with no SDK dependency. For details, see [Lua](https://www.envoyproxy.io/docs/envoy/v1.24.0/configuration/http/http_filters/lua_filter.html#stream-handle-api).

* Quick deployment: You can enter Lua code directly in the console, with no need for a compilation or build process.

* Hot update: Plugin configuration changes take effect immediately, with no need to restart the gateway instance.


<span id="03rDTUgB"></span>
## Usage limits


* Currently, only standard gateway instances support Lua plugins. The elastic gateway and Serverless gateway are not supported.

* Currently, Lua plugins only support route\-level configuration.

* The custom plugin capability requires the gateway to be version 4.3.7 or later.


<span id="IIiBC4p8"></span>
## Prerequisites


* A standard gateway instance has been created. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A service has been created. For details, see [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service?lang=en).

* A route has been created. For details, see [Creating routes](https://docs.byteplus.com/en/docs/apig/Creating_a_route).


<span id="tQYrWS6F"></span>
## Procedure

<span id="ghqESxnA"></span>
### Step 1: Install a custom Lua plugin


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the ** Instance management ** drop\-down list. Then, click ** Plugin Center**.

4. On the **Plugin Center ** page, select **Custom plugin \> Install custom plugin**, and configure the custom plugin parameters.

   
   |Parameter |Description |
   |---|---|
   |Plugin identifier (Key) |The identifier of the custom plugin. |
   |Plugin alias |The alias of the plugin. After configuration, the plugin is displayed with this name. |
   |Resource type |Select LUA. |
   |Lua script |Enter a Lua script in the script editor. The code must include the envoy_on_request or envoy_on_response function. |
   |Version |The version number of the plugin. The default value is 1.0.0. You can increment the version number for subsequent feature iterations. |
   |Version description |A change description of the current plugin version. |
   

5. Click **Confirm**.


<span id="KlAAlCO0"></span>
### Step 2: Create a plugin


1. On the **Custom plugin** page, click **Create plugin**.

2. On the Create plugin page, configure the following plugin parameters.

   
   |Parameter |Description |
   |---|---|
   |Effective level |The level at which the plugin takes effect. Only the route level is supported. |
   |Service |Select the service associated with the plugin from the drop\-down list. |
   |Route |Select the route associated with the plugin from the drop\-down list. |
   |Addon configuration |Configure the effective logic of the custom plugin. You can use JSON or YAML for the configuration. |
   

3. Click **Confirm**.


<span id="xj86YEuL"></span>
## Validate results

You can view plugin status and other details. Plugins are enabled by default after creation.

&nbsp;

<span id="ATGgb0In"></span>
## Lua development guide

<span id="n9l7N0lI"></span>
### Lua plugin example

<span id="0QPxTCG1"></span>
#### Script structure

Interaction between Lua plugins and Envoy is based on the following two entry functions:


* envoy_on_request(request_handle): Called on the request path to process inbound requests.

* envoy_on_response(response_handle): Called on the response path to process outbound responses.


<span id="fqnCjNPv"></span>
#### Sample code

The following is a basic sample code of a Lua plugin. It adds the size of the request body to request headers, adds the size of the response body to response headers, and removes the response header named` foo`.

```Lua
-- Called on the request path
function envoy_on_request(request_handle)
  -- Wait for the complete request body, and add the request body size to the request header
  request_handle:headers():add("request_body_size", request_handle:body():length())
end

-- Called on the response path
function envoy_on_response(response_handle)
  -- Wait for the complete response body, and add the size of the response body to the response header
  response_handle:headers():add("response_body_size", response_handle:body():length())
  -- Delete the response header named foo
  response_handle:headers():remove("foo")
end
```


<span id="TnpmzSg2"></span>
### Lua plugin configuration example

The following example uses JSON. The example configuration contains three data mapping rules. Each rule extracts data from a specified field or from a JSON path in the request body, applies Base64 decoding to the source value, and then writes the result to an HTTP request header and a specified JSON node in the request body. This enables cross\-location copying of request header and request body parameters, along with data decoding, when the gateway forwards requests.

```JSON
{
  "transformations": [
    {
      // Conversion rule 1: Extract the instance_address field, Base64-decode it, and write it to the request header x-instance-address
      "source": {
        "query": "instance_address"
      },
      "target": {
        "header": "x-instance-address"
      },
      "codec": "BASE64_DECODE"
    },
    {
      // Conversion rule 2: Extract the instance_address field, Base64-decode it, and write it to the "/a" node of the request body JSON
      "source": {
        "query": "instance_address"
      },
      "target": {
        "body_json_pointer": "/a"
      },
      "codec": "BASE64_DECODE"
    },
    {
      // Conversion rule 3: Read the value at the "/b" node of the request body JSON and copy it to the "x-b" request header without encoding or decoding
      "source": {
        "body_json_pointer": "/b"
      },
      "target": {
        "header": "x-b"
      }
    }
  ]
}
```
