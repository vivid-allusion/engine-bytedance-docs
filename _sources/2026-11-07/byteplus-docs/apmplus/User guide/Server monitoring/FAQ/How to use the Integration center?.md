---
title: "How to use the Integration center?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_use_the_access_center"
---

The Integration center provides not only App Key and other integration configurations, but also detailed step‑by‑step guides and examples. This topic uses Java to show you how to quickly integrate your application via the Integration center.

<span id="ESH9iPmT"></span>
## Background

APMPlus offers the following 3 integration methods. Select an appropriate one based on your language and scenario:


* **Integrate via OpenTelemetry (recommended)** : Install the `apmplus-opentelemetry-collector` and `apmplus-server-agent` add\-ons in your VKE cluster to enable data reporting quickly. There are two OpenTelemetry reporting configurations available: auto‑injection and manual SDK instrumentation.

   * **Auto‑injection**: After add\-on installation, add an annotation to your service's workload configuration to complete the setup. For example, add the `instrumentation.apmplus.volcengine.com/inject-java: 'true'` annotation under `spec.template.metadata.annotations` in the Deployment YAML for your Java service. For more examples, see [Integrating via probe automatically](https://docs.byteplus.com/en/docs/apmplus/Java_application_integration#56f4c1a7).

   * **Manual SDK instrumentation**: After add\-on installation, use the acquired Collector endpoint address to report data. For more examples, see [Integrating via SDK manually](https://docs.byteplus.com/en/docs/apmplus/Java_application_integration#0e173ae9).

* **Integrate via Skywalking, Zipkin, or Jaeger**: Obtain the APMPlus endpoint and App Key, then report data to APMPlus through the domain name.

* **Configure data upload via local code directly**: Obtain the APMPlus endpoint and App Key, then report data to APMPlus through the domain name.


<span id="ESH9iPmT"></span>
## Prerequisites


* APMPlus has already been activated. For more details, see [Activating APMPlus](https://docs.byteplus.com/en/docs/apmplus/Activate_server-side_monitoring).

* To integrate via OpenTelemetry, ensure that the `apmplus-opentelemetry-collector` and `apmplus-server-agent` add\-ons are successfully installed in your VKE cluster. For detailed add\-on installation instructions, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


<span id="50WRqI6n"></span>
## Procedure

<span id="AfIzilXt"></span>
### Step 1: Obtain configuration information

<span id="dkX4xVHx"></span>
#### Obtain the App Key

Although the App Key does not differ by service type or data collection method, it varies across workspaces. Follow these steps to get an App Key:


1. Log in to the [Server-side Monitoring console](https://console.byteplus.com/observe/apmplus-server). 

2. Click **Click to enter service list** to go to the Service management page.

3. In the left navigation pane, select **Integration hub**, specify the workspace, and obtain the App Key from the service integration information.


<span id="GrmN1jTh"></span>
#### Obtain annotation information

To automatically inject via OpenTelemetry, add an annotation under `spec.template.metadata.annotations` in your service's YAML configuration. Different syntaxes correspond to different annotations. Common annotations are as follows:


|Syntax |Annotation |
|---|---|
|Java |instrumentation.apmplus.volcengine.com/inject\-java: 'true' |
|Python |instrumentation.apmplus.volcengine.com/inject\-python: 'true' |
|Nodejs |instrumentation.apmplus.volcengine.com/inject\-nodejs: 'true' |


Using Java auto‑injection as an example, the annotation location in YAML is shown below:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: simple-java
  labels:
    app: simple-java
spec:
  replicas: 1
  selector:
    matchLabels:
      app: simple-java
  template:
    metadata:
      labels:
        app: simple-java
      annotations:
        instrumentation.apmplus.volcengine.com/inject-java: 'true'
    spec:
      containers:
      - name: simple-java
        image: java_demo_simple
        imagePullPolicy: Always
        env:
        - name: CONTAINER_RUNTIME
          value: "k8s"
```


<span id="2knXM9Tj"></span>
#### Obtain Collector endpoint information

To integrate applications via OpenTelemetry, after successfully installing the `apmplus-opentelemetry-collector` and `apmplus-server-agent` add\-ons in your VKE cluster, the collector is automatically installed and its endpoint is exposed for data reporting.

The Collector endpoint address is the same across regions, but differs by protocol. Details are as follows:


|Protocol |Collector endpoint |
|---|---|
|HTTP |https://apmplus\-opentelemetry\-gateway\-service\-http.apmplus\-opentelemetry\-operator:4318 |
|gRPC |apmplus\-opentelemetry\-gateway\-service\-grpc.apmplus\-opentelemetry\-operator:4317 |


<span id="59K0hBuu"></span>
#### Obtain APMPlus endpoint information

If you cannot use a VKE environment and cannot install the APMPlus add\-ons, you can use the APMPlus endpoint to collect data directly via a domain name.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default"><code>{region}</code> is the region ID. Ensure it is replaced with the actual value before use. For region IDs, see <a href="https://docs.byteplus.com/en/docs/apmplus/server-launching_region">Service regions</a>.</div>


* <div data-tips="true" data-tips-type="default">When reporting data directly to APMPlus via a domain name, ensure the header includes: <code>"X-ByteAPM-AppKey": ${app_key}</code>.</div>


* For integrating via the public network, the APMPlus endpoint addresses by protocol are as follows.



|Protocol |APMPlus endpoint |
|---|---|
|HTTP |https://apmplus\-{region}.volces.com/api/otlp |
|gRPC |apmplus\-{region}.volces.com:4317 |



* For integrating via VPC, the APMPlus endpoint addresses by protocol are as follows.



|Protocol |APMPlus endpoint |
|---|---|
|HTTP |https://apmplus\-{region}.ivolces.com/api/otlp |
|gRPC |apmplus\-{region}.ivolces.com:4317 |


<span id="nnYurGbJ"></span>
### Step 2: View the integration guide


1. Go to the Integration center and select an appropriate integration method based on the development language of your service.

2. Click **Integrate** on your target method card to view its supported **monitoring systems** and **data collection methods**.

3. After choosing a data collection method, follow the steps in the integration guide to complete data reporting and application integration.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The configuration code in the integration guide may contain variables that you need to replace with actual environment values.</div>


<span id="nm0Cl7qd"></span>
## What to do next

You can integrate your application via the guide in the Integration center or by referring to the integration documentation. Integration methods vary by language. For more details, see [Integration guide](https://docs.byteplus.com/en/docs/apmplus/Integration_guide).
