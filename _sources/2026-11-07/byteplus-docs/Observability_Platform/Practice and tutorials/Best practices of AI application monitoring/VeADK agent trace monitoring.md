---
title: "VeADK agent trace monitoring"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/VeADK_agent_trace_monitoring"
---

Volcengine Agent Development Kit (VeADK) provides observability capabilities to record the critical paths and intermediate states of an agent during execution. It can also report trace data to Application Performance Management (APM) via an exporter, enabling developers to perform debugging, performance analysis, behavior tracing, and other related tasks. This topic describes how to monitor the trace data reported by VeADK through APM.

<span id="Bxa3AeHD"></span>
## Background

VeADK is an end\-to\-end architecture for agents that is launched by BytePlus. It provides developers with a full\-process development framework for agent build, cloud deployment, and evaluation and optimization. VeADK outperforms existing agent development frameworks with its deep integration with the BytePlus product ecosystem. It empowers developers to build enterprise\-grade AI agent applications more efficiently. For more details, refer to the [official VeADK documentation](https://volcengine.github.io/veadk-python/).

<span id="isF4D0OE"></span>
## Prerequisites


* VeADK has been installed. For detailed installation steps, refer to the [VeADK installation guide](https://volcengine.github.io/veadk-python/quickstart/).

* You have obtained the AK and SK of your BytePlus account. .


<span id="pwvRh5T3"></span>
## Procedure

<span id="ZlO3ZnLv"></span>
### Step 1: Configure environment variables

Configure your AK and SK as environment variables for your application based on your actual needs. These credentials are used to set the API Key or other authentication information for large model calls.

<span id="aiEye3KL"></span>
### Step 2: Report observability data

Build your agent by following the instructions in [Quick start guide](https://volcengine.github.io/veadk-python/quickstart/). After the agent is built, configure a cloud `exporter` to report observability data to APM. Sample code is provided below:

```Python
import json
from veadk import Agent, Runner
from veadk.memory.short_term_memory import ShortTermMemory
from veadk.tools.demo_tools import get_city_weather
from veadk.tracing.telemetry.exporters.apmplus_exporter import APMPlusExporter
from veadk.tracing.telemetry.exporters.cozeloop_exporter import CozeloopExporter
from veadk.tracing.telemetry.exporters.tls_exporter import TLSExporter
from veadk.tracing.telemetry.opentelemetry_tracer import OpentelemetryTracer

session_id = "your_session_id"

# Initialize tracing exporters
exporters = [APMPlusExporter()]
tracer = OpentelemetryTracer(exporters=exporters)

# Create agent with tool and tracer
agent = Agent(
    name="chat_robot",
    description="A robot talk with user.",
    instruction="Talk with user friendly.",
    tools=[get_city_weather],
    tracers=[tracer],
)

# Create runner and execute
runner = Runner(
    agent=agent,
    short_term_memory=ShortTermMemory(),
)
await runner.run(messages="How is the weather like in Xi'an?", session_id=session_id)

print(f"Tracing file path: {tracer._trace_file_path}")
```


<span id="Uacqp6Ig"></span>
### Step 3: Monitor agent tracing

Once VeADK reports observability data as expected, you can view the relevant tracing information for your agent in APM.


1. Log in to[ the APM console](https://console.byteplus.com/observe/apmplus-server), and select the project and region in the top navigation bar. 

2. In the left navigation bar, select **Service Monitoring \> Service List** to go to the service list page.

3. Filter the service associated with the target agent by service name, click the service name to access the service details page, and view the monitoring metrics for the agent on the **Service overview** tab. Such metrics include QPS of large model calls, number of large model calls, and token usage.

4. On the **Trace analysis** tab, click the target trace ID to go to the details page of a single trace. View the agent instrumentation data in the list view.
