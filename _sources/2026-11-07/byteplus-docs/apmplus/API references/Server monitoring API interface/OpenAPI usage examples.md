---
title: "OpenAPI usage examples"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/OpenAPI_usage_examples"
---

This topic introduces the demo examples in various programming languages provided by APMPlus to help you quickly call the OpenAPI.

<span id="2d0b6ada"></span>
## Prerequisites

You need to use the signing method from the signature SDK. 

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The sample code is strongly dependent on the signature SDK. Authorization constructed through the signature mechanism cannot be used.</div>


<span id="520d5975"></span>
## Sample code


<Tabs>
<Tab zoneid="aP4QhexTo1" title="Go">
<TabTitle>Go</TabTitle>

```Go
package main

import (
    "bytes"
    "context"
    "fmt"
    "io"
    "net/http"
    "time"

    volc "github.com/volcengine/volc-sdk-golang/base"
)

const (
    Host        = "https://apmplus-openapi.cn-beijing.byteplusapi.com"
    ServiceName = "apmplus_openapi"
    Region      = "cn-beijing"
    AK          = "xx"
    SK          = "xx=="
)

func main() {
    // 1. Initialize method information
    var (
        action  = "GetAppAlarmRuleList" // API name
        version = "2022-10-12"          // API version
        appID   = "123456"              // Application ID
    )
    ctx := context.Background()
    // 2. Construct request body
    req := buildRequest(ctx, action, version, appID)
    // 3. Send request
    cli := &http.Client{Timeout: time.Second * 5}
    resp, err := cli.Do(req)
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()
    data, _ := io.ReadAll(resp.Body)
    fmt.Println(string(data))
}

// buildRequest
func buildRequest(ctx context.Context, action, version, appID string) *http.Request {
    payload := buildRequestJsonBody()
    body := bytes.NewBuffer([]byte(payload))

    req, _ := http.NewRequest("POST", Host, body)
    q := req.URL.Query()
    q.Add("Action", action)
    q.Add("Version", version)
    req.URL.RawQuery = q.Encode()
    req.Header.Set("x-app-ids", appID)
    req.Header.Set("content-type", "application/json")
    // Sign signature
    c := volc.Credentials{
        AccessKeyID:     AK,
        SecretAccessKey: SK,
        Service:         ServiceName,
        Region:          Region,
    }
    req = c.Sign(req)
    return req
}

// buildRequestBody: request body to the current API, in JSON string format
func buildRequestJsonBody() string {
    return `{
        "monitor_types":[
            "crash"
        ],
        "query_key":"test alert",
        "status":[
        ],
        "page_no":1,
        "page_size":1
    }`
}
```





</Tab>
<Tab zoneid="iRSLK44Taf" title="Java">
<TabTitle>Java</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The dependency version must meet the requirement: volc\-sdk\-java version ≥ 1.0.133.</div>


```Java
package com.example.demo;

import com.volcengine.error.SdkError;
import com.volcengine.helper.Const;
import com.volcengine.model.ApiInfo;
import com.volcengine.model.Credentials;
import com.volcengine.model.ServiceInfo;
import com.volcengine.model.response.RawResponse;
import com.volcengine.service.BaseServiceImpl;
import org.apache.http.NameValuePair;
import org.apache.http.Header;
import org.apache.http.message.BasicHeader;
import org.apache.http.message.BasicNameValuePair;

import java.nio.charset.StandardCharsets;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

public class DemoService extends BaseServiceImpl {

    private static final String ServiceName = "apmplus_openapi";
    private static final String Host = "apmplus-openapi.cn-beijing.byteplusapi.com";
    private static final String Scheme = "https";
    private static final String Path = "/";
    private static final String AK = "xx";
    private static final String SK = "xx==";
    private static final String AppID = "123456";

    public DemoService(ServiceInfo info, Map<String, ApiInfo> apiInfoList) {
        super(info, null, apiInfoList);
    }

    public static void main(String[] args) throws Exception {

        String action = "AnalyseSummary"; // API name string, version = "2022-10-12"; // Version number

        Map<String, ApiInfo> apiInfoList = buildApiInfo(action, version);

        ServiceInfo serviceInfo = buildServiceInfo();

        DemoService service = new DemoService(serviceInfo, apiInfoList);
        service.setAccessKey(DemoService.AK);
        service.setSecretKey(DemoService.SK);

        RawResponse response = service.json(action, null, buildRequestJsonBody());
        if (response.getCode() != SdkError.SUCCESS.getNumber()) {
            System.out.println("errorNo:" + response.getCode());
            return;
        }
        System.out.println(new String(response.getData(), StandardCharsets.UTF_8));
    }

    /**
     * Request body to the current API, in JSON string format.
     * {
     * "os":"iOS",
     * "start_time":1658664000,
     * "end_time":1658750543,
     * "compare_start_time":1658577457,
     * "compare_end_time":1658664000,
     * "filters": {
     * "type":"and",
     * "sub_conditions":[
     * {
     * "dimension":"os",
     * "op":"in",
     * "type":"expression",
     * "values":["iOS"]
     * }
     * ]
     * },
     * "order_by":"count"
     * }
     */private static String buildRequestJsonBody() {
        return "{"os":"iOS","start_time":1658664000,"end_time":1658750543,"compare_start_time":1658577457,"compare_end_time":1658664000,"filters":{"type":"and","sub_conditions":[{"dimension":"os","op":"in","type":"expression","values":["iOS"]}]},"order_by":"count"}";
    }

    private static ServiceInfo buildServiceInfo() {
        return new ServiceInfo(new HashMap<String, Object>() {
            {
                put(Const.CONNECTION_TIMEOUT, 5000);
                put(Const.SOCKET_TIMEOUT, 5000);
                put(Const.Host, DemoService.Host);
                put(Const.Credentials, new Credentials(Const.REGION_CN_NORTH_1, DemoService.ServiceName));
                put(Const.Scheme, DemoService.Scheme);
            }
        });
    }

    private static Map<String, ApiInfo> buildApiInfo(final String action, final String version) {
        return new HashMap<String, ApiInfo>() {
            {
                put(action, new ApiInfo(
                        new HashMap<String, Object>() {
                            {
                                put(Const.Method, "POST");
                                put(Const.Path, DemoService.Path);
                                put(Const.Header, new ArrayList<Header>() {
                                    {
                                        add(new BasicHeader("x-app-ids", DemoService.AppID));
                                    }
                                });
                                put(Const.Query, new ArrayList<NameValuePair>() {
                                    {
                                        add(new BasicNameValuePair("Action", action));
                                        add(new BasicNameValuePair("Version", version));
                                    }
                                });
                            }
                        }));
            }
        };
    }

}
```



</Tab>
<Tab zoneid="HM6mWGAm7Q" title="Python">
<TabTitle>Python</TabTitle>

```Python
import json

from volcengine.ApiInfo import ApiInfo
from volcengine.Credentials import Credentials
from volcengine.ServiceInfo import ServiceInfo
from volcengine.base.Service import Service

# https://github.com/volcengine/volc-sdk-python# pip install --user volcengine# Request information
host = "apmplus-openapi.cn-beijing.byteplusapi.com"
ak = "xx"
sk = "xx=="
service = "apmplus_openapi"
region = "cn-beijing"
action = "GetAppAlarmRuleList"
version = "2022-10-12"
method = "POST"
params = {}
header = {
    "x-app-ids": "123456",
    "content-type": "application/json"
}
payload = {
    "monitor_types": ["crash"],
    "page_no": 1,
    "page_size": 1,
}

if __name__ == '__main__':
    s = Service(
        ServiceInfo(host, header, Credentials(ak, sk, service, region), 5, 5),
        {
          action: ApiInfo(method, "/", {"Action": action, "Version": version}, {}, {})
        }
    )
    resp = s.json(action, params, json.dumps(payload))
    print(resp)
```





</Tab>
</Tabs>


When calling the API, please modify the sample code with the corresponding Action, AppID, AK, SK, Service, and Region for the target API.
