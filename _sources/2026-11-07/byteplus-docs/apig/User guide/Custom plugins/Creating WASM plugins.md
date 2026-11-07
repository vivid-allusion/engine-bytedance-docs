---
title: "Creating WASM plugins"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Creating_WASM_plugins"
---

Custom WASM plugins allow you to write your own gateway processing logic and apply custom rules at different levels, including instances, services, and routes, to customize traffic control. This topic describes how to create and configure WASM plugins.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>[Beta · apply for trial]</strong>: This feature is currently in Beta. To use this feature, contact your account manager.</div>


<span id="53hJ4CIy"></span>
## Background

WASM is a portable, lightweight, and fast\-loading binary executable format. It supports compiling programs written in C++, Go, Rust, and other programming languages into bytecode that can be efficiently executed in a sandbox environment. In API Gateway, WASM plugins allow you to develop custom gateway extension logic with Go, such as custom authentication, traffic control, and request rewriting. After you compile the code into a .wasm binary file and upload the file to the console, the file can be loaded and executed on the gateway data plane.

<span id="dJnbT1wx"></span>
## Usage limits


* Currently, only standard gateway instances support WASM plugins. The elastic gateway and Serverless gateway are not supported.

* Currently, WASM plugins can be written only in Go. We recommend that you use Go 1.24 or later for compilation.

* The custom plugin capability requires the gateway of version 4.3.7 or later.


<span id="9jUzF3WO"></span>
## Prerequisites


* A standard gateway instance has been created. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* A service has been created. For details, see [Creating services](https://docs.byteplus.com/en/docs/apig/Creating_a_service?lang=en).

* A route has been created. For details, see [Creating routes](https://docs.byteplus.com/en/docs/apig/Creating_a_route).

* The WASM Go SDK has been obtained, and the plugin code has been developed and compiled.


<span id="vl72tyW8"></span>
## Procedure

<span id="9dWnHfHA"></span>
### Step 1: Install a custom WASM plugin


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. Select the target region in the top navigation bar.

3. In the left navigation pane, select the target instance from the ** Instance management ** drop\-down list. Then, click ** Plugin Center**.

4. On the **Plugin Center ** page, select **Custom plugin \> Install custom plugin**, and configure the custom plugin parameters.

   
   |Parameter |Description |
   |---|---|
   |Plugin identifier (Key) |The identifier of the custom plugin. The key can contain uppercase and lowercase letters, underscores (_), hyphens (\-), and periods (.), and cannot exceed 30 characters. |
   |Plugin alias |Specify a plugin alias based on your business requirements. After configuration, the custom plugin is displayed with this name. |
   |Resource type |Select WASM. |
   |WASM file |Upload the WASM plugin configuration file. |
   |Version |The version number of the plugin. The default value is 1.0.0. You can increment the version number for subsequent feature iterations. |
   |Version description |A change description of the current plugin version. |
   

5. Click **Confirm**.


<span id="7elWlWyQ"></span>
### Step 2: Create a plugin


1. On the page for the installed custom plugin, click **Create plugin**.

2. On the Create plugin page, complete the following configuration and click **Confirm**.

   
   |Parameter |Description |
   |---|---|
   |Effective level |Select the effective level of the plugin. Service level, Instance level, and Routing level are available. |
   |Instance |Displays the name of the APIG instance associated with the plugin. |
   |Service |Select **Service level ** for "Effective level", and select the service associated with the plugin from the drop\-down list. |
   |Route |Select ** Routing level ** for Effective level, and select the route associated with the plugin from the drop\-down list. |
   |Notes |Optional. Enter a description for the plugin, such as its purpose, for easy identification later. |
   |Addon configuration |Configure the effective logic of the custom plugin. You can use JSON or YAML for the configuration. |
   


<span id="huFN8xn9"></span>
## Validate results

You can view plugin status and other details. Plugins are enabled by default after creation.

<span id="2mHhkShh"></span>
## WASM plugin configuration example

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


<span id="zelVCoId"></span>
##
