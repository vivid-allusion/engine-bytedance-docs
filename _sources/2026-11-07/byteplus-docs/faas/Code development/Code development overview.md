---
title: "Code development overview"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Code_development_overview"
---

The Function Service offers two deployment options: code deployment and container image deployment, refer to [Native Runtime](https://docs.byteplus.com/en/docs/faas/Native_runtime) for using container image. This topic introduces the basic concepts related to code writing using the code deployment method.

<span id="handler-function"></span>
## handler function

The handler is the entry point for the function request handling logic. When your function receives a call request, the Function Service starts from the handler function, starts the Function Service process, and processes the request event. The handler function generally contains event and context parameters.


* event parameter: The trigger passes the basic information of the triggering event to your handler function through the event parameter.

* context parameter: Used to pass runtime information to your handler function.


<span id="initializer-function"></span>
## initializer function

The initializer is the entry point for the function's initialization logic. If an initializer function is set, the Function Service will first call the initializer to complete the initialization of the function, and then call the handler to process the request. Instance\-level global initialization within a single function is recommended to be done using the initializer function.


* **Operating principle**

   If you pass a non\-null initializer function, the Function Service will manage the initialization process of the function. After the function's server\-side process starts (known through the Liveness probe), the Function Service will issue control signals and call the initializer to execute the function's initialization logic, ensuring successful function initialization. You can indicate initialization failure by returning an error (or experiencing a panic during the initialization process). If the function initialization fails, the result will return initializer failure, and the request will not be executed.

* **Advantages**

   * Decouples function initialization and function service startup

      If the initializer fails, it won’t cause the function's process to repeatedly restart. However, if initialization in the main function or init function is unsuccessful, it could cause your function service to fail to start normally, resulting in frequent pull\-ups of the function or deployment failures.

   * Smooth scale\-out

      In the context of scale\-out, the data traffic scheduling logic of the Function Service will try to inject new traffic into the current Instance only after the initializer of the function has been successfully executed, to ensure the smoothness of the scale\-out as much as possible.
