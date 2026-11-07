---
title: "Integrate .NET applications with OpenTelemetry"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_NET_applications_with_OpenTelemetry"
---

.NET applications have different Methods for integration in various scenarios. This article describes the Actions for integrating .NET applications using OpenTelemetry. After integration, you can automatically collect trace information, automatically generate metric, and use features such as trace search, log search, and more.

OpenTelemetry is an observability project under CNCF, aiming to provide standardized solutions in the field of observability. It addresses the standardization of data models, collection, processing, and export of observability data, and offers services independent of third\-party vendors.

If your application has already integrated the OpenTelemetry SDK, the APMPlus server side can receive data reported by OpenTelemetry. After integrating with APMPlus, you will gain RED method generation capability, multidimensional trace search, single trace search, topology generation, and more.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To isolate production and test data, see <a href="https://docs.byteplus.com/en/docs/apmplus/Isolate_production_and_test_data">Isolate production and test data</a>.</div>


<span id="AD092Iqn"></span>
### Limits


* There are certain restrictions when converting OpenTelemetry metrics to Prometheus metrics:

   * As with [open source](https://opentelemetry.io/docs/reference/specification/compatibility/prometheus_and_openmetrics/#dropped-data-points), [ExponentialHistogram](https://opentelemetry.io/docs/reference/specification/metrics/data-model/#exponentialhistogram) is not supported.

   * Data with aggregation method set to delta is not supported. Do not modify the default aggregation configuration on the SDK side to ensure that the aggregation method on the SDK side is cumulative.

* Each workspace has its own data reporting credentials. To manage and isolate data using workspaces, ensure that the `apmplus-opentelemetry-collector` component has been upgraded to version v3.1.0 or above.


<span id="GY27ubQc"></span>
### Data reporting

<span id="ikmWhs7w"></span>
#### Method 1: Report directly to the APMPlus server side

Observability data is reported directly to the APMPlus server side, supporting data reporting via grpc, http/protobuf, and other Methods.

<span id="KAP5kf0K"></span>
#### Method 2: Otel Collector forwarding [Recommended]

APMPlusOpenTelemetryCollector is a data collector developed by APMPlus based on OpenTelemetryCollector. You can install the Opentelemetry Collector in the cluster for data forwarding. There are two installation Methods:


* Install the apmplus\-opentelemetry\-collector component via the VKE cluster component center using the one\-click installation (also known as blank screen installation). In addition, it is recommended to install the apmplus\-server\-agent component at the same time to enable metric collection at the host and process levels.

* Manually install using the script provided on the service integration page.


<span id="EShhuDsH"></span>
### Data Integration

<span id="TT9PUeE2"></span>
#### Method 1: Automatic instrumentation


   * <div data-tips="true" data-tips-type="tip">.NET SDK 6+</div>


   * <div data-tips="true" data-tips-type="tip">.NET Framework does not currently support automatic instrumentation</div>


* <div data-tips="true" data-tips-type="tip"><strong>Supported frameworks</strong></div>


   * <div data-tips="true" data-tips-type="tip">see <a href="https://opentelemetry.io/docs/instrumentation/net/automatic/instrumentations/">OpenTelemetry official documentation</a>.</div>


1. Develop web applications using ASP.NET Core.

   1. Create a demo application.


```Shell
mkdir dotnet-simple-demo
cd dotnet-simple-demo
dotnet new web
```



   2. Replace the contents of the *Properties/launchSettings.json* file with the following configuration.


```JSON
{
  "$schema": "http://json.schemastore.org/launchsettings.json",
  "profiles": {
    "http": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "applicationUrl": "http://localhost:8080",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```



   3. Build the application.


```Shell
dotnet build
```



2. Configure automatic instrumentation for the application.

   1. Unix\-shell

      1. Download and execute the OpenTelemetry .NET automatic instrumentation installation script.


```Shell
curl -L -O https://github.com/open-telemetry/opentelemetry-dotnet-instrumentation/releases/latest/download/otel-dotnet-auto-install.sh

./otel-dotnet-auto-install.sh
```



      2. Set environment variables and run the OpenTelemetry .NET automatic instrumentation script.


```Shell
export OTEL_TRACES_EXPORTER=otlp \
  OTEL_METRICS_EXPORTER=otlp \
  OTEL_LOGS_EXPORTER=otlp \
  OTEL_SERVICE_NAME=<service_name> \
  OTEL_EXPORTER_OTLP_PROTOCOL=<protocol> \
  OTEL_EXPORTER_OTLP_ENDPOINT=<apmplus_endpoint> \
  OTEL_EXPORTER_OTLP_HEADERS="x-byteapm-appkey=<app_key>"
. $HOME/.otel-dotnet-auto/instrument.sh
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><service_name\> Enter the service name, which will be displayed in the APMPlus service list.</div>


* <div data-tips="true" data-tips-type="tip"><protocol\> It is recommended to use grpc.</div>


* <div data-tips="true" data-tips-type="tip"><apmplus_endpoint\> The address varies depending on region (Shanghai, Beijing, and so on) and network type (public, private). For details, see the APMPlus service access page to obtain the specific endpoint.</div>


* <div data-tips="true" data-tips-type="tip"><app_key\> Enter the app_key provided by the service access console. The app_key for each workspace is different. For instructions on how to obtain it, see <a href="https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication">How to obtain the AppKey for application performance monitoring?</a>.</div>


* <div data-tips="true" data-tips-type="tip">For more environment variable configuration options for OpenTelemetry .NET automatic instrumentation, see <a href="https://opentelemetry.io/docs/instrumentation/net/automatic/config/">OpenTelemetry .NET automatic instrumentation environment variables</a>.</div>


   2. PowerShell

      1. Download and execute the OpenTelemetry .NET automatic instrumentation installation script.


```PowerShell
$module_url = "https://github.com/open-telemetry/opentelemetry-dotnet-instrumentation/releases/latest/download/OpenTelemetry.DotNet.Auto.psm1"
$download_path = Join-Path $env:temp "OpenTelemetry.DotNet.Auto.psm1"
Invoke-WebRequest -Uri $module_url -OutFile $download_path -UseBasicParsing

Import-Module $download_path
Install-OpenTelemetryCore
```



      2. Set environment variables and run the OpenTelemetry .NET automatic instrumentation script.


```PowerShell
$env:OTEL_TRACES_EXPORTER="otlp"
$env:OTEL_METRICS_EXPORTER="otlp"
$env:OTEL_LOGS_EXPORTER="otlp"
$env:OTEL_EXPORTER_OTLP_PROTOCOL="<protocol>"
$env:OTEL_EXPORTER_OTLP_ENDPOINT="<apmplus_endpoint>"
$env:OTEL_EXPORTER_OTLP_HEADERS="x-byteapm-appkey=<app_key>"
Register-OpenTelemetryForCurrentSession -OTelServiceName "<service_name>"
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><service_name\> Enter the service name, which will be displayed in the APMPlus service list.</div>


* <div data-tips="true" data-tips-type="tip"><protocol\> It is recommended to use grpc.</div>


* <div data-tips="true" data-tips-type="tip"><apmplus_endpoint\> The address varies depending on region (Shanghai, Beijing, and so on) and network type (public, private). For details, see the APMPlus service access page to obtain the specific endpoint.</div>


* <div data-tips="true" data-tips-type="tip"><app_key\> Enter the app_key provided by the service access console.</div>


* <div data-tips="true" data-tips-type="tip">For more environment variable configuration options for OpenTelemetry .NET automatic instrumentation, see <a href="https://opentelemetry.io/docs/instrumentation/net/automatic/config/">OpenTelemetry .NET automatic instrumentation environment variables</a>.</div>


3. Run and access the application.

   1. Run the application.


```Shell
dotnet run
```



   2. Use the following command to access the application. The generated trace will be automatically uploaded to APMPlus.


```Shell
curl localhost:8080/
```


<span id="RXa53TsG"></span>
#### Method 2: Semi\-automatic instrumentation


* <div data-tips="true" data-tips-type="tip">Supported versions:</div>


   * <div data-tips="true" data-tips-type="tip">.NET ≥ 5.0</div>


   * <div data-tips="true" data-tips-type="tip">.NET Core ≥ 2.0</div>


   * <div data-tips="true" data-tips-type="tip">.NET Framework ≥ 4.6.1</div>



OpenTelemetry supports automatic upload of trace data for dozens of .NET frameworks. For a detailed list of .NET frameworks, see [Supported Libraries](https://github.com/open-telemetry/opentelemetry-dotnet-instrumentation/blob/main/docs/config.md#traces-instrumentations).


1. Create an ASP.NET Core application (web application).


Replace <your\-project\-name\> with the actual application name.

```Shell
mkdir <your-project-name>
cd <your-project-name>
dotnet new mvc
```



2. Download the required OpenTelemetry dependencies for observing .NET applications.


```Shell
dotnet add package OpenTelemetry.Exporter.Console # 在控制台导出采集的数据
dotnet add package OpenTelemetry.Extensions.Hosting
dotnet add package OpenTelemetry.Exporter.OpenTelemetryProtocol # 以OTLP协议导出
```



3. Download the automatic instrumentation dependencies.


Download the dependencies for automatic instrumentation of the ASP.NET Core framework. When the application receives an HTTP request, a Span will be automatically generated and reported. To enable automatic instrumentation for other frameworks, see [Supported Libraries](https://github.com/open-telemetry/opentelemetry-dotnet-instrumentation/blob/main/docs/config.md#traces-instrumentations) to download the corresponding dependencies.

```Shell
dotnet add package OpenTelemetry.Instrumentation.AspNetCore
```



4. Modify the code in the <your\-project\-name\>/Program.cs file.

   1. Import the required packages at the beginning of the source file.


```C#
using System.Diagnostics;
using OpenTelemetry.Exporter;
using OpenTelemetry.Resources;
using OpenTelemetry.Trace;
```



   2. Add OpenTelemetry initialization code.

      * Report using the gRPC protocol.

      * Please replace <grpc_endpoint\> and <token\> in the following code with the access point information and Token obtained from the prerequisites.


```C#
// ...
builder.Services.AddOpenTelemetry()
    .WithTracing(tracerProviderBuilder =>
        tracerProviderBuilder
            .AddSource(DiagnosticsConfig.ActivitySource.Name)
            .SetResourceBuilder(OpenTelemetry.Resources.ResourceBuilder.CreateDefault()
                .AddAttributes(new Dictionary<string, object> {
                    {"service.name", "<service_name>"},
                    {"host.name",DiagnosticsConfig.HostName}
                }))
            .AddAspNetCoreInstrumentation()
            .AddConsoleExporter() // Export Trace data in the console (optional)
            .AddOtlpExporter(opt =>
            {
                // Report using the gRPC protocol
                opt.Endpoint = new Uri("<apmplus_endpoint>");
                opt.Headers = "x-byteapm-appkey=<app_key>";
                opt.Protocol = OtlpExportProtocol.Grpc;
            })
     );
// ...
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><service_name\> Enter the service name. It will be displayed in the service list of APMPlus.</div>


* <div data-tips="true" data-tips-type="tip"><apmplus_endpoint\> The address varies depending on the region (Shanghai, Beijing, and so on) and network type (public network, private network). For details, go to the apmplus service access page to obtain the specific endpoint.</div>


* <div data-tips="true" data-tips-type="tip"><app_key\> Enter the app_key provided by the service access console.</div>


5. Run the following command in the terminal to start the project.


```Shell
dotnet run
```


Sample response:

Obtain the URL from the response information, for example, http://localhost:5107.

```Shell
Building...
info: Microsoft.Hosting.Lifetime[14]
      Now listening on: http://localhost:5107
info: Microsoft.Hosting.Lifetime[0]
      Application started. Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
      Hosting environment: Development
info: Microsoft.Hosting.Lifetime[0]
      Content root path: /path/to/<your-project-name>
```



6. Visit http://localhost:5107 in your browser. If the following page is returned, it indicates that the data has been reported to APMPlus.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9bcbcb7fc710a0caac36b120bd88db4a.png) </span>
