---
title: "AgentkitAgentServerApp"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/AgentkitAgentServerApp"
---

AgentkitAgentServerApp is an advanced application framework within the AgentKit SDK based on the Agent\-to\-Agent (A2A) protocol. It is designed for building fully\-featured agent server applications. The framework integrates the Google ADK Web Server, providing a complete set of REST API endpoints. It supports features such as session management, streaming conversations, multimodal input, and evaluation sets.

<span id="iqfHkI8y"></span>
## **Applicable scenarios**


* Agent applications that require full ADK capabilities.

* Scenarios involving inter\-agent communication.

* Production environment deployments requiring comprehensive observability and lifecycle management capabilities.

* Multimodal interaction scenarios that involve handling text, images, files, and other input types.


<span id="u8aOunc8"></span>
## **Core features**


* **Complete ADK integration:**  Provides session management, long\-term memory, artifact management, credential services, evaluation set management, and other features.

* **A2A protocol support:**  Encapsulates agents as A2A services, supporting communication between agents.

* **Built\-in telemetry:**  Automatically collects traces, performance metrics, and logs.

* **Lifecycle management:**  Automatically manages startup, operation, and shutdown processes and performs resource initialization and cleanup.


<span id="DP12UVPb"></span>
## **Architecture advantages**


* **Unified API standard:**  Complies with the Google ADK API standard.

* **Multiple call methods:**  Supports REST API and SSE streaming.

* **Comprehensive session management:**  Automatically handles session creation, updating, and deletion.

* **Production\-ready: ** Includes built\-in telemetry and error handling.

* **Cross\-platform compatibility:**  Consistent with ADK implementations in other languages.

* **Multimodal support:**  Supports text, images, files, function calls, and other input types.


<span id="CudQxLvf"></span>
## **Comparison with other application frameworks**


|**Framework** |**Usage** |**Core features** |
|---|---|---|
|AgentkitSimpleApp |Standard agent application |Simple and easy to use; features the `@app.entrypoint` decorator. |
|AgentkitMCPApp |MCP tool service |Features the `@app.tool `decorator for tool encapsulation. |
|AgentkitA2aApp |A2A communication |Features the `@app.agent_executor` decorator. |
|AgentkitAgentServerApp |Full server\-side application |Integrates the ADK Web Server and supports A2A. |


<span id="ivA70Tmy"></span>
## Quick start


1. Create and start the server.

   ```Python
   import os
   from agentkit.apps import AgentkitAgentServerApp
   from veadk import Agent
   from veadk.memory.short_term_memory import ShortTermMemory
   
   from veadk.tracing.telemetry.exporters.apmplus_exporter import APMPlusExporter
   from veadk.tracing.telemetry.opentelemetry_tracer import OpentelemetryTracer
   
   exporters = [
       APMPlusExporter( ) if os.getenv("ENABLE_APMPLUS", "").lower() == "true" else None,
   ]
   tracer = OpentelemetryTracer(
       exporters=[exporter for exporter in exporters if exporter is not None]
   )
   
   # Create an agent
   root_agent = Agent(
       name="root_agent",
       instruction="You are a helpful assistant. You can answer the user's questions.",
       tracers=[tracer]
   )
   
   # Create a short-term memory service
   short_term_memory = ShortTermMemory(backend="local")
   
   # Create the application
   agent_server_app = AgentkitAgentServerApp(
       agent=root_agent,
       short_term_memory=short_term_memory,
   )
   
   # Start the server
   if __name__ == "__main__":
       agent_server_app.run(host="0.0.0.0", port=8000)
   ```
   

2. Test the agent.

   1. Create a session.

      ```Bash
      curl -X POST http://localhost:8000/apps/root_agent/users/u_123/sessions/s_123 \
        -H "Content-Type: application/json" \
        -d '{}'
      ```
      

   2. Send a streaming conversation request.

      ```Bash
      curl -X POST http://localhost:8000/run_sse \
        -H "Content-Type: application/json" \
        -d '{
          "app_name": "root_agent",
          "user_id": "u_123",
          "session_id": "s_123",
          "streaming": false,
          "new_message": {
            "role": "user",
            "parts": [{"text": "Please introduce yourself."}]
          }
        }'
      ```
      

      If a response in the following format is returned, the agent is working as expected.

      ```JSON
      {
          "data": {
              "modelVersion": "doubao-seed-1-6-250615",
              "content": {
                  "parts": [
                      {
                          "text": "The user has asked me to introduce myself again. First, I need to review the previous conversation history to see how I answered before, so I can avoid repetition while maintaining consistency. My previous response mentioned that I am an AI assistant developed by the VeADK team, specializing in data science, documentation, and software development, and that I can provide problem-solving assistance, technical support, and information consultation. Now that the user is asking again, they may want to confirm this information or get a more detailed introduction. I should keep the core information unchanged, while slightly expanding on it — for example, mentioning specific things I can help with, such as data analysis, code writing, and document organization — to make the introduction more concrete. I should also maintain a friendly tone that fits the role of a helpful assistant. I need to make sure I do not add any new information that was not mentioned in the system prompt. The system prompt states that I was developed by the VeADK team and specialize in data science, documentation, and software development, so these are the key points. I can emphasize my expertise in these areas and how I help users solve problems efficiently. I should avoid complex terminology and keep the introduction concise and clear. To summarize, the response should be structured as follows: team background, areas of focus, specific assistance provided, and goal (helping users solve problems). This way, the response addresses the user's request while maintaining consistency and professionalism.",
                          "thought": true
                      },
                      {
                          "text": "I am an AI assistant developed by the VeADK team, primarily focused on providing professional support in data science, documentation, and software development. In data science, I can help with data analysis, model understanding, and visualization design. In documentation, I can help you organize logical structures, refine expressions, and tidy up technical documents or reports. In software development, I offer code interpretation, basic feature implementation suggestions, and development workflow consultation. My goal is to help you efficiently address various needs in technical scenarios through accurate information and practical solutions."
                      }
                  ],
                  "role": "model"
              },
              "partial": false,
              "finishReason": "STOP",
              "usageMetadata": {
                  "cachedContentTokenCount": 0,
                  "candidatesTokenCount": 363,
                  "promptTokenCount": 209,
                  "totalTokenCount": 572
              },
              "invocationId": "e-a78b1c29-908e-4cfd-8e0e-e4822ad0****",
              "author": "root_agent",
              "actions": {
                  "stateDelta": {},
                  "artifactDelta": {},
                  "requestedAuthConfigs": {},
                  "requestedToolConfirmations": {}
              },
              "id": "b4cef459-4ad7-42bd-aa9d-b3040391****",
              "timestamp": 1768825786.93406
          }
      }
      ```
      


<span id="o8c7OZyo"></span>
## API endpoint reference

<span id="4ZiCGXVf"></span>
### **Session management endpoints (**  **`/sessions`** **)** 

Used to create agent sessions. Two methods are supported:

<span id="HfwgKIbb"></span>
#### **Method 1: Specify a ** **`session_id`**

Create an agent session with a specified `session_id`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="0">warning</div>


<div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">Multiple sessions with the same <code>user_id</code> and <code>session_id </code>cannot be created.</div>


<div data-tips="true" data-tips-type="warning" data-wrapper-indent="0">If the session already exists, an error is returned<code>: {"detail":"Session already exists: s_123"}</code>.</div>


* **Endpoint: ** `POST /apps/{app_name}/users/{user_id}/sessions/{session_id}`

* **Sample request**:

   ```Bash
   curl -X POST http://localhost:8000/apps/root_agent/users/u_123/sessions/s_123 \
     -H "Content-Type: application/json" \
     -d '{}'
   ```
   

* **Sample response**:

   ```JSON
   {
     "id": "s_123",
     "appName": "root_agent",
     "userId": "u_123",
     "state": {},
     "events": [],
     "lastUpdateTime": 1743711430.022186
   }
   ```
   


<span id="FvEjCQRT"></span>
#### **Method 2: Automatically assign a ** **`session_id`**

The system automatically generates a unique `session_id` to create a new agent session per call. A new session instance is created for each call. Applicable to business scenarios where manual management of `session_id` is not required.


* **Endpoint: ** `POST /apps/{app_name}/users/{user_id}/sessions`

* **Sample request:** 

   ```Bash
   curl -X POST http://localhost:8000/apps/root_agent/users/u_123/sessions \
     -H "Content-Type: application/json" \
     -d '{}'
   ```
   


<span id="FDOSbkIX"></span>
### **Conversation request endpoints (**  **`/run_sse`** **)** 

Used to send conversation requests, supporting SSE streaming responses or one\-time responses. `/run_sse` is recommended.

**Endpoint: ** `POST /run_sse` (recommended, streaming) or `POST /run` (non\-streaming)

<span id="sSvn9Fi3"></span>
#### Request field descriptions


|Parameter​ |**Type** |**Required** |**Description** |
|---|---|---|---|
|`app_name` |string |Yes |The agent application name. |
|`user_id` |string |Yes |Unique user identifier. |
|`session_id` |string |No |Unique session identifier (can be omitted during session creation). |
|`new_message` |Content |Yes |User message content (supports multimodal input). For details, see the new_message structure below. |
|`streaming` |boolean |No |Whether to use streaming response. Default: `false`. |
|`state_delta` |dict |No |State update (optional). |
|`invocation_id` |string |No |Call ID, used to resume long\-running functions (optional). |


**new_message structure**


|Parameter​ |Type |Required |Description |
|---|---|---|---|
|parts |list[Part] |Yes |List of message content parts. Each part can be of a different type (such as text, image, or file). For details, see the Part structure below. |
|role |string |No |The content producer, used for multi\-turn conversations. Must be `user` or `model`. If not specified, the system infers it automatically.<br><br><br>* `user`: User.<br><br>* `model`: Model. |


**Part structure**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">Only one field can be set for each element in the<code> parts</code> array. For example, <code>types.Part(text="hello")</code> and <code>types.Part(inline_data=...)</code> cannot be set at the same time.</div>


* <div data-tips="true" data-tips-type="warning">Multimodal messages are implemented by combining multiple <code>Part</code> elements.</div>




|Python code |JSON field |Type |Description |
|---|---|---|---|
|types.Part(text="...") |{"text": "..."} |String |Plain text content. |
|types.Part(inline_data=...) |{"inlineData": {...}} |Blob |Inline data (such as Base64\-encoded images and videos). |
|types.Part(file_data=...) |{"fileData": {...}} |FileData |File reference (accessed via URI). |
|types.Part(function_call=...) |{"functionCall": {...}} |FunctionCall |Function call. |
|types.Part(function_response=...) |{"functionResponse": {...}} |FunctionResponse |Function response. |
|types.Part(executable_code=...) |{"executableCode": {...}} |ExecutableCode |Executable code. |
|types.Part(code_execution_result=...) |{"codeExecutionResult": {...}} |CodeExecutionResult |Code execution result. |
|types.Part(thought=...) |{"thought": true/false} |Boolean |Indicates whether it is the model's reasoning. |
|types.Part(thought_signature=...) |{"thoughtSignature": "..."} |Bytes |Signature of the reasoning, used for subsequent requests. |
|types.Part(media_resolution=...) |{"mediaResolution": {...}} |PartMediaResolution |Resolution of input media. |
|types.Part(video_metadata=...) |{"videoMetadata": {...}} |VideoMetadata |Video metadata (used only when video data is provided). |


<span id="meCTNrbl"></span>
#### Sample requests of different message types


* **Plain text message**

   **Python example:** 

   ```Python
   from google.genai import types
   
   agent = Agent()
   runner = Runner(agent=agent)
   
   message = types.UserContent(
       parts=[
           types.Part(text="Please introduce yourself.")
       ]
   )
   
   async for event in runner.run_async(
       user_id=runner.user_id,session_id=session_id,new_message=message,
   ):
       ...
   ```
   

   **curl example:** 

   ```Bash
   curl -X POST http://localhost:8000/run_sse \
     -H "Content-Type: application/json" \
     -d '{
       "app_name": "root_agent",
       "user_id": "u_123",
       "session_id": "s_123",
       "streaming": true,
       "new_message": {
         "role": "user",
         "parts": [{"text": "Please introduce yourself."}]
       }
     }'
   ```
   

* **Multimodal message: text and Base64\-encoded image**

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This scenario requires model support for multimodal understanding.   </div>
   

   **Python example:** 

   ```Python
   from google.genai import types
   import base64
   
   # Read the image and encode it to base64
   with open("image.png", "rb") as f:
       image_data = base64.b64encode(f.read()).decode()
   
   message = types.UserContent(
       parts=[
           types.Part(text="描述一下这张图片"),
           types.Part(
               inline_data=types.Blob(
                   data=base64.b64decode(image_data),
                   mime_type="image/png"
               )
           )
       ]
   )
   ```
   

   **curl example:** 

   ```Bash
   curl -X POST http://localhost:8000/run \
     -H "Content-Type: application/json" \
     -d '{
       "app_name": "root_agent",
       "user_id": "u_123",
       "session_id": "s_123",
       "streaming": false,
       "new_message": {
         "role": "user",
         "parts": [
           {
             "text": "Describe this image."
           },
           {
             "inlineData": {
               "data": "iVBORw0KGgoAAAANSUhEUgAAAgAAIACAYAAAD0eNT6AAAACXBIWXMAAAsTAAALEwEAmpw...",
               "mimeType": "image/png"
             }
           }
         ]
       }
     }'
   ```
   

* **Multimodal message: text and image**

   **Python example:** 

   ```Python
   from google.genai import types
   
   message = types.UserContent(
       parts=[
           types.Part(text="Describe this image."),
           types.Part(
               file_data=types.FileData(
                   display_name="image1.png",
                   file_uri="file:///path/to/image.png",
                   mime_type="image/png"
               )
           )
       ]
   )
   ```
   

   **curl example:** 

   ```Bash
   curl -X POST http://localhost:8000/run \
     -H "Content-Type: application/json" \
     -d '{
       "app_name": "root_agent",
       "user_id": "u_123",
       "session_id": "s_123",
       "streaming": false,
       "new_message": {
         "role": "user",
         "parts": [
           {
             "text": "Describe this image."
           },
           {
             "fileData": {
               "displayName": "image1.png",
               "fileUri": "file:///path/to/image.png",
               "mimeType": "image/png"
             }
           }
         ]
       }
     }'
   ```
   

* **Multimodal message: function call**

   **Python example:** 

   ```Python
   from google.genai import types
   
   message = types.UserContent(
       parts=[
           types.Part(
               function_call=types.FunctionCall(
                   name="get_weather",
                   args={"city": "beijing"}
               )
           )
       ]
   )
   ```
   

   **curl example:** 

   ```Bash
   curl -X POST http://localhost:8000/run \
     -H "Content-Type: application/json" \
     -d '{
       "app_name": "root_agent",
       "user_id": "u_123",
       "session_id": "s_123",
       "streaming": false,
       "new_message": {
         "role": "user",
         "parts": [
           {
             "functionCall": {
               "name": "get_weather",
               "args": {"city": "beijing"}
             }
           }
         ]
       }
     }'
   ```
   


<span id="qHV9QWdS"></span>
#### **Response format**


* **Streaming response** (streaming: true):

   ```Python
   data: {"author": "agent", "parts": [{"text": "Sure,"}]}
   
   data: {"author": "agent", "parts": [{"text": "I'll help you"}]}
   
   data: {"author": "agent", "parts": [{"text": "describe this image"}]}
   
   data: {"author": "agent", "parts": [{"text": "..."}]}
   
   data: {"author": "agent", "parts": [{"text": "Done!"}]}
   ```
   

* **Non\-streaming response** (streaming: false):

   ```Python
   {"author": "agent", "parts": [{"text": "Sure, I will help you describe this image."}]}, # One-time response
   ```
   


<span id="nfsEGlOH"></span>
### **Compatibility endpoint (**  **`/invoke`** **)** 

A simplified conversation endpoint compatible with the AgentKit CLI call method.


* **Endpoint: ** `POST /invoke`.

* **Features**:

   * Extracts `user_id` and` session_id` from `HTTP headers`.

   * Supports `prompt` field (simplified, automatically converted to `new_message`).

   * Automatically creates a session (if it does not exist).

   * Always returns SSE streaming responses.

* **Sample request:** 

   ```Bash
   curl -X POST http://localhost:8000/invoke \
     -H "user_id: u_123" \
     -H "session_id: s_123" \
     -H "Content-Type: application/json" \
     -d '{
       "prompt": "Please introduce yourself."
     }'
   ```
   

* **Parameter descriptions:** 

   * Headers:

      * `user_id` or `x-user-id`: Unique user identifier.

      * `session_id`: Unique session identifier.

   * Body:

      * `prompt`: Text prompt (automatically converted to `new_message`).

* **Response format:** 

   ```Bash
   data: {"author": "agent", "parts": [{"text": "Hello!"}]}
   
   data: {"author": "agent", "parts": [{"text": "I am a..."}]}
   
   data: {"author": "agent", "parts": [{"text": "..."}]}
   ```
