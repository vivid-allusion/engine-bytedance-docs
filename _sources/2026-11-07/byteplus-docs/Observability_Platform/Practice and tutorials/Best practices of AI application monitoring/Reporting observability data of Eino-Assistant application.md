---
title: "Reporting observability data of Eino-Assistant application"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Reporting_observability_data_of_Eino-Assistant_application"
---

Application Performance Management (APM) has been adapted to multiple CloudWeGo frameworks, enabling tracing for CloudWeGo\-related services. This topic describes how to view the observability data of the Eino\-Assistant application, with its observability data reporting to APM as an example.

<span id="ZtmiYzop"></span>
## Prerequisites

For the code repository and documentation of Eino\-Assistant, refer to [github_eino_assistant](https://github.com/cloudwego/eino-examples/tree/main/quickstart/eino_assistant).

<span id="R1vk190J"></span>
## Procedure

<span id="CadkKXpT"></span>
### Step 1: Deploy Eino\-Assistant


* #### Method 1: Local deployment <span id="tGpUN2Yf"></span>

   1. In `.env`, configure the APM authentication information `APMPLUS_APP_KEY`. For information on how to obtain the AppKey, refer to [How to obtain the AppKey for APM authentication?](https://docs.byteplus.com/en/docs/apmplus/How_can_I_obtain_the_AppKey_for_server-side_Monitoring_authentication).

   2. In `.env`, configure the endpoint and API Key for the large model.

   3. Deploy Redis locally by executing the ` docker-compose up -d` command.

   4. Start the application by executing the `go run cmd/einoagent/main.go` command.

* #### Method 2: Deployment on BytePlus <span id="x69Kn06G"></span>

   1. Log in to the [ModelArk console](https://console.byteplus.com/ark) and create two models: one for Embedding and one for Chat.

   2. Log in to the [Database console](https://console.byteplus.com/db), create a Redis Cluster, and obtain the private network address.

   3. Log in to the [VKE console](https://console.byteplus.com/vke), deploy the [Dockerfile](https://github.com/cloudwego/eino-examples/blob/main/quickstart/eino_assistant/Dockerfile) application, and configure the Server\-side Monitoring endpoint, ModelArk endpoint, and Redis parameters.


&nbsp;

&nbsp;


&nbsp;

   4. In VKE, create a public Service of the LoadBalancer type and obtain its public access address.

   5. Access the Eino\-Assistant application via a browser and interact with it.


<span id="qw2UOqLX"></span>
### Step 2: View observability data in APM


* #### View metrics <span id="0pU6Bfqx"></span>

   1. Log in to the [APM console](https://console.byteplus.com/observe/apmplus-server), and select the project and region in the top navigation bar.

   2. In the left navigation bar, select **Service Monitoring \> Service List** to go to the service list page.

   3. Click the Eino\-Assistant service name to go to the service management page, where you can view the metrics of Eino\-Assistant. The metrics include large model metrics, golden signals, and runtime monitoring metrics.

      * **Large model metrics**

      * **Golden signals**

      * **Runtime monitoring metrics**

* #### View traces <span id="Ra1wGOAg"></span>

   1. Click **Trace Analysis** in the left navigation bar, search for traces related to Eino\-Assistant by service name, and view the trace list.

   2. Click the target trace ID to view the details of a single trace. Three display modes are supported: flame graph, list, and topology map.
