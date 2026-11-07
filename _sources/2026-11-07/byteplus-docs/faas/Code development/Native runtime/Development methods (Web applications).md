---
title: "Development methods (Web applications)"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Native_runtime_Development_methods_Web_applications"
---

For **Web applications**, your program is an HTTP Server Service running in a Native runtime. This topic introduces the standards and methods that need to be followed when locally developing this HTTP Server.

<span id="service-specifications"></span>
## Service Specifications

When developing the HTTP Server locally, you need to follow the specifications below:


* **The service itself must be stateless**

   If a state is needed, it can be stored remotely in redis or mysql, and the Service startup does not depend on local memory cache or data persistence on disk.

* **Startup command**

   The service needs to provide a startup command (configured during the [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications) in the console later).

   * For simple startup commands, configure directly in the console.

   * If the startup process is complex, support providing a startup script in the project and specify this startup script when configuring the Startup command in the console.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The startup script must have corresponding executable permissions, otherwise, releasing the service will result in a <strong>permission denied</strong> error. You can refer to the following command to add execution permissions to the script for all user groups in a Linux system.   </div>
   

   ```shell
   # Note that this command is executed locally
   # Assume the startup script is run.sh
   chmod a+x run.sh
   ```
   

* **Listening port**

   A service needs to listen to a port.

   * Ensure that the port listened to by the service code matches the port configured in the console (configure the listening port when you [Create Web Applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications) later); otherwise, it will cause the function to fail to start on release and the following error will occur.

   ```shell
   function_start_timeout
   
   function process start timeout: function start timed out (120s) with command `./main --port 3000`, function may not listen on address *:8000, logs: current working directory: /opt/bytefaas Server listen on address: :3000. Please check your log(runtime_log)/code and then retry, or contact oncall
   ```
   

   * In the service, you can obtain the specified listening port through the environment variable `_FAAS_RUNTIME_PORT`.

* **Background processes are not recommended**

   It is not recommended for services to start background processes or threads (that is, when the request has returned a response, there is no need to execute asynchronous tasks in the background). The Function Service dynamically scales the backend instances based on the request volume, so the survivability of background processes and threads cannot be guaranteed.


<span id="http-server-code-example"></span>
## HTTP Server code example

In the Native runtime, the function service forwards the request Method, Path, Body, Query, and Headers to your HTTP Server. You can directly use the request headers (Headers) and request body (Body) to write the business logic of the function.

For example, in the Golang language, a complete HTTP Server code example is as follows:

```go
package main

import (
        "flag"
        "fmt"
        "log"
        "net/http"
        "os"
        "os/signal"
        "syscall"
)

func hello(w http.ResponseWriter, r *http.Request) {
        w.WriteHeader(http.StatusOK)
        w.Write([]byte("Hello World from VeFaaS"))
}

func main() {
        // Obtain the listening port from command line arguments or environment variables
        var port string
        flag.StringVar(&port, "port", "", "http server listen port")
        flag.Parse()

        if port == "" {
                port = os.Getenv("_FAAS_RUNTIME_PORT")
        }

        // Configure the request handler for HTTP Server
        http.HandleFunc("/v1/hello", hello)

        addr := fmt.Sprintf("0.0.0.0:%s", port)
        srv := http.Server{Addr: addr}

        // Start HTTP Server
        go func() {
                log.Printf("Start HTTP Server at: %s", addr)
                if err := srv.ListenAndServe(); err != nil {
                        log.Println("ListenAndServe: ", err)
                }
        }()

        // Listen to SIGINT, SIGTERM signals
        quit := make(chan os.Signal, 1)
        signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)
        <-quit

        // Gracefully shut down after receiving a signal
        log.Println("Shutting down server...")
        // Performing your graceful shutdown logic
        log.Println("Doing your graceful shutdown logic")
        if err := srv.Shutdown(nil); err != nil {
                log.Fatal("Server shutdown error: ", err)
        }

        log.Println("Server gracefully stopped")
}
```


<span id="service-listening-port-and-start-commands"></span>
### Service listening port and start commands

You can pass the listening port through a command line parameter or obtain the configured listening port (default is 8000) through the environment variable `_FAAS_RUNTIME_PORT`. The following code shows the logic to obtain the port number from command parameters and environment variables.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The listening port of the Service must match the listening port configured in the console.</div>


```go
var port string
flag.StringVar(&port, "port", "", "http server listen port")
flag.Parse()

if port == "" {
        port = os.Getenv("_FAAS_RUNTIME_PORT")
}
```


After obtaining the listening port number port, you need to ensure that the started HTTP Server is listening to `0.0.0.0:port`; otherwise, the Deployment will fail. The following code demonstrates the logic to concatenate the Service listening address and start the HTTP Server.

```go
// Concatenate address 0.0.0.0:port
addr := fmt.Sprintf("0.0.0.0:%s", port)
srv := http.Server{Addr: addr}

// Start HTTP Server
go func() {
        log.Printf("Start HTTP Server at: %s", addr)
        if err := srv.ListenAndServe(); err != nil {
                log.Println("ListenAndServe: ", err)
        }
}()
```


<span id="request-handling"></span>
### Request handling

For the HTTP Server in the Native runtime, since you have already implemented an HTTP Server, you can customize your request handlers within the logic of your HTTP Server. The following code demonstrates a simple request handling interface.

```go
func hello(w http.ResponseWriter, r *http.Request) {        w.WriteHeader(http.StatusOK)        w.Write([]byte("Hello World from VeFaaS"))}
```


The following code shows the routing for request handling.

```go
// Configure the request handling handler for the HTTP Server
http.HandleFunc("/v1/hello", hello)
```


<span id="server-graceful-shutdown"></span>
### Server graceful shutdown

When the function instance exits, the graceful shutdown of the Function Service sends a SIGINT signal to your HTTP Server. Capture this signal and execute custom graceful shutdown logic.

The following code demonstrates the process from signal capture to HTTP Server shutdown.

```go
// listening to SIGINT, SIGTERM signals
quit := make(chan os.Signal, 1)
signal.Notify(quit, syscall.SIGINT, syscall.SIGTERM)
<-quit

// Shutting down gracefully after receiving the signal
log.Println("Shutting down server...")
// Execute your graceful shutdown logic
log.Println("Doing your graceful shutdown logic")
if err := srv.Shutdown(nil); err != nil {
        log.Fatal("Server shutdown error: ", err)
}

log.Println("Server gracefully stopped")
```


<span id="configure-start-command"></span>
### Configure start command

After completing the code development and compilation, you need to [Creating Web applications](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications) in the console, configuring the start command and listening port. The diagram assumes that the service binary name is `http-server`, and the listening port is `3000`.

<span id="use-environment-variables"></span>
## Use environment variables

You can configure the environment variables required for the function runtime in the console, and read the corresponding environment variables in the code for the function processing logic. For the configured environment variables, FaaS will inject them into the container where the function runs, and the program can read them through the built\-in library of the language. For example: if the key of the environment variable in your function configuration is `envKey`, the code to read this environment variable in the running environment is as follows.

```go
import "os"
envValue := os.Getenv("envKey")
```
