---
title: "Supabase edge function integration with RPC practice"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase_edge_function_integration_with_RPC_practice"
---

This topic explains how to connect various communication protocols with Supabase edge function to access external systems.

<span id="BP45aIiD"></span>
## Background

Within enterprise internal systems, communication between services commonly includes **Thrift RPC** and **gRPC** besides http. When internal services have been established, existing RPC services can be integrated through **Supabase edge function** to reuse capabilities, reduce duplicate development, and quickly provide a unified function entry for upper\-layer applications.

This topic covers the following two types of scenarios:


* **Accessing external services based on Thrift RPC**

* **Accessing external services based on gRPC**


Each scenario offers examples in **deno (node.js compatible runtime)**  and **python** to help you complete integration quickly.

<span id="kUPJCqKv"></span>
## Applicable scenarios

Your backend service already provides interfaces based on Thrift RPC or gRPC, and you want to unify the packaging capability through Supabase edge function to offer HTTP call entry externally.

<span id="IWDDT34D"></span>
## Prerequisites

Before you start, ensure you have completed the following preparations:


1. Already had a usable **Supabase edge function** runtime environment. For more details, refer to [Managing edge function in Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Edge_Function?lang=en#9sty9YEi).

2. Already had an available accessible RPC service.

   * The service address in the Thrift RPC example in this topic is `www.example.com:9090`.

   * The service address in the gRPC example in this topic is `www.example.com:50051`.

3. Corresponding interface definition files have been prepared.

   * Thrift RPC：`pingpong.thrift`。

   * gRPC：`pingpong.proto`。

4. Understood the call method of the target function and have access to the following environment variables:

   * `SUPABASE_BASE_URL`

   * `SERVICE_ROLE_KEY`

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more details on getting environment variables, refer to <a href="https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables">Getting variables</a>.   </div>
   

5. If using the Python solution, ensure the function runtime supports installing dependencies via `requirements.txt`.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The address, function names, and example request bodies in this topic are for demonstration purposes. When integrating officially, replace with your actual service address, function names, and business parameters.</div>


<span id="7Qjek88K"></span>
## install

This section describes the interface description files and dependency generation steps required before integration for different solutions.

<span id="FWIDGeI8"></span>
### Thrift RPC solution

<span id="ybKbjwL2"></span>
#### Prepare thrift IDL

Example `pingpong.thrift` is as follows:

```Thrift
namespace py pingpong
namespace go pingpong
namespace java com.example.pingpong.thrift

service PingPongService {
  string ping(1:string message)
}
```


<span id="CCd0BSja"></span>
#### Generate language\-related files

**Deno example:**  first generate TypeScript files based on the `pingpong.thrift` file.

```Bash
mkdir -p .generated
npx --yes @creditkarma/thrift-typescript \
  --target apache \
  --rootDir . \
  --sourceDir . \
  --outDir .generated \
  pingpong.thrift
cp .generated/com/example/pingpong/thrift/PingPongService.ts ./PingPongService.ts
cp .generated/com/example/pingpong/thrift/index.ts ./pingpong.ts
rm -rf .generated
```


**Python example:**  first generate Python files based on the `pingpong.thrift` file.

```Bash
thrift --gen py -out . pingpong.thrift
```


<span id="uOt5ZPcv"></span>
### gRPC solution

<span id="rZWK1STP"></span>
#### Prepare proto files

Example `pingpong.proto` is as follows:

```ProtoBuf
syntax = "proto3";

package pingpong;

option go_package = "github.com/example/pingpong/idl/pb;pb";
option java_multiple_files = true;
option java_package = "com.example.pingpong.proto";
option java_outer_classname = "PingPongProto";

service PingPongService {
  rpc Ping (PingRequest) returns (PongReply);
}

message PingRequest {
  string message = 1;
}

message PongReply {
  string message = 1;
}
```


<span id="SnDQ0p3b"></span>
#### Generate language\-related files

**Deno example:**  gRPC supports dynamic loading of definitions based on proto files at runtime, so generating TypeScript files in advance is unnecessary. Just place the proto files in the function directory.

**Python example:**  Python code must be generated from the proto files first.

```Bash
python3 -m grpc_tools.protoc \
  -I . \
  --python_out=. \
  --grpc_python_out=. \
  pingpong.proto
```


<span id="FZryiXY0"></span>
## Configuration item

This topic explains the directory structure and runtime dependencies to consider before deploying each solution.

**Configuration item highlights**


* Deno solutions typically use `index.ts` as the entry point.

* Python solutions typically include `app.py + run.sh + requirements.txt` as a complete runtime unit.

* All generated files, IDL files, and business code must be placed together in the edge function project directory.


<span id="8wZfRoq5"></span>
### Thrift RPC configuration item

<span id="qiGYylrE"></span>
#### Deno directory structure

```Bash
.
├── index.ts
├── PingPongService.ts
└── pingpong.ts
```


<span id="hnK9rznp"></span>
#### Python directory structure

```Bash
.
├── app.py
├── constants.py
├── PingPongService.py
├── pingpong.thrift
├── requirements.txt
├── run.sh
└── ttypes.py
```


<span id="wxCVERCw"></span>
#### Python dependency file `requirements.txt`

```Plain Text
fastapi
thrift==0.23.0
uvicorn[standard]
```


<span id="2jUxqMc3"></span>
#### Python startup script

The following `run.sh` works for both Thrift RPC python and gRPC python examples:

```Bash
#!/bin/bash
set -ex
cd `dirname $0`

if [ -d "output" ]; then
    cd ./output/
fi

HOST="0.0.0.0"
PORT=${_BYTEFAAS_RUNTIME_PORT:-8000}
TIMEOUT=${_FAAS_FUNC_TIMEOUT}
export PYTHONPATH=$PYTHONPATH:./site-packages

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


<span id="dofuEEpO"></span>
### gRPC configuration

<span id="vXljfB9E"></span>
#### Deno directory structure

```Bash
.
├── index.ts
└── pingpong.proto
```


<span id="saIfCXrZ"></span>
#### Python directory structure

```Bash
.
├── app.py
├── pingpong_pb2_grpc.py
├── pingpong_pb2.py
├── pingpong.proto
├── requirements.txt
└── run.sh
```


<span id="MFC27AjS"></span>
#### Python dependency file `requirements.txt`

```Plain Text
fastapi
grpcio==1.80.0
protobuf==6.33.6
uvicorn[standard]
```


<span id="SN9o0zLN"></span>
#### Python startup script

The following run.sh works for both Thrift RPC python and gRPC python examples:

```Bash
#!/bin/bash
set -ex
cd `dirname $0`

if [ -d "output" ]; then
    cd ./output/
fi

HOST="0.0.0.0"
PORT=${_BYTEFAAS_RUNTIME_PORT:-8000}
TIMEOUT=${_FAAS_FUNC_TIMEOUT}
export PYTHONPATH=$PYTHONPATH:./site-packages

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


<span id="DG30EgRd"></span>
## Usage

This topic provides core example code and call methods for each solution.

<span id="rUJdxJD8"></span>
### Use Thrift RPC to access external services

<span id="g70SNUHO"></span>
#### Deno example

In the Deno scenario, you need to explicitly import `thrift` via npm; implicit local references cannot be used directly.

```TypeScript
// false: invalid.
import * as thrift from "thrift";

// valid
import * as thrift from "npm:thrift@0.23.0";
```


The example `index.ts` is as follows:

```TypeScript
// Deno
// Setup type definitions for built-in Supabase Runtime APIs、
import "jsr:@supabase/functions-js/edge-runtime.d.ts";
import thrift from "npm:thrift@0.23.0"; // note, this must be an explicit npm import
import * as PingPongService from "./PingPongService.ts";

interface reqPayload {
  message: string;
}

const HOST = "www.example.com";
const PORT = 9090;

function unaryPing(message: string): Promise<string> {
  return new Promise((resolve, reject) => {
    const connection = thrift.createConnection(HOST, PORT, {
      transport: thrift.TBufferedTransport,
      protocol: thrift.TBinaryProtocol,
    });
    let settled = false;
    const fail = (error: Error) => {
      if (settled) {
        return;
      }
      settled = true;
      connection.end();
      reject(error);
    };
    const succeed = (value: string) => {
      if (settled) {
        return;
      }
      settled = true;
      connection.end();
      resolve(value);
    };

    connection.on("error", fail);
    connection.on("connect", () => {
      const client = thrift.createClient(PingPongService, connection);
      client.ping(message).then(succeed, fail);
    });
  });
}

console.info("server started");
Deno.serve(async (req: Request) => {
  const { message }: reqPayload = await req.json();
  const reply = await unaryPing(message);
  const data = {
    message: reply,
  };
  return new Response(
    JSON.stringify(data),
    { headers: { "Content-Type": "application/json", "Connection": "keep-alive" }},
  );
});
```


Call example (assuming the function name is `thrift-hello-deno`):

```Bash
curl -X POST $SUPABASE_BASE_URL/functions/v1/thrift-hello-deno \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  --data '{"message":"hello thrift"}'
```


Response example:

```Bash
{"message":"pong: hello thrift"}
```


<span id="94ybWK1M"></span>
#### Python example

The example `app.py` is as follows:

```Python
from fastapi import FastAPI
from thrift.protocol import TBinaryProtocol
from thrift.transport import TSocket, TTransport

from PingPongService import Client

app = FastAPI()

def rpc_ping(message: str) -> str:
    socket = TSocket.TSocket("www.example.com", 9090)
    transport = TTransport.TBufferedTransport(socket)
    protocol = TBinaryProtocol.TBinaryProtocol(transport)
    client = Client(protocol)
    transport.open()
    try:
        return client.ping(message)
    finally:
        transport.close()

@app.post('/')
async def root_post_handler(payload: dict):
    return {"message": rpc_ping(str(payload["message"]))}
```


Call example (assuming the function name is `thrift-hello-python`):

```Bash
curl -L -X POST $SUPABASE_BASE_URL/functions/v1/thrift-hello-python \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  --data '{"message":"hello thrift"}'
```


Response example:

```Bash
{"message":"pong: hello thrift"}
```


<span id="MEPKF6PE"></span>
### Access external services using gRPC

<span id="70ZxGM0X"></span>
#### Deno example

Example `index.ts` as follows:

```TypeScript
// Deno
// Setup type definitions for built-in Supabase Runtime APIs
import "jsr:@supabase/functions-js/edge-runtime.d.ts";
import * as grpc from "npm:@grpc/grpc-js@1.10.10";
import * as protoLoader from "npm:@grpc/proto-loader@0.7.13";
import { dirname, join } from "node:path";
import { fileURLToPath } from "node:url";

interface reqPayload {
  message: string;
}

const HOST = "www.example.com";
const PORT = 50051;
const protoPath = join(dirname(fileURLToPath(import.meta.url)), "pingpong.proto");

function unaryPing(message: string): Promise<{ message: string }> {
  const definition = protoLoader.loadSync(protoPath, {
    keepCase: true,
    longs: String,
    enums: String,
    defaults: true,
    oneofs: true,
  });
  const pkg: any = grpc.loadPackageDefinition(definition);
  const client = new pkg.pingpong.PingPongService(`${HOST}:${PORT}`, grpc.credentials.createInsecure());

  return new Promise((resolve, reject) =>
    client.Ping({ message }, (error: unknown, response: { message: string }) =>
      error ? reject(error) : resolve(response),
    )
  );
}

console.info("server started");
Deno.serve(async (req: Request) => {
  const { message }: reqPayload = await req.json();
  const reply = await unaryPing(message);
  const data = {
    message: reply.message,
  };
  return new Response(
    JSON.stringify(data),
    { headers: { "Content-Type": "application/json", "Connection": "keep-alive" }},
  );
});
```


Call example (assuming the function name is `pingpong-grpc-deno`):

```Bash
curl -X POST $SUPABASE_BASE_URL/functions/v1/pingpong-grpc-deno \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  --data '{"message":"Hello grpc"}'
```


Response example:

```Bash
{"message":"pong: Hello grpc"}
```


<span id="109icaLH"></span>
#### Python example

Example `app.py` as follows:

```Python
import grpc
from fastapi import FastAPI

import pingpong_pb2
import pingpong_pb2_grpc

app = FastAPI()


def rpc_ping(message: str) -> str:
    with grpc.insecure_channel("www.example.com:50051") as channel:
        client = pingpong_pb2_grpc.PingPongServiceStub(channel)
        reply = client.Ping(pingpong_pb2.PingRequest(message=message))
    return reply.message


@app.post('/')
async def root_post_handler(payload: dict):
    return {"message": rpc_ping(str(payload["message"]))}
```


Call example (assuming the function name is `pingpong-grpc-python`):

```Bash
curl -X POST ${SUPABASE_BASE_URL}/functions/v1/pingpong-grpc-python \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \
  -H "Content-Type: application/json" \
  --data '{"message":"Hello grpc"}'
```


response example:

```Bash
{"message":"pong: Hello grpc"}
```
