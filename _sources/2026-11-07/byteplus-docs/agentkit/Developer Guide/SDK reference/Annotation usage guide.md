---
title: "Annotation usage guide"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Annotation_usage_guide"
---

AgentKit SDK provides a set of concise decorators (annotations) for quickly building different types of Agent applications. This topic provides a detailed introduction to the usage and best practices for different annotations.

<span id="UtF8rvmU"></span>
## Simple Agent annotation

`AgentkitSimpleApp` is the most commonly used application framework, providing standard HTTP service endpoints.

<span id="AwD5tGlP"></span>
### @app.entrypoint

Defines the main entry point function for the agent, which handles incoming call requests from the Platform.

<span id="UP8GxCtO"></span>
#### **Function signature**

```Python
@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    pass
```


<span id="cQC7q9Oo"></span>
#### Parameter description


* **payload** (dict): The request body, which contains user input and configuration.

   * `prompt `(str): The user\-provided prompt.

   * Other custom fields.

* **headers** (dict): The request headers, which contain contextual information.

   * `user_id` (str): User ID.

   * `session_id` (str): Session ID.

   * `request_id `(str): Request ID for tracing.

   * Other custom headers.

* **Return value** (str): Response result of the agent.


<span id="nFyzIDut"></span>
#### **Complete example**

```Python
from agentkit.apps import AgentkitSimpleApp
from veadk import Agent, Runner
from veadk.tools.demo_tools import get_city_weather

app = AgentkitSimpleApp()
agent = Agent(tools=[get_city_weather])
runner = Runner(agent=agent)

@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    """Agent main entry function"""
    # 1. Extract input parameter
    prompt = payload.get("prompt", "")
    user_id = headers.get("user_id", "anonymous")
    session_id = headers.get("session_id", "default")
    
    # 2. Call agent to run
    response = await runner.run(
        messages=prompt,
        user_id=user_id,
        session_id=session_id
    )
    
    # 3. Response
    return response
```


<span id="J1sK0cdz"></span>
#### Usage notes


* **The function must be asynchronous**, defined with` async def`.

* **Fixed parameter order**: The first parameter is payload, the second is headers.

* **Return string**: The return value is automatically packaged into a JSON response.

* **Error handling**: It is recommended to handle exceptions inside the function.


<span id="UlJmRJyJ"></span>
#### **Error handling example**

```Python
import logging

logger = logging.getLogger(__name__)

@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    try:
        prompt = payload["prompt"]
        response = await runner.run(messages=prompt)
        return response
    except KeyError as e:
        logger.error(f"Missing required field: {e}")
        return f"Error: Missing required field {e}"
    except Exception as e:
        logger.error(f"Agent execution failed: {e}")
        return f"Error: {str(e)}"
```


<span id="BugAQmTr"></span>
### @app.ping

Defines a health check function used for health probes from AgentKit and Kubernetes.

<span id="OPpUC1l3"></span>
#### Function signature

```Python
@app.ping
def ping() -> str:
    pass
```


<span id="bPwrBBYn"></span>
#### Parameter description


* **No parameters**: The health check function takes no parameters.

* **Return value** (str): Health status information, typically "pong" or "ok".


<span id="MdcI5FGc"></span>
#### Basic example

```Python
@app.ping
def ping() -> str:
    """Health check"""
    return "pong!"
```


<span id="5a29BKlQ"></span>
#### Advanced example: Including dependency checks

```Python
import redis
from sqlalchemy import create_engine

# Initialize dependency
redis_client = redis.Redis(host='localhost', port=6379)
db_engine = create_engine('postgresql://...')

@app.ping
def ping() -> str:
    """Health check, including dependent service detection"""
    try:
        # Check Redis connection
        redis_client.ping()
        
        # Check database connection
        with db_engine.connect() as conn:
            conn.execute("SELECT 1")
        
        return "ok - all services healthy"
    except Exception as e:
        logger.error(f"Health check failed: {e}")
        return f"degraded - {str(e)}"
```


<span id="8m8hZRo8"></span>
#### Usage notes


* **No parameters**: The function signature must be `def ping() -> str:`.

* **Synchronous function**: Defined with `def` instead of `async def`.

* **Fast response**: It should return within 1 second to avoid timeouts.

* **Lightweight check**: Avoid performing time\-consuming operations.


<span id="4Fe9yLlp"></span>
#### Available endpoints

The health check function is automatically registered to the following endpoints:


* `GET /ping`: Basic health check.

* `GET /health`: Health status.

* `GET /readiness`: Kubernetes readiness probe.

* `GET /liveness`: Kubernetes liveness probe.


<span id="VubLzPUA"></span>
## MCP Agent annotation

`AgentkitMCPApp` is used to build MCP (Model Context Protocol) services and encapsulate functions as standard MCP tools.

<span id="g4i4lcKZ"></span>
### @app.tool

Registers a function as an MCP tool for LLMs to call.

<span id="TuVXGi2C"></span>
#### Function signature

```Python
@app.tool
def tool_name(param1: str, param2: int) -> dict:
    pass
```


<span id="kTMoCstL"></span>
#### Parameter description


* **Function parameters**: Input parameters for the tool. Type annotations are required.

* **Return value**: Execution result of the tool. The dict type is recommended.

* **Docstring**: Used as the tool description to help the LLM understand the tool's purpose.


<span id="viUKQ0AH"></span>
#### Basic example

```Python
from agentkit.apps import AgentkitMCPApp

mcp_app = AgentkitMCPApp()

@mcp_app.tool
def get_city_weather(city: str) -> dict[str, str]:
    """Obtain city weather information.
    
    Args:
        city: City name (must be in English)
        
    Returns:
        A dictionary containing weather conditions and temperature
    """
    weather_data = {
        "beijing": {"condition": "Sunny", "temperature": 25},
        "shanghai": {"condition": "Cloudy", "temperature": 22},
    }
    
    city = city.lower().strip()
    if city in weather_data:
        info = weather_data[city]
        return {"result": f"{info['condition']}, {info['temperature']}°C"}
    else:
        return {"result": f"Weather information not found for {city}"}
```


<span id="gGUM2OSm"></span>
#### Asynchronous tool example

```Python
import aiohttp

@mcp_app.tool
async def fetch_web_content(url: str) -> dict:
    """Obtain web page content.
    
    Args:
        url: Web page URL
        
    Returns:
        A dictionary containing web page content
    """
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            content = await response.text()
            return {
                "status": response.status,
                "content": content[:1000]  # Take the first 1000 characters
            }
```


<span id="NFy4HCC3"></span>
#### Usage notes


* **Type annotations required**: All parameters must have type annotations. MCP needs this information to generate the tool schema.

* **Detailed documentation string**: Serves as the tool description to help the LLM understand the tool's purpose.

* **Supports both synchronous and asynchronous**: Both `def` and `async def` are supported.

* **Returned structured data**: It is recommended to return the `dict` type for easier parsing by LLMs.

* **Error handling**: Handle exceptions inside the function to avoid tool call failure.


<span id="wCShiTNd"></span>
#### Complex parameter example

```Python
from typing import List, Optional
from pydantic import BaseModel

class SearchQuery(BaseModel):
    keywords: List[str]
    max_results: int = 10
    filters: Optional[dict] = None

@mcp_app.tool
def search_documents(query: SearchQuery) -> dict:
    """Search documents
    
    Args:
        query: Search query object, including keywords, result count, and filter conditions.
        
    Returns:
        List of search results
    """
    # Implement search logic
    results = perform_search(
        keywords=query.keywords,
        max_results=query.max_results,
        filters=query.filters
    )
    return {"results": results, "count": len(results)}
```


<span id="ngDjhr8X"></span>
### @app.agent_as_a_tool

Encapsulates the entire agent as an MCP tool to enable agent composition and collaboration.

<span id="G5ehxA6c"></span>
#### Function signature

```Python
@app.agent_as_a_tool
async def agent_tool(prompt: str) -> str:
    pass
```


<span id="QPzzvbrr"></span>
#### Usage example

```Python
from veadk import Agent, Runner
from veadk.tools.demo_tools import get_city_weather

# Create a dedicated weather agent 
weather_agent = Agent(tools=[get_city_weather])
weather_runner = Runner(agent=weather_agent)

mcp_app = AgentkitMCPApp()

@mcp_app.agent_as_a_tool
async def weather_assistant(prompt: str) -> str:
    """Weather assistant agent
    
    An agent dedicated to handling weather-related queries, which can retrieve weather information for cities worldwide.
    
    Args:
        prompt: User's weather query
        
    Returns:
        Weather query result
    """
    response = await weather_runner.run(messages=prompt)
    return response
```


<span id="7W04DYWI"></span>
#### Multi\-agent collaboration example

```Python
# Create multiple dedicated agents
weather_agent = Agent(tools=[get_city_weather])
news_agent = Agent(tools=[get_latest_news])
calendar_agent = Agent(tools=[check_schedule])

@mcp_app.agent_as_a_tool
async def weather_assistant(query: str) -> str:
    """Weather assistant"""
    return await Runner(agent=weather_agent).run(messages=query)

@mcp_app.agent_as_a_tool
async def news_assistant(query: str) -> str:
    """News assistant"""
    return await Runner(agent=news_agent).run(messages=query)

@mcp_app.agent_as_a_tool
async def calendar_assistant(query: str) -> str:
    """Schedule assistant"""
    return await Runner(agent=calendar_agent).run(messages=query)
```


<span id="sUJOFJZD"></span>
#### Usage notes


* **Agent single responsibility**: Each agent should focus on a specific domain.

* **Clear description**: Provide a clear documentation string for the agent that outlines its capability boundaries.

* **Asynchronous execution**: Typically an asynchronous function.

* **Reasonable timeout**: Set a reasonable execution timeout period.


<span id="PQ9zAKWO"></span>
## A2A Agent annotation

`AgentKitA2aApp` is used to build A2A (Agent\-to\-Agent) applications, supporting communication and collaboration between agents.

<span id="BnFFsbHy"></span>
### @app.agent_executor

Registers an Agent executor and defines the agent's execution logic.

<span id="85JUFnPY"></span>
#### Function signature

```Python
@app.agent_executor(runner=runner, **kwargs)
class MyAgentExecutor(A2aAgentExecutor):
    pass
```


<span id="4QHNZLcM"></span>
#### Parameter description


* **runner**: Agent runner instance

* **kwargs**: Other configuration parameters


<span id="taOMRTii"></span>
#### Basic example

```Python
from agentkit.apps import AgentkitA2aApp
from google.adk.a2a.executor.a2a_agent_executor import A2aAgentExecutor
from veadk import Agent, Runner
from veadk.a2a.agent_card import get_agent_card
from veadk.tools.demo_tools import get_city_weather

# Create A2A application
a2a_app = AgentkitA2aApp()

# Create agent 
agent = Agent(tools=[get_city_weather])
runner = Runner(agent=agent)

# Register executor
@a2a_app.agent_executor(runner=runner)
class WeatherAgentExecutor(A2aAgentExecutor):
    """Weather query agent executor"""
    pass

# Run application
if __name__ == "__main__":
    a2a_app.run(
        agent_card=get_agent_card(agent=agent, url="http://127.0.0.1:8000"),
        host="127.0.0.1",
        port=8000,
    )
```


<span id="cSFZYI6y"></span>
#### Custom executor example

```Python
from a2a.server.agent_execution import AgentExecutor
from a2a.server.agent_execution.context import RequestContext
from a2a.server.events.event_queue import EventQueue

@a2a_app.agent_executor(runner=runner)
class CustomAgentExecutor(AgentExecutor):
    """Custom agent executor"""
    
    async def execute(
        self,
        context: RequestContext,
        event_queue: EventQueue
    ) -> str:
        """Execute agent logic
        
        Args:
            context: Request context, including input messages and history
            event_queue: Event queue for sending intermediate results
            
        Returns:
            Agent response
        """
        # Extract input from context
        user_message = context.current_input
        
        # Send an intermediate event (optional)
        await event_queue.put({
            "type": "thinking",
            "content": "Thinking..."
        })
        
        # Execute agent 
        response = await self.runner.run(messages=user_message)
        
        return response
```


<span id="vDgBDWE2"></span>
#### Usage notes


* **Inherit from AgentExecutor**: Must inherit from `AgentExecutor` or its subclasses.

* **Provide runner**: Must provide a runner instance via parameters.

* **Implement execute method**: To customize logic, rewrite the execute method.

* **Use event_queue**: Send intermediate status via the event queue.


<span id="m9XQ1wsq"></span>
### @app.task_store

Registers a task storage for persisting the A2A task state.

<span id="MJtJRUZQ"></span>
#### Function signature

```Python
@app.task_store(**kwargs)
class MyTaskStore(TaskStore):
    pass
```


<span id="3DgoIhEJ"></span>
#### Use default storage

```Python
# If task_store is not specified, memory storage (InMemoryTaskStore) will be used
a2a_app = AgentkitA2aApp()

@a2a_app.agent_executor(runner=runner)
class MyExecutor(A2aAgentExecutor):
    pass
```


<span id="PicI51xm"></span>
#### Custom task storage example

```Python
from a2a.server.tasks.task_store import TaskStore
from a2a.types import Task
import redis

@a2a_app.task_store(redis_url="redis://localhost:6379")
class RedisTaskStore(TaskStore):
    """Redis-based task storage"""
    
    def __init__(self, redis_url: str):
        self.redis_client = redis.from_url(redis_url)
    
    async def save_task(self, task: Task) -> None:
        """Save the task"""
        task_data = task.model_dump_json()
        self.redis_client.set(f"task:{task.id}", task_data)
    
    async def get_task(self, task_id: str) -> Task | None:
        """Obtain the task"""
        task_data = self.redis_client.get(f"task:{task_id}")
        if task_data:
            return Task.model_validate_json(task_data)
        return None
    
    async def delete_task(self, task_id: str) -> None:
        """Delete the task"""
        self.redis_client.delete(f"task:{task_id}")
```


<span id="T92aaokJ"></span>
#### Usage notes


* **Optional decorator**: If not specified, memory storage is used.

* **Inherit from TaskStore**: Must inherit from `TaskStore`.

* **Implement required methods**: Implement required methods such as `save_task`, `get_task`, and `delete_task`.

* **Persistent storage**: Persistent storage (such as Redis and databases) is recommended for production environments.


<span id="0xVI6c65"></span>
## Best practice

<span id="95VFPAX5"></span>
### Error handling

All decorated functions should have proper error handling.

```Python
import logging

logger = logging.getLogger(__name__)

@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    try:
        # Business logic
        result = await process(payload)
        return result
    except ValueError as e:
        logger.warning(f"Invalid input: {e}")
        return f"Invalid input: {str(e)}"
    except Exception as e:
        logger.error(f"Unexpected error: {e}", exc_info=True)
        return "An error occurred. Please try again later."
```


<span id="uwyxzBhk"></span>
### Log record

Add appropriate logs for issue tracking.

```Python
@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    request_id = headers.get("request_id", "unknown")
    logger.info(f"[{request_id}] Processing request: {payload}")
    
    try:
        response = await runner.run(messages=payload["prompt"])
        logger.info(f"[{request_id}] Request completed successfully")
        return response
    except Exception as e:
        logger.error(f"[{request_id}] Request failed: {e}")
        raise
```


<span id="F3H0TMp0"></span>
### Type annotation

Use complete type annotations to improve code quality.

```Python
from typing import Dict, Any

@app.entrypoint
async def run(payload: Dict[str, Any], headers: Dict[str, str]) -> str:
    prompt: str = payload["prompt"]
    user_id: str = headers.get("user_id", "anonymous")
    # ...
```


<span id="rdUJCLUz"></span>
### Documentation string

Add detailed documentation strings to all functions.

```Python
@mcp_app.tool
def calculate_distance(lat1: float, lon1: float, lat2: float, lon2: float) -> dict:
    """Calculate the distance between two geographic coordinates.
    
    Calculate the great-circle distance between two points on the Earth's surface using the Haversine formula.
    
    Args:
        lat1: Start latitude (degrees)
        lon1: Start longitude (degrees)
        lat2: End latitude (degrees)
        lon2: End longitude (degrees)
        
    Returns:
        A dictionary containing distance information in kilometers
        
    Example:
        >>> calculate_distance(39.9, 116.4, 31.2, 121.5)
        {"distance_km": 1067.5}
    """
    # Implement logic
```


<span id="Y7MmN0ad"></span>
### Performance optimization

Avoid time\-consuming initialization within decorated functions.

```Python
# ❌ Bad practice
@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    agent = Agent(tools=[...])  # Created on every request
    runner = Runner(agent=agent)
    return await runner.run(messages=payload["prompt"])

# ✅ Good practice
agent = Agent(tools=[...])  # Created only once
runner = Runner(agent=agent)

@app.entrypoint
async def run(payload: dict, headers: dict) -> str:
    return await runner.run(messages=payload["prompt"])
```
