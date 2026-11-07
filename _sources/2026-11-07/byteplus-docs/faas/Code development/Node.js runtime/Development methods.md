---
title: "Development methods"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Node_js_runtime_Development_methods"
---

For Node.js functions, veFaaS starts the function service process with the entry function handler defined in the `index.js` file you provide, handling request events. Example code as follows:

```javascript
// vefaas-nodejs14-default
exports.handler = async function handler (event, context) {
  return {
    statusCode: 200,
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify({ 'vefaas-nodejs14-default': 'hello world'}),
  };
};
```


If the function has some global initialization logic, such as establishing a connection with a database or initializing downstream clients, it is recommended to add an initializer function on top of the handler function for instance initialization. Example code as follows:

```javascript
// vefaas-nodejs14-default
exports.handler = async function handler (event, context) {
  return {
    statusCode: 200,
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify({ 'vefaas-nodejs14-default': 'hello world'}),
  };
};

// vefaas will try to do initializer when start up the instance, to avoid cold start from user perspective.
// initializer will only be executed for one time when there is no exception.
// otherwise initializer will be executed again before every invoke, till successfully inited.
exports.initializer = async function (context) {
  console.log('initializer begin');
  // replace the following line, with the real init logic
  await new Promise(resolve => setTimeout(resolve,3 * 1000));
  console.log('initializer end');
};
```


<span id="entry-function-handler"></span>
## Entry function handler

The handler is the entry point for the function request processing logic. The handler contains your core business logic to handle event requests and ultimately returns an optional value. The signature of the handler function is as follows.

```javascript
exports.handler = async function handler (event, context) {
  return {
    statusCode: 200,
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify({ 'vefaas-nodejs14-default': 'hello world'}),
  };
};
```


When FaaS triggers your handler function, the Node.js runtime passes `event` parameter and `context` parameter to your handler function.

<span id="event-parameter"></span>
### Event parameter

The event parameter is used to pass trigger event data to your handler function. The type of the event parameter is `Object`.

The specific content of the event parameter varies according to the type of the trigger event.

<span id="context-parameter"></span>
### Context parameter

The context parameter is used to pass runtime information to your handler function. The context parameter includes the following fields.

```json
{
  "requestId": "888590af-cb2e-4ad4-86b3-2b03d4a7****",Request ID
}
```


**Parameter description**


|**Parameter** |**Description** |
|---|---|
|requestId |The system\-generated request uuid, please obtain it from the context passed in the handler function. |


<span id="return-value"></span>
### Return value

The return value of the handler function is of `Object` type, and only the three key\-value pairs: `statusCode`, `headers`, and `body` will ultimately be returned to the requestor.

If you choose not to return any value, FaaS will by default return a 200 interface status code.

Example code for the return value of the function handler is as follows.

```javascript
{"statusCode": 200,  # Return code, the same meaning as HTTP status code. Default value is 200."headers": {         # Optional, headers returned by the HTTP trigger.    "Content-Type": "application/json"  },  "body": JSON.stringify({"message": "hello world" # Optional value, body returned by the http trigger  })}
```


**Parameter description**


|**Parameter** |**Required** |**explain** |
|---|---|---|
|statusCode |Optional |The interface return code has the same semantics as the common HTTP status code.<br><br>If no parameter value is provided, the default return code is 200. |
|headers |Optional |Return header. Includes the following sub\-parameters: Content\-Type: message body type, it is recommended to use the default value application/json. |
|body |Optional |Return message body. Includes the following sub\-parameters: message: returned message content. |


<span id="initializer-function"></span>
### Initializer function

The initializer is the entry point for the function's initialization logic. Instance\-level global initialization within a single function is recommended to be done using the initializer function. Currently, the initializer function signature supported by FaaS is as follows, and users can indicate initialization failure by returning an error.

```javascript
exports.initializer = async function (context) {
  console.log('initializer begin');
  // replace the following line, with the real init logic
  await new Promise(resolve => setTimeout(resolve,3 * 1000));
  console.log('initializer end');
};
```


<span id="using-environment-variables"></span>
## Using environment variables

You can configure the environment variables required for function runtime through the console and read the corresponding environment variables in your code for function processing logic. FaaS will inject the configured environment variables into the container where the function runs, and the program can obtain them through `process.env`.

For example: If the key\-value pair of the environment variable you configured is `HELLO: FAAS`, the code to read this environment variable in the running environment is as follows:

```javascript
console.log(process.env.HELLO); // Output: FAAS
```
