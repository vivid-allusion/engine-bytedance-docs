---
title: "APP/Agent accessing AI models through AI-Gateway"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-APP_Agent_accessing_AI_models_through_AI-Gateway"
---

Developers can flexibly call AI models from the frontend or backend using the AI models Access capability (AI\-Gateway) provided by AIDAP. This topic compiles sample code for three core Access scenarios, covering mainstream JavaScript and Python SDKs.

<span id="2a3jNfoy"></span>
## Scenario 1: Access from frontend using access_token based on Supabase Auth

Suitable for pure frontend applications or Agents, the frontend code can use the access_token issued by Volc Supabase Auth for logged\-in users to directly Access AI models through the browser.


1. ### Call text model via OpenAI JavaScript SDK <span id="qujhSmLq"></span>


```JavaScript
import { createClient } from '@supabase/supabase-js'
import OpenAI from 'openai';

const supabaseUrl = 'https://br-xxx.supabase.aidap.cn-beijing.volces.com'; // BytePlus Supabase Address
const supabaseAnonKey = 'your-supabase-anon-key'; // BytePlus Supabase anon_key

// Construct Supabase client
const supabase = createClient(
  supabaseUrl,
  supabaseAnonKey
)

// Access AI models through BytePlus Supabase AI-Gateway
async function chatWithAI() {
  // Obtain the Suapbase session of the logged-in app user
  const { data: { session } } = await supabase.auth.getSession();

  // Construct OpenAI Client
  const openai = new OpenAI({
    baseURL: supabaseUrl + "/v1", // baseURL constructed based on BytePlus Supabase Address
    apiKey: session.access_token, // Use the access_token issued by BytePlus Supabase Auth as apiKey
    dangerouslyAllowBrowser: true
  });
  
  // Converse with any model through OpenAI Client
  const stream = await openai.chat.completions.create({
    model: 'bytedance/doubao-seed-2.0-pro', // Specify models supported by BytePlus Supabase
    messages: [{ role: 'user', content: '你好' }],
    stream: true,
  });
  
  for await (const chunk of stream) {
     const content = chunk.choices[0]?.delta?.content || "";
     process.stdout.write(content);
  }
}

chatWithAI();

// Continue using Other Supabase BaaS functions
async function getTodos() {
    const { data, error } = await supabase
        .from('todos')
        .select('*');
    if (error) console.error(error);
    else console.log('Todos:', data);
}

getTodos();
```



2. ### Call text model via Vercel JavaScript SDK <span id="7iowujTh"></span>


```JavaScript
import { createClient } from '@supabase/supabase-js'
import { createOpenAICompatible, generateText } from "ai";

const supabaseUrl = 'https://br-xxx.supabase.aidap.cn-beijing.volces.com'; // BytePlus Supabase Address
const supabaseAnonKey = 'your-supabase-anon-key'; // BytePlus Supabase anon_key

// Construct Supabase client
const supabase = createClient(
  supabaseUrl,
  supabaseAnonKey
)

// Access AI models through BytePlus Supabase AI-Gateway
async function chatWithAI() {
  // Get suapbase session of logged-in APP user
  const { data: { session } } = await supabase.auth.getSession();
  
  // Construct Vercel AI Client
  const gateway = createOpenAICompatible({
    baseURL: supabaseUrl + "/v1", // baseURL constructed based on BytePlus Supabase Address
    apiKey: session.access_token, // Use access_token issued by BytePlus Supabase Auth as apiKey
    name: "supabase-ai-gateway", // Any name
  });
  
  // Use Vercel AI Client to converse with any model
  const result = streamText({
    model: gateway('bytedance/doubao-seed-2.0-pro'), // Specify models supported by BytePlus Supabase
    prompt: '你好',
  });

  // Stream output
  for await (const chunk of result.textStream) {
    process.stdout.write(chunk);
  }
}

chatWithAI();

// Continue using Other Supabase BaaS functions
async function getTodos() {
    const { data, error } = await supabase
        .from('todos')
        .select('*');
    if (error) console.error(error);
    else console.log('Todos:', data);
}

getTodos();
```



3. ### Call image model via Ark Python SDK <span id="TdgozmxA"></span>


```Python
import os

from arkruntime import Ark
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = Ark(
        base_url=supabase_url + "/v1",
        api_key=session.access_token,
    )

    response = client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        watermark=False,
        response_format="url",
        output_format="png",
    )
    print("response:", response)

generate_image()
```



4. ### Call image model via OpenAI Python SDK <span id="pWdjYSzY"></span>


```Python
import os

from openai import OpenAI
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = OpenAI(
        base_url=supabase_url + "/v1",
        api_key=session.access_token,
    )

    response = client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        response_format="url",
        extra_body={
            "watermark": False,
            "output_format": "png",
        },
    )
    print("response:", response)

generate_image()
```



5. ### Call image model via Vercel Python SDK <span id="cIjcrdha"></span>


```Python
import asyncio
import os

import ai
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

async def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    provider = ai.get_provider(
        "openai",
        base_url=supabase_url + "/v1",
        api_key=session.access_token,
    )

    response = await provider.sdk_client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        response_format="url",
        extra_body={
            "watermark": False,
            "output_format": "png",
        },
    )
    print("response:", response)

asyncio.run(generate_image())
```



6. ### Call video model via Ark Python SDK <span id="Q2hXk3KJ"></span>


```Python
import os
import time

from arkruntime import Ark
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_video() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = Ark(
        base_url=supabase_url + "/api/v3",
        api_key=session.access_token,
    )

    response = client.content_generation.tasks.create(
        model="bytedance/doubao-seedance-2.0-fast",
        content=[
            {
                "type": "text",
                "text": (
                    "一段 5 秒的产品展示视频：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
                    "镜头缓慢推进，写实摄影风格，高质量细节"
                ),
            }
        ],
        duration=5,
        ratio="16:9",
        resolution="720p",
        watermark=False,
    )

    task = client.content_generation.tasks.get(response.id)
    while str(getattr(task.status, "value", task.status)) not in {
        "succeeded",
        "failed",
        "cancelled",
    }:
        time.sleep(10)
        task = client.content_generation.tasks.get(response.id)

    print("response:", task)

generate_video()
```


<span id="yWrWgpRN"></span>
## Scenario 2: Access from frontend using JWT based on third\-party Auth

Refer to [Configuring third-party login](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_third-party_login), you can configure trusted third\-party Auth systems or [Customize JWKS](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_third-party_login?lang=en#twbH5srd). Your frontend code can use the JWT token issued by the trusted third\-party system for users to Access AI models through BytePlus Supabase AI\-Gateway from the browser.


1. ### Call text model via OpenAI JavaScript SDK <span id="Huri2vn7"></span>


```JavaScript
import { createClient } from '@supabase/supabase-js'
import OpenAI from 'openai';

const supabaseUrl = 'https://br-xxx.supabase.aidap.cn-beijing.volces.com'; // BytePlus Supabase Address
const supabaseAnonKey = 'your-supabase-anon-key'; // BytePlus Supabase anon_key

// Construct Supabase client
const supabase = createClient(
  supabaseUrl,
  supabaseAnonKey
)

// Access AI models through BytePlus Supabase AI-Gateway
async function chatWithAI() {
  // Obtain the Suapbase session of the logged-in app user
  const { data: { session } } = await supabase.auth.getSession();

  // Construct OpenAI Client
  const openai = new OpenAI({
    baseURL: supabaseUrl + "/v1",        // Construct baseURL based on BytePlus Supabase address
    apiKey: getUserThirdPartyJwtToken(), // Obtain JWT token issued by trusted third-party system
    dangerouslyAllowBrowser: true
  });
  
  // Use OpenAI Client to interact with any model
  const stream = await openai.chat.completions.create({
    model: 'bytedance/doubao-seed-2.0-pro', // Specify models supported by BytePlus Supabase
    messages: [{ role: 'user', content: '你好' }],
    stream: true,
  });
  
  for await (const chunk of stream) {
     const content = chunk.choices[0]?.delta?.content || "";
     process.stdout.write(content);
  }
}

chatWithAI();

// Continue using Other Supabase BaaS functions
async function getTodos() {
    const { data, error } = await supabase
        .from('todos')
        .select('*');
    if (error) console.error(error);
    else console.log('Todos:', data);
}

getTodos();
```



2. ### Call text model via Vercel JavaScript SDK <span id="YFPElPqz"></span>


```JavaScript
import { createClient } from '@supabase/supabase-js'
import { createOpenAICompatible, generateText } from "ai";

const supabaseUrl = 'https://br-xxx.supabase.aidap.cn-beijing.volces.com'; // BytePlus Supabase address
const supabaseAnonKey = 'your-supabase-anon-key'; // BytePlus Supabase anon_key

// Construct Supabase client
const supabase = createClient(
  supabaseUrl,
  supabaseAnonKey
)

// Access AI models through BytePlus Supabase AI-Gateway
async function chatWithAI() {
  // Obtain the Suapbase session of the logged-in APP user
  const { data: { session } } = await supabase.auth.getSession();
  
  // Construct Vercel AI Client
  const gateway = createOpenAICompatible({
    baseURL: supabaseUrl + "/v1",        // Construct baseURL based on BytePlus Supabase address
    apiKey: getUserThirdPartyJwtToken(), // Obtain JWT token issued by trusted third-party system
    name: "supabase-ai-gateway",         // Any name
  });
  
  // Use Vercel AI Client to converse with any model
  const result = streamText({
    model: gateway('bytedance/doubao-seed-2.0-pro'), // Specify models supported by BytePlus Supabase
    prompt: '你好',
  });

  // Stream output
  for await (const chunk of result.textStream) {
    process.stdout.write(chunk);
  }
}

chatWithAI();

// Continue using Other Supabase BaaS functions
async function getTodos() {
    const { data, error } = await supabase
        .from('todos')
        .select('*');
    if (error) console.error(error);
    else console.log('Todos:', data);
}

getTodos();
```



3. ### Call image model via Ark Python SDK <span id="NnOWQ4HE"></span>


```Python
import os

from arkruntime import Ark
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = Ark(
        base_url=supabase_url + "/v1",
        api_key=getUserThirdPartyJwtToken(),
    )

    response = client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        watermark=False,
        response_format="url",
        output_format="png",
    )
    print("response:", response)

generate_image()
```



4. ### Call image model via OpenAI Python SDK <span id="X86Zb2zu"></span>


```Python
import os

from openai import OpenAI
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = OpenAI(
        base_url=supabase_url + "/v1",
        api_key=getUserThirdPartyJwtToken(),
    )

    response = client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        response_format="url",
        extra_body={
            "watermark": False,
            "output_format": "png",
        },
    )
    print("response:", response)

generate_image()
```



5. ### Call image model via Vercel Python SDK <span id="BeeLxdjt"></span>


```Python
import asyncio
import os

import ai
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

async def generate_image() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    provider = ai.get_provider(
        "openai",
        base_url=supabase_url + "/v1",
        api_key=getUserThirdPartyJwtToken(),
    )

    response = await provider.sdk_client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        response_format="url",
        extra_body={
            "watermark": False,
            "output_format": "png",
        },
    )
    print("response:", response)

asyncio.run(generate_image())
```



6. ### Call video model via Ark Python SDK <span id="gIlaPOlG"></span>


```Python
import os
import time

from arkruntime import Ark
from supabase import create_client

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_anon_key = os.environ.get("SUPABASE_ANON_KEY")

// Construct Supabase client;
supabase = create_client(supabase_url, supabase_anon_key)

def generate_video() -> None:
    // Obtain the Suapbase session of the logged-in app user;
    session = supabase.auth.get_session()
    client = Ark(
        base_url=supabase_url + "/api/v3",
        api_key=getUserThirdPartyJwtToken(),
    )

    response = client.content_generation.tasks.create(
        model="bytedance/doubao-seedance-2.0-fast",
        content=[
            {
                "type": "text",
                "text": (
                    "一段 5 秒的产品展示视频：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
                    "镜头缓慢推进，写实摄影风格，高质量细节"
                ),
            }
        ],
        duration=5,
        ratio="16:9",
        resolution="720p",
        watermark=False,
    )

    task = client.content_generation.tasks.get(response.id)
    while str(getattr(task.status, "value", task.status)) not in {
        "succeeded",
        "failed",
        "cancelled",
    }:
        time.sleep(10)
        task = client.content_generation.tasks.get(response.id)

    print("response:", task)

generate_video()
```


<span id="vZCMsCfh"></span>
## Scenario three: Access from backend based on service_role_key

Your backend code can use the service_role_key of BytePlus Supabase to Access AI models through Supabase AI\-Gateway from the backend.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Keep your service_role_key secure and never expose it in frontend code to prevent unauthorized access.</div>



1. ### Call text model via OpenAI Python SDK <span id="okf72sVW"></span>


```Python
import os
from openai import OpenAI

supabase_url = 'https://br-xxx.supabase.aidap.cn-beijing.volces.com'  # BytePlus Supabase address
supabase_service_role_key = os.environ.get('SERVICE_ROLE_KEY')  # BytePlus Supabase service_role_key

# Construct OpenAI client
openai_client = OpenAI(
    base_url=supabase_url+"/v1",       # Construct baseURL based on BytePlus Supabase address
    api_key=supabase_service_role_key  # Use the access_token issued by BytePlus Supabase Auth as the apiKey
)

# Chat with any model through OpenAI client
response = openai_client.chat.completions.create(
    model="bytedance/doubao-seed-2.0-pro",  # Specify models supported by BytePlus Supabase
    messages=[
        {
            "role": "user", 
            "content": "你好，请简单介绍一下自己"
        }
    ]
)

# Print AI models Access response
print("response：", response.choices[0].message.content)
```



2. ### Call text model via Vercel Python SDK <span id="VH0VkSj3"></span>


```Python
import asyncio 
from vercel_ai import generate_text, stream_text 
from vercel_ai.providers import openai_compatible

supabase_url = 'https://br-xxx.supabase.aidap.cn-beijing.volces.com'  # BytePlus Supabase address
supabase_service_role_key = os.environ.get('SERVICE_ROLE_KEY')  # BytePlus Supabase service_role_key

# Construct Vercel AI Client
gateway = openai_compatible({
    "baseURL": supabase_url+"/v1",       # Construct baseURL based on BytePlus Supabase address
    "apiKey": supabase_service_role_key, # Use the access_token issued by BytePlus Supabase Auth as apiKey
})

async def chart_with_ai():
    # Converse with any model through Vercel AI Client
    stream = stream_text(
        model=gateway("bytedance/doubao-seed-2.0-pro"), # Specifying BytePlus Supabase supported models
        prompt="写一个Python异步爬虫示例",
    )

    print("流式输出: ")
    async for chunk in stream.text_stream:
        print(chunk, end="")
```



3. ### Call image model via Ark Python SDK <span id="AjerJGdu"></span>


```Python
import os

from arkruntime import Ark

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_service_role_key = os.environ.get("SERVICE_ROLE_KEY")

def generate_image() -> None:
    client = Ark(
        base_url=supabase_url + "/v1",
        api_key=supabase_service_role_key,
    )

    response = client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        watermark=False,
        response_format="url",
        output_format="png",
    )
    print("response:", response)

generate_image()
```



4. ### Call image model via OpenAI Python SDK <span id="LgXePNu2"></span>


```Python
import os

from openai import OpenAI

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_service_role_key = os.environ.get("SERVICE_ROLE_KEY")

def generate_image() -> None:
    client = OpenAI(
        base_url=supabase_url + "/v1",
        api_key=supabase_service_role_key,
    )

    response = client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        response_format="url",
        extra_body={
            "watermark": False,
            "output_format": "png",
        },
    )
    print("response:", response)

generate_image()
```



5. ### Call image model via Vercel Python SDK <span id="sygc2e8T"></span>


```Python
import asyncio
import os

import ai

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_service_role_key = os.environ.get("SERVICE_ROLE_KEY")

async def generate_image() -> None:
    provider = ai.get_provider(
        "openai",
        base_url=supabase_url + "/v1",
        api_key=supabase_service_role_key,
    )

    response = await provider.sdk_client.images.generate(
        model="bytedance/doubao-seedream-5.0-pro",
        prompt=(
            "一张简洁的科技产品海报：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
            "写实摄影风格，高质量细节"
        ),
        size="1024x1024",
        response_format="url",
        extra_body={
            "watermark": False,
            "output_format": "png",
        },
    )
    print("response:", response)

asyncio.run(generate_image())
```



6. ### Call video model via Ark Python SDK <span id="tVbJyYkY"></span>


```Python
import os
import time

from arkruntime import Ark

supabase_url = "https://br-xxx.supabase.aidap.cn-beijing.volces.com"
supabase_service_role_key = os.environ.get("SERVICE_ROLE_KEY")

def generate_video() -> None:
    client = Ark(
        base_url=supabase_url + "/api/v3",
        api_key=supabase_service_role_key,
    )

    response = client.content_generation.tasks.create(
        model="bytedance/doubao-seedance-2.0-fast",
        content=[
            {
                "type": "text",
                "text": (
                    "一段 5 秒的产品展示视频：银色机器人手臂在明亮工作台上绘制一朵蓝色花，"
                    "镜头缓慢推进，写实摄影风格，高质量细节"
                ),
            }
        ],
        duration=5,
        ratio="16:9",
        resolution="720p",
        watermark=False,
    )

    task = client.content_generation.tasks.get(response.id)
    while str(getattr(task.status, "value", task.status)) not in {
        "succeeded",
        "failed",
        "cancelled",
    }:
        time.sleep(10)
        task = client.content_generation.tasks.get(response.id)

    print("response:", task)

generate_video()
```
