---
title: "Using Edge Function"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Edge_Function"
---

This topic introduces how different roles use the Edge Function module.

<span id="AnZcJRxD"></span>
## Background

The feature modules in Supabase console provide different methods for various roles in the application development process.

**Role**

As a BaaS service, the feature modules in Supabase console serve different roles in the application development process: app developers and app users.

**Method**

The Edge Function feature in the Supabase console can be configured and used on the console and also served through two types of APIs.


* Admin API: refers to the management API configured by app developers for Supabase, requiring `SERVICE_ROLE_KEY`.

* Client API: refers to the API accessed by app users in Supabase, usually called after login.


Methods and examples of calling Admin API and Client API are as follows.


|**API type** |**User** |**Function** |**Methods and examples** |
|---|---|---|---|
|admin API (HTTP interface)<br><br> |App developer |Manage EdgeFunction<br><br> |* Create function & Update function body: refer to parameters at https://supabase.com/docs/reference/api/v1\-deploy\-a\-function<br><br><br>```Bash```<br>```curl -X POST $SUPABASE_BASE_URL/functions/v1/deploy \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \```<br>```  -H "Content-Type: application/json" ```<br>```  -d '{...}'```<br><br><br><br>* Query function list: https://supabase.com/docs/reference/api/v1\-list\-all\-functions<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The URL path must end with a slash (/) to avoid error 401.</div><br><br><br>```Bash```<br>```# querying configuration```<br>```curl -X GET $SUPABASE_BASE_URL/functions/v1/ \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \```<br>```  -H "Content-Type: application/json" ```<br> |
|Client API (Supabase Client SDK) |App users |Trigger EdgeFunction in the app<br><br> |```Bash```<br>```curl -X POST $SUPABASE_BASE_URL/functions/v1/{function_slug} \```<br>```  -H "apikey: ${ANON_KEY}" \```<br>```  -H "Authorization: Bearer ${ACCESS_TOKEN}" \```<br>```  -H "Content-Type: application/json" \```<br>```  -d '{...}'```<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><code>${ACCESS_TOKEN}</code> is automatically obtained after the app user logs in successfully.</div><br> |


<span id="9sty9YEi"></span>
## Manage Edge Function in the Supabase console

<span id="1jC9ROJb"></span>
### Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).


<span id="GaqYkrRM"></span>
### Create Edge Function


1. In the Supabase console, click **Edge Functions** on the left to enter the **Edge Functions** page.

2. On the **Edge Functions** page, click **Deploy a new function** \> **via Editor** to enter the **Create new edge function** page.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also select <strong>Deploy a new function</strong> \> <strong>via AI Assistant</strong> to create an Edge Function by interacting with the AI assistant using natural language.   </div>
   

3. On the **Create new edge function** page, select the script type as needed and complete the Edge Function in the editor, then click **Deploy** at the bottom of the page to create the Edge Function.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, Edge Functions can be created using Deno, Python 3.12, Python 3.10, and Python 3.9.   </div>
   

<span id="H3CuI3Z0"></span>
### Update Edge Function


1. In the Supabase console, click **Edge Functions** on the left to enter the **Edge Functions** page.

2. On the **Edge Functions** page, click the target Edge Function in the Edge Function list to open it in the editor.

3. In the editor, after completing the required modifications, click **Deploy updates** at the bottom of the page and click **Deploy updates** again in the pop\-up dialog to update the Edge Function.


<span id="dU2tj9D9"></span>
## Manage Edge Function via Admin API

<span id="BnoglA8Z"></span>
### Create Deno function & update Deno function body

Core parameter [Reference](https://supabase.com/docs/reference/api/v1-deploy-a-function).

```Bash
curl -X POST $SUPABASE_BASE_URL/functions/v1/deploy?slug=my_deno_func \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  --data-raw $'{
    "files": [
        {
            "name": "index.ts",
            "content": "// Deno\\n// Setup type definitions for built-in Supabase Runtime APIs\\nimport \\"jsr:@supabase/functions-js/edge-runtime.d.ts\\";\\ninterface reqPayload {\\n  name: string;\\n}\\nconsole.info(\'server started\');\\nDeno.serve(async (req: Request) => {\\n  const { name }: reqPayload = await req.json();\\n  const data = {\\n    message: `Hello ${name}\u0021`,\\n  };\\n  return new Response(\\n    JSON.stringify(data),\\n    { headers: { \'Content-Type\': \'application/json\', \'Connection\': \'keep-alive\' }}\\n  );\\n});"
        }
    ],
    "metadata": {
        "entrypoint_path": "index.ts",
        "name": "my_deno_func",
        "verify_jwt": true
    }
   }'
```


<span id="sfeXkjdM"></span>
### Create a Python function & update the Python function body:


* Core parameter [Reference](https://supabase.com/docs/reference/api/v1-deploy-a-function).

* The metadata in the body needs to explicitly specify **runtime** as one of the following enum values **:** 

   * `native-python3.9/v1`

   * `native-python3.10/v1`

   * `native-python3.12/v1`


```Bash
curl -X POST $SUPABASE_BASE_URL/functions/v1/deploy?slug=my_python_func \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  --data-raw $'{
    "files": [
        {
            "name": "app.py",
            "content": "from fastapi import FastAPI\\n\\napp = FastAPI()\\n\\n@app.post(\'/\')\\nasync def root_post_handler(payload: dict):\\n    return {\\"message\\": \\"POST request received\\", \\"payload\\": payload}"
        },
        {
            "name": "requirements.txt",
            "content": "fastapi\\nuvicorn[standard]"
        },
        {
            "name": "run.sh",
            "content": "#\u0021/bin/bash\\nset -ex\\ncd `dirname $0`\\n\\n# A special check for CLI users (run.sh should be located at the \'root\' dir)\\nif [ -d \\"output\\" ]; then\\n    cd ./output/\\nfi\\n\\n# Default values for host and port\\nHOST=\\"0.0.0.0\\"\\nPORT=${_BYTEFAAS_RUNTIME_PORT:-8000}\\nTIMEOUT=${_FAAS_FUNC_TIMEOUT}\\nexport PYTHONPATH=$PYTHONPATH:./site-packages\\n\\n# Parse arguments\\nwhile [[ $# -gt 0 ]]; do\\n    case $1 in\\n        --port)\\n            PORT=\\"$2\\"\\n            shift 2\\n            ;;\\n        --host)\\n            HOST=\\"$2\\"\\n            shift 2\\n            ;;\\n        *)\\n            shift\\n            ;;\\n    esac\\ndone\\n\\nexec python3 -m uvicorn app:app --host $HOST --port $PORT --timeout-graceful-shutdown $TIMEOUT"
        }
    ],
    "metadata": {
        "entrypoint_path": "app.py",
        "name": "my_python_func",
        "verify_jwt": true,
        "runtime": "native-python3.12/v1"
    }
  }'
```


<span id="f4H7lNVK"></span>
### Update function metadata

Parameter [Reference](https://supabase.com/docs/reference/api/v1-update-a-function).

```Bash
curl -X PATCH $SUPABASE_BASE_URL/v1/projects/default/functions/{function_slug} \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" 
  -d '{
    "projectRef": "default",
    "name": "helloedge",
    "payload": {
      "description": "hi vefaas"
    }
  }'
```


<span id="gz1GQXHJ"></span>
### Delete function


* Parameter [Reference](https://supabase.com/docs/reference/api/v1-delete-a-function).


```Bash
curl -X DELETE $SUPABASE_BASE_URL/v1/projects/default/functions/{function_slug} \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" 
```


<span id="nwpn4DOh"></span>
### Query function metadata

Parameter [Reference](https://supabase.com/docs/reference/api/v1-get-a-function).

```Bash
curl -X GET $SUPABASE_BASE_URL/v1/projects/default/functions/{function_slug} \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" 
```


<span id="NGSR3sXK"></span>
### Query function body

Parameter [Reference](https://supabase.com/docs/reference/api/v1-get-a-function-body).

```Bash
curl -X GET $SUPABASE_BASE_URL/functions/v1/{function_slug}/body \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" 
```


<span id="6re5JpTp"></span>
### Query function list

Parameter [Reference](https://supabase.com/docs/reference/api/v1-list-all-functions).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The URL path must end with a slash (/) to avoid error 401.</div>


```Bash
# querying configuration
curl -X GET $SUPABASE_BASE_URL/functions/v1/ \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" 
```


<span id="a1hDqrQs"></span>
## Sample \- call Edge Function through Supabase client SDK

```JavaScript
import { createClient } from '@supabase/supabase-js'
const supabase = createClient(
  "<SUPABASE_BASE_URL>",
  "<SUPABASE_ANON_KEY>")

// call Edge Function
async function runFunction() {
  const { data, error } = await supabase.functions.invoke('myfunction', {
    body: { 
      name: 'test', 
      age: 10
    }
  })

  if (error) {
    console.log('调用失败:', error.message)
    return
  }

  console.log('调用成功:', data)
  return data
}
```
