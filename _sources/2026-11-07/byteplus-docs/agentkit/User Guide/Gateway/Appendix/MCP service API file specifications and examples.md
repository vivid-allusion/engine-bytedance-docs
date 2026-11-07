---
title: "MCP service API file specifications and examples"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/MCP_service_API_file_specifications_and_examples"
---

AgentKit allows you to quickly convert existing APIs into MCP services for direct calls by agents. This topic describes the file specifications required for converting APIs to MCP services and provides sample code.

### File specifications

API files must comply with the following specifications.

|Type |Description |
|---|---|
|Syntax |* The code must not contain any syntax errors in Swagger/OpenAPI 3.<br><br>* The code must contain Swagger/OpenAPI 3 metadata, title, and version.<br><br>* We recommend that you set an operationId for each operation. |
|Request method |* Only GET, POST, PUT, DELETE, and PATCH are supported.<br><br>* Request methods, such as CONNECT, HEAD, OPTIONS, and TRACE, will be ignored. |
|Request type |* JSON (application/json) and Form (application/x\-www\-form\-urlencoded) content types are supported.<br><br>* Content types such as application/xml, multipart/form\-data, and application/octet\-stream are not supported. |
|Request parameters |* Swagger<br><br>   * When a parameter is located in path, query, header, or formData, array\-type parameters are serialized as comma\-separated values (CSV).<br><br>   * The file data type is not supported for parameters.<br><br>* OpenAPI 3.0<br><br>   * When a parameter is located in path, query, header, or cookie, array\-type parameters are serialized as comma\-separated values (CSV). |
|Response |Only 200, 201 and default are supported for parsing, and only one of them will be parsed. If multiple status codes exist at the same time, the parsing priority follows the sequence: 200 \> 201 \> default. |

## Sample code

The following is a sample POST request in JSON format.

### Swagger

```JSON
{
  "swagger": "2.0",
  "info": {
    "title": "weather",
    "version": "1.0.0"
  },
  "paths": {
    "/weather/{city}": {
      "get": {
        "operationId": "weather",
        "summary": "Check weather status。",
        "consumes": ["application/json"],
        "parameters": [
          {
            "name": "city",
            "description": "City",
            "type": "string",
            "in": "path",
            "required": true
          },
          {
            "name": "body",
            "in": "body",
            "schema": {
              "type": "object",
              "properties": {
                "date": {
                  "description": "Date",
                  "type": "string"
                }
              }
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Weather status",
            "schema": {
              "type": "object",
              "properties": {
                "weather": {
                  "description": "Weather",
                  "type": "string"
                }
              }
            }
          }
        }
      }
    }
  }
}
```

### OpenAPI 3.0

```JSON
{
  "openapi": "3.0.1",
  "info": {
    "title": "weather",
    "version": "1.0.0"
  },
  "paths": {
    "/weather/{city}": {
      "get": {
        "operationId": "weather",
        "summary": "check the weather",
        "parameters": [
          {
            "name": "city",
            "description": "city",
            "type": "string",
            "schema": {
              "type": "string"
            },
            "in": "path",
            "required": true
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "date": {
                    "description": "Date",
                    "type": "string"
                  }
                }
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "weather",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "weather": {
                      "description": "weather",
                      "type": "string"
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```
