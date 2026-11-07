---
title: "Data encoding method"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/data-encoding-method"
---

TLS uses the Protocol Buffer format as the standard log writing format in the log upload API (PutLogs). The Protocol Buffer format is used for structured interchange formats. Before writing logs to the server level through the API interface, the raw log data needs to be serialized into a Protocol Buffer stream in the following format.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When calling the PutLogs, the log is uploaded and written through the LogGroupList.</div>


```Plain
syntax = "proto3";
package pb;
option go_package = "./;pb";
message LogContent
{
  string Key = 1;
  string Value = 2;
}

message Log
{
  int64 Time = 1;// UNIX Time Format
  repeated LogContent Contents = 2;
}

message LogTag
{
  string Key = 1;
  string Value = 2;
}

message LogGroup
{    
  repeated Log Logs = 1;
  string Source = 2;
  repeated LogTag LogTags = 3;
  string FileName = 4;
  string ContextFlow = 5; 
}

message LogGroupList
{
  repeated LogGroup LogGroups = 1;
}
```
