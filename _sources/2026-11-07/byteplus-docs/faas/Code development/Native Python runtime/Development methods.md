---
title: "Development methods"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_Python_runtime_Development_methods"
---

For **Web applications**, your program is a service running as an HTTP Server in the Native Python runtime. This topic introduces the standards and methods you need to follow when developing this HTTP Server.

<span id="service-standards"></span>
## Service standards

You need to follow these standards when developing an HTTP Server locally:


* **The service itself must be stateless**

   If state is needed, it can be stored in a remote redis or mysql; service start\-up does not depend on local memory cache or data on disk.

* **Startup command**

   The service needs to provide a startup command (configured later in the console when [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications)).

   * For simple startup commands, they can be configured directly on the console.

   * If the startup process is complex, it supports providing a startup script in the project, and specifying this startup script when configuring the startup command on the console.

   ```shell
   # Note that this command should be executed locally
   # Assuming the startup script is run.sh
   chmod a+x run.sh
   ```
   

* **Listening port**

   The service needs a listening port.

   * Ensure that the port your service code is listening to matches the port configured in the console (the listening port will be configured when [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications) in the console later); otherwise, it will lead to a failure in function deployment during cold start and the following error will occur.

      ```shell
      function_start_timeout
      
      function process start timeout: function start timed out (120s) with command `./main --port 3000`, function may not listen on address *:8000, logs: current working directory: /opt/bytefaas Server listen on address: :3000. Please check your log(runtime_log)/code and then retry, or contact oncall
      ```
      

   * In the service, you can obtain the specified listening port through the environment variable `_FAAS_RUNTIME_PORT.`

* **Background processes are not recommended**

   It is not recommended for services to start background processes or threads (that is, when the request has returned a response, there is no need to execute asynchronous tasks in the background). Function Services dynamically scale backend instances based on request volume, and cannot guarantee the survival of background processes and threads.


<span id="development-example"></span>
## Development example

In the Native Python runtime, the function service will forward the Request Method, Path, Body, Query, and Headers to your HTTP Server. You can directly use the request headers (Headers) and request body (Body) to write the business logic of the function.

For example, using the fastapi framework, the complete code is as follows.


* `app.py`:

   ```python
   from fastapi import FastAPI
   import time
   
   # create a FastAPI Application instance
   app = FastAPI()
   
   # Define a GET route for root path '/'
   @app.get('/')
   def index_handler():
       return 'Hello FastAPI From FaaS nativepython3 (and bye python2)!'
   
   # Define a POST route for root path '/'
   @app.post('/')
   async def root_post_handler(payload: dict):
       return {"message": "POST request received", "payload": payload}
   ```
   

* `run.sh` (Start script):

   ```bash
   #!/bin/bash
   set -ex
   cd `dirname $0`
   
   if [ -d "output" ]; then
       cd ./output/
   fi
   
   # Configure listening address and port
   HOST="0.0.0.0"
   PORT=${_FAAS_RUNTIME_PORT}
   TIMEOUT=${_FAAS_FUNC_TIMEOUT}
   
   # parameter resolution
   while [[ $# -gt 0 ]]; do
       case $1 in
           --port)
               PORT="$2"
               shift 2
               ;;
           --host)
               HOST="$2"
               shift 2
               ;;
           *)
               shift
               ;;
       esac
   done
   
   exec python3 -m uvicorn app:app --host $HOST --port $PORT --timeout-graceful-shutdown $TIMEOUT
   ```
   


<span id="service-listening-port-and-startup"></span>
### Service listening port and startup

You can pass the port through command line parameters, or obtain the configured listening port through the environment variable `_FAAS_RUNTIME_PORT` (default is 8000). The following code in the run.sh file demonstrates the logic of obtaining the listening address (HOST) and port number (PORT) from environment variables and command parameters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The port that the service listens on must match the port configured in the console.</div>


```bash
# Configure listening address and port.
# The listening address must be 0.0.0.0, otherwise it will lead to deployment failure.
HOST="0.0.0.0"
PORT=${_FAAS_RUNTIME_PORT}
TIMEOUT=${_FAAS_FUNC_TIMEOUT}

# parameter resolution
while [[ $# -gt 0 ]]; do
    case $1 in
        --port)
            PORT="$2"
            shift 2
            ;;
        --host)
            HOST="$2"
            shift 2
            ;;
        *)
            shift
            ;;
    esac
done
```


<span id="request-handling"></span>
### Request handling

For the HTTP Server of the Native Python runtime, since you have already implemented an HTTP Server, you have the ability to customize your request handler within the HTTP Server's logic. The following code shows a simple request handling interface.

```python
# Request handling
@app.get('/')
def index_handler():
    return 'Hello FastAPI From FaaS nativepython3 (and bye python2)!'
```


<span id="configuration-of-the-start-command"></span>
### Configuration of the start command

After completing code development and compilation, you need to configure the start command and listening port when [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications) in the console. In this example, the start command is `./run.sh`, and the listening port is 8000.

<span id="using-environment-variables"></span>
## Using environment variables

For Native Python functions, you can configure the environment variables required for the runtime in the console, and read the corresponding environment variables in the code for the function processing logic. For the configured environment variables, FaaS will inject them into the container where the function runs, and the program can read them through the built\-in library of the language.

For example: if the key of the environment variable in your function configuration is `envKey`, the code to read this environment variable in the running environment is as follows.

```python
import "os"
envValue = os.getenv("envKey")
```
