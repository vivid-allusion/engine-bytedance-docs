---
title: "Development methods"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Python_runtime_Development_methods"
---

For Python functions, FaaS starts the function service process with the handler entry function defined in the `index.py` file you provide, handling request events. Python functions support both online console editing and code package uploading. When submitting a code Zip package using a local Zip file or TOS upload methods, please confirm that the root directory of the Zip contains a Python source file named `index.py`, which includes an entry function named `handler`, to avoid execution failures due to inability to find the entry file and function.

The example of Python function code is as follows.

```Python
import json

def handler(event, context):
# Function business logic
    return {
        "statusCode": 200,
        "headers": {
            "Content-Type": "application/json"
        },
        "body": json.dumps({
            "info": "hello veFaaS!"
        })
    }
```


<span id="entry-function-handler"></span>
## Entry function handler

The handler is the entry point for the function request processing logic. The handler contains your core business logic to handle event requests and ultimately returns an optional value. The signature of the handler function is as follows.

```Python
def handler(event, context):
    # The logic of business function 
    return some_value # Optional return value
```


When FaaS triggers your handler function, the Python runtime passes `event` parameter and `context` parameter to your handler function.

<span id="the-event-parameter"></span>
### The event parameter

The event parameter is used to pass trigger event data to your handler function. The type of the event parameter is dict.

The specific content of the event parameter varies according to the type of the trigger event.

<span id="the-context-parameter"></span>
### The context parameter

The context parameter is used to pass runtime information to your handler function. The type of the context parameter is object.


* **Description field**

   The context parameter includes the following fields:

   
   |Field |Description |
   |---|---|
   |request_id |The system\-generated request uuid, please obtain it from the context passed in the handler function. |
   

* **Usage example**

   ```Python
   def handler(event, context):
   print("Request ID:", context.request_id)
   ```
   


<span id="return-value"></span>
### Return value

The function handler can return an optional return value of `dict` type. In the return value, only the key\-value pairs `statusCode`, `headers`, and `body` will ultimately be returned to the requestor.

If you choose not to return any value, FaaS will by default return a 200 interface status code.

Example code for the return value of the function handler is as follows.

```Python
{
"statusCode": 200,  # Return code, the same meaning as HTTP status code. Default value is 200.
"headers": {        # Optional, headers returned by the HTTP trigger.
    "Content-Type": "application/json"
  },
"body": json.dumps({ # Optional, body returned by the HTTP trigger,
    "message": 'hello world'
  })
}
```


**Parameter description**


|Parameter |Required |Description |
|---|---|---|
|statusCode |Optional |The interface return code has the same semantics as the common HTTP status code.<br><br>If no parameter value is provided, the default return code is 200. |
|headers |Optional |Return header. Includes the following sub\-parameters: Content\-Type: message body type, it is recommended to use the default value `application/json`. |
|body |Optional |Return message body. Includes the following sub\-parameters:<br><br>`message`: returned message content. |


<span id="using-environment-variables"></span>
## Using environment variables

For FaaS functions, you can configure the environment variables required for the function runtime in the console, and read the corresponding environment variables in the code for the function processing logic. For the configured environment variables, FaaS will inject them into the container where the function runs, and the program can read them through the built\-in library of the language.

For example: if the key of the environment variable in your function configuration is `ENV_KEY`, the code to read this environment variable in the running environment is as follows.

```Python
import os

env_value = os.environ.get('ENV_KEY')
```
