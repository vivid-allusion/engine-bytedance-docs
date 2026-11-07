---
title: "Code samples—Content"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/samples-content_code_samples"
---

This section provides the implementation code samples for the Content Industry. You can refer to the code samples for your reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are still a lot of improvements being worked on. We will let you know when there are new updates.</div>


<span id="199bd60d"></span>
# Install the client library


<Tabs>
<Tab zoneid="K0ZgzciE2l" title="Go">
<TabTitle>Go</TabTitle>

```Go
// add this to "go.mod"
require github.com/byteplus-sdk/byteplus-sdk-go-rec latest

//or
go get github.com/byteplus-sdk/byteplus-sdk-go-rec
```



</Tab>
<Tab zoneid="As4WrJ6mxU" title="Python">
<TabTitle>Python</TabTitle>

```Python
pip install --upgrade byteplus-rec
```



</Tab>
<Tab zoneid="c5wer5gKeg" title="Java">
<TabTitle>Java</TabTitle>

```Java
<dependency>
    <groupId>com.byteplus</groupId>
    <artifactId>byteplus-sdk-java-rec</artifactId>
    <version>\\${latest}</version>
</dependency>
```



</Tab>
</Tabs>


<span id="e9d19f33"></span>
# Import the libraries


<Tabs>
<Tab zoneid="MBT9UUkBtm" title="Go">
<TabTitle>Go</TabTitle>

```Go
import (
        "encoding/json"
        "fmt"
        "os"
        "time"

        core "github.com/byteplus-sdk/byteplus-sdk-go-rec-core"
        "github.com/byteplus-sdk/byteplus-sdk-go-rec-core/logs"
        "github.com/byteplus-sdk/byteplus-sdk-go-rec-core/option"
        "github.com/byteplus-sdk/byteplus-sdk-go-rec/content"
        "github.com/byteplus-sdk/byteplus-sdk-go-rec/content/protocol"
        "github.com/byteplus-sdk/byteplus-sdk-go-rec/region"
        "github.com/google/uuid"
)
```



</Tab>
<Tab zoneid="Lo5wlSpSN4" title="Python">
<TabTitle>Python</TabTitle>

```Python
import json
import logging
import os
import time
import uuid
from datetime import timedelta
from signal import SIGKILL
from typing import Optional

from google.protobuf.message import Message

from byteplus_rec.region.region import Region
from byteplus_rec.content.content_client import Client
from byteplus_rec.content.content_client_builder import ClientBuilder
from byteplus_rec.content.constant import STAGE_TRIAL, STAGE_PRODUCTION, STAGE_INCREMENTAL
from byteplus_rec.content.example.mock_helper import mock_users, mock_contents, mock_user_events, mock_predict_content, \
    mock_device
from byteplus_rec.content.protocol import WriteResponse, WriteDataRequest, FinishWriteDataRequest, Date,\
    Scene, PredictRequest, PredictResponse, PredictResult, AckServerImpressionsRequest, AckServerImpressionsResponse
from byteplus_rec_core.exception import BizException, NetException
from byteplus_rec_core.http_caller import Config
from byteplus_rec_core.metrics.metrics_option import MetricsCfg
from byteplus_rec_core.option import Option
from byteplus_rec_core import utils
from byteplus_rec_core.status_helper import is_upload_success, is_success
```



</Tab>
<Tab zoneid="tuMUoSmlV9" title="Java">
<TabTitle>Java</TabTitle>

```Java
import com.alibaba.fastjson.JSON;
import com.byteplus.rec.core.BizException;
import com.byteplus.rec.core.NetException;
import com.byteplus.rec.core.Option;
import com.byteplus.rec.core.StatusHelper;
import com.byteplus.rec.sdk.content.ContentClient;
import com.byteplus.rec.sdk.content.ContentClientBuilder;
import com.byteplus.rec.sdk.region.Region;
import com.byteplus.rec.sdk.content.Constant;
import com.byteplus.rec.sdk.content.example.entity.DemoUser;
import com.byteplus.rec.sdk.content.example.entity.DemoUserEvent;
import com.byteplus.rec.sdk.content.example.entity.DemoContent;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.WriteDataRequest;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.WriteResponse;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.FinishWriteDataRequest;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.PredictRequest;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.Scene;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.Content;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.Device;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.PredictResponse;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.PredictResult;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.PredictResult.ResponseContent;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.AckServerImpressionsRequest;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.AckServerImpressionsRequest.AlteredContent;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.AckServerImpressionsResponse;
import com.byteplus.rec.sdk.content.protocol.ByteplusSaasContent.Date;
import lombok.extern.slf4j.Slf4j;
import org.jetbrains.annotations.NotNull;

import java.time.Duration;
import java.time.LocalDate;
import java.util.*;
```



</Tab>
</Tabs>


<span id="d8d400c0"></span>
# Initialize a client with AK/SK


<Tabs>
<Tab zoneid="NZB4n06AE5" title="Go">
<TabTitle>Go</TabTitle>

```Go
var ( 
        client content.Client 
) 
 
func init() { 
        logs.Level = logs.LevelDebug 
        var err error 
        client, err = content.NewClientBuilder(). 
                AccountID("***********"). // Required. The BytePlus account ID. 
                ProjectID(projectID). 
                Region(region.SG).     // Required. The region of the server used to provide service. 
                AuthAK("***********"). // Required. Access Key, used to generate request signature. 
                AuthSK("***********"). // Required. Secure key, used to generate request signature. 
                //KeepAlive(true). // Optional. 
                //CallerConfig(callerConfig). // Optional. 
                //MetricsConfig(metricsConfig). // Optional. 
                //Schema("https"). // Optional. 
                //Hosts([]string{"rec-api-sg1.recplusapi.com"}). // Optional. 
                Build() 
        if err != nil { 
                panic(fmt.Sprintf("byteplus rec sdk init err:%s", err.Error())) 
        } 
}
```



</Tab>
<Tab zoneid="buLnYmpsk0" title="Python">
<TabTitle>Python</TabTitle>

```Python
# Full Parameters
# try:
#     client: Client = ClientBuilder() \\
#         .account_id("***********") \\
#         .region(Region.SG) \\
#         .project_id(PROJECT_ID) \\
#         .auth_ak("***********") \\ # Access Key, used to generate request signature. Saas Standard projects should use.
#         .auth_sk("***********") \\ # Secure Key, used to generate request signature. Saas Standard projects should use.
# #         .air_auth_token("***********") \\ # The token of this project. Saas Premium projects should use.
#         .schema("https") \\ # Opitonal. The options are 'http', 'https'
#         .hosts(["rec-api-sg1.recplusapi.com"]) \\ # Optional. If you are not a Byteplus Standard Project, please use the domain name specified by hosts to access.
#         .keep_alive(True) \\ # Optional.
#         .caller_config(caller_config) \\ # Optional.
#         .metrics_config(metrics_config) \\ # Optional.
#         .build()
# except BizException as clientE:
#     log.error("fail to create byteplus rec client, msg:%s", clientE)
try: 
    client: Client = ClientBuilder() \\ 
        .account_id("***********") \\ 
        .region(Region.SG) \\ 
        .project_id(PROJECT_ID) \\ 
        .auth_ak("***********") \\ 
        .auth_sk("***********") \\ 
        .build() 
except BizException as clientE: 
    log.error("fail to create byteplus rec client, msg:%s", clientE)
```



</Tab>
<Tab zoneid="A3BvS7KQna" title="Java">
<TabTitle>Java</TabTitle>

```Java
@Slf4j 
public class Main { 
    private static RetailClient client; 
 
    static { 
        try { 
            client = new ContentClientBuilder() 
                    .accountID("*********")  // Required. The BytePlus account ID. 
                    .projectID(PROJECT_ID) 
                    .region(Region.SG)  // Required. The region of the server used to provide service. 
                    .authAK("*********")  // Required. Access Key, used to generate request signature. 
                    .authSK("*********")  // Required. Secure key, used to generate request signature. 
//                    .metricsConfig(metricsCfg) // Optional. 
//                    .keepAlive(true) // Optional. 
//                    .callerConfig(callerConfig) // Optional. 
//                    .schema("http") // Optional. 
//                    .hosts(Collections.singletonList("rec-api-sg1.recplusapi.com")) // Optional 
                    .build(); 
        } catch (BizException e) { 
            log.error("fail to create byteplus rec client", e); 
        } 
    } 
 
}
```



</Tab>
</Tabs>


<span id="1111c8cb"></span>
# Initialize a client with Token


<Tabs>
<Tab zoneid="xZ5uV0pZxp" title="Go">
<TabTitle>Go</TabTitle>

```Go
var ( 
        client content.Client 
) 
 
func init() { 
        logs.Level = logs.LevelDebug 
        var err error 
        client, err = content.NewClientBuilder(). 
                AccountID("***********"). // Required. The BytePlus account ID. 
                ProjectID(projectID). 
                Region(region.SG).     // Required. The region of the server used to provide service. 
                AirAuthToken("*************").  // Required. The token of this project. 
                //KeepAlive(true). // Optional. 
                //CallerConfig(callerConfig). // Optional. 
                //MetricsConfig(metricsConfig). // Optional. 
                //Schema("https"). // Optional. 
                //Hosts([]string{"rec-api-sg1.recplusapi.com"}). // Optional. 
                Build() 
        if err != nil { 
                panic(fmt.Sprintf("byteplus rec sdk init err:%s", err.Error())) 
        } 
}
```



</Tab>
<Tab zoneid="AwtpSrbHPr" title="Python">
<TabTitle>Python</TabTitle>

```Python
# Full Parameters
# try:
#     client: Client = ClientBuilder() \
#         .account_id("***********") \
#         .region(Region.SG) \
#         .project_id(PROJECT_ID) \
#         .air_auth_token("***********") \ # The token of this project. Saas Premium projects should use.
#         .schema("https") \ # Opitonal. The options are 'http', 'https'
#         .hosts(["rec-api-sg1.recplusapi.com"]) \ # Optional. If you are not a Byteplus Standard Project, please use the domain name specified by hosts to access.
#         .keep_alive(True) \ # Optional.
#         .caller_config(caller_config) \ # Optional.
#         .metrics_config(metrics_config) \ # Optional.
#         .build()
# except BizException as clientE:
#     log.error("fail to create byteplus rec client, msg:%s", clientE)

try:  
    client: Client = ClientBuilder() \  
        .account_id("***********") \  
        .region(Region.SG) \  
        .project_id(PROJECT_ID) \  
        .air_auth_token("***********")\ 
        .build()  
except BizException as clientE:  
    log.error("fail to create byteplus rec client, msg:%s", clientE)
```



</Tab>
<Tab zoneid="Rm2nYlvCPQ" title="Java">
<TabTitle>Java</TabTitle>

```Java
@Slf4j 
public class Main { 
    private static RetailClient client; 
 
    static { 
        try { 
            client = new ContentClientBuilder() 
                    .accountID("*********")  // Required. The BytePlus account ID. 
                    .projectID(PROJECT_ID) 
                    .region(Region.SG)  // Required. The region of the server used to provide service. 
                    .airAuthToken("***********")      // Required. The token of this project. 
//                    .metricsConfig(metricsCfg) // Optional. 
//                    .keepAlive(true) // Optional. 
//                    .callerConfig(callerConfig) // Optional. 
//                    .schema("http") // Optional. 
//                    .hosts(Collections.singletonList("rec-api-sg1.recplusapi.com")) // Optional 
                    .build(); 
        } catch (BizException e) { 
            log.error("fail to create byteplus rec client", e); 
        } 
    } 
 
}
```



</Tab>
</Tabs>


<span id="a5ee8cf2"></span>
# WriteUsers


<Tabs>
<Tab zoneid="N8mvMmx7ah" title="Go">
<TabTitle>Go</TabTitle>

```Go
func writeUsersExample() {
        // The WriteUsers API can transfer up to 2,000 items in one request.
        request := buildWriteUsersRequest(1)
        opts := defaultOptions(DefaultWriteTimeout)
        response, err := client.WriteUsers(request, opts...)
        if err != nil {
                logs.Error("write user occur err, msg:%v", err)
                return
        }
        if core.IsUploadSuccess(response.GetStatus().GetCode()) {
                logs.Info("write user success")
                return
        }
        logs.Error("write user find failure info, msg:%s errItems:%+v",
                response.GetStatus(), response.GetErrors())
}

func buildWriteUsersRequest(count int) *protocol.WriteDataRequest {
        users := mockUsers(count)
        marshalUsers := make([]string, 0, len(users))
        for _, user := range users {
                marshalUser, _ := json.Marshal(user)
                marshalUsers = append(marshalUsers, string(marshalUser))
        }
        return &protocol.WriteDataRequest{
                Stage: content.StageIncremental,
                Data:  marshalUsers,
                Extra: map[string]string{"extra_info": "extra"},
        }
}

func defaultOptions(timeout time.Duration) []option.Option {
        // All options are optional.
        opts := []option.Option{
                option.WithRequestID(uuid.NewString()),
                option.WithTimeout(timeout),
    // Optional. Add a header to a custom HTTP header collection.
                //option.WithHTTPHeader("key", "value"),
                // Optional. Add a query to a custom query collection.
                //option.WithHTTPQuery("key", "value"),
                // Optional. Specify the duration before a server timeout.
                // If it is not specified, it is expected that the server will process the data for the maximum amount of time.
                // If the processing duration exceeds the specified duration, the server will return the result immediately,
                // regardless of whether there is any remaining data that has not been processed.
                //option.WithServerTimeout(5000 * time.Millisecond),
        }
        return opts
}
```



</Tab>
<Tab zoneid="znxZFBJhmH" title="Python">
<TabTitle>Python</TabTitle>

```Python
def write_users_example():
    # The WriteUsers API can transfer up to 2,000 items in one request.
    request = _build_write_user_request(1)
    opts = _default_opts(DEFAULT_WRITE_TIMEOUT)
    try:
        # response: WriteResponse = utils.do_with_retry(client.write_users, request, opts, DEFAULT_RETRY_TIMES)
        response: WriteResponse = client.write_users(request, *opts)
    except BizException as e:
        log.error("write user occur err, msg:%s", e)
        return
    if is_upload_success(response.status.code):
        log.info("write user success")
        return
    log.error("write user find fail, msg:%s errItems:%s", response.status, response.errors)
    return


def _build_write_user_request(count: int) -> WriteDataRequest:
    request = WriteDataRequest()
    request.stage = STAGE_INCREMENTAL
    users = mock_users(count)

    user_str_list = [Optional[str]] * len(users)
    for i in range(len(users)):
        user_str_list[i] = json.dumps(users[i])

    request.data.extend(user_str_list)

    # Optional.
    # request.extra["extra_info"] = "value"
    return request


def _default_opts(timeout: timedelta) -> tuple:
    return (
        Option.with_timeout(timeout),
        Option.with_request_id(str(uuid.uuid1())),
        # Optional. Add a header to a custom header collection.
        #Option.with_http_header("key", "value"),
        # Optional. Add a query to a custom query collection.
        #Option.with_http_query("key", "value"),
        # Optional. Specify the duration of a request before a server timeout.
        # If it is not specified, it is expected that the server will process the data for the maximum amount of time.
        # If the processing time exceeds this time, the server will return the result immediately,
        # regardless of whether there is any remaining data that has not been processed.
        #Option.with_server_timeout(timedelta(milliseconds=5000))
    )
```



</Tab>
<Tab zoneid="WryFhsOwk4" title="Java">
<TabTitle>Java</TabTitle>

```Java
public class Main {
    public static void writeUsersExample() {
        // The WriteUsers API can transfer up to 2,000 items in one request.
        WriteDataRequest request = buildWriteUsersRequest(1);
        Option[] opts = defaultOptions(DEFAULT_WRITE_TIMEOUT);
        WriteResponse response;
        try {
            response = client.writeUsers(request, opts);
            //response = Utils.doWithRetry(client::writeUsers, request, opts, DEFAULT_RETRY_TIMES);
        } catch (NetException | BizException e) {
            log.error("write user occur err, msg:{}", e.getMessage());
            return;
        }
        if (StatusHelper.isUploadSuccess(response.getStatus().getCode())) {
            log.info("write user success");
            return;
        }
        log.error("write user find failure info, msg:{} errItems:{}",
                response.getStatus(), response.getErrorsList());
    }

    private static WriteDataRequest buildWriteUsersRequest(int count) {
        List<DemoUser> users = MockHelper.mockUsers(count);
        WriteDataRequest.Builder requestBuilder = WriteDataRequest.newBuilder()
                .setStage(Constant.STAGE_INCREMENTAL);
        for (DemoUser user : users) {
            requestBuilder.addData(JSON.toJSONString(user));
        }
        return requestBuilder.build();
    }

    private static Option[] defaultOptions(Duration timeout) {
        return new Option[]{
                // Required，The Request ID of each request must not repeat.
                // If it is not passed, the SDK will add it to each request by default.
                Option.withRequestID(UUID.randomUUID().toString()),
                // Optional. Specify the duration before a request timeout.
                Option.withTimeout(timeout),
                Option.withHTTPHeader("X-TT-ENV", "preview_prod")
                // Optional. Add a header to a custom header collection.
                //Option.withHTTPHeader("key", "value"),
                // Optional. Add a query to a custom query collection.
                //Option.withHTTPQuery("key", "value"),
                // Optional. Specify the duration before a server timeout.
                // If it is not specified, it is expected that the server will process the data for the maximum amount of time.
                // If the processing time exceeds this time, the server will return the result immediately,
                // regardless of whether there is any remaining data that has not been processed.
                //Option.withServerTimeout(Duration.ofMillis(5000))
        };
    }
}
```



</Tab>
</Tabs>


<span id="43ea86b4"></span>
# WriteContents


<Tabs>
<Tab zoneid="AsfIDbJNJI" title="Go">
<TabTitle>Go</TabTitle>

```Go
func writeContentsExample() {
        // The WriteContents API can transfer up to 2,000 items in one request.
        request := buildWriteContentsRequest(1)
        opts := defaultOptions(DefaultWriteTimeout)
        response, err := client.WriteContents(request, opts...)
        if err != nil {
                logs.Error("write content occur err, msg:%v", err)
                return
        }
        if core.IsUploadSuccess(response.GetStatus().GetCode()) {
                logs.Info("write content success")
                return
        }
        logs.Error("write content find failure info, msg:%s errItems:%+v",
                response.GetStatus(), response.GetErrors())
}

func buildWriteContentsRequest(count int) *protocol.WriteDataRequest {
        contents := mockContents(count)
        marshalContents := make([]string, 0, len(contents))
        for _, content := range contents {
                marshalContent, _ := json.Marshal(content)
                marshalContents = append(marshalContents, string(marshalContent))
        }
        return &protocol.WriteDataRequest{
                Stage: content.StageIncremental,
                Data:  marshalContents,
                Extra: map[string]string{"extra_info": "extra"},
        }
}

func defaultOptions(timeout time.Duration) []option.Option {
        // All options are optional.
        opts := []option.Option{
                option.WithRequestID(uuid.NewString()),
                option.WithTimeout(timeout),
                // Optional. Add a header to a custom HTTP header collection.
                //option.WithHTTPHeader("key", "value"),
                // Optional. Add a query to a custom query collection.
                //option.WithHTTPQuery("key", "value"),
    // Optional. Specify the duration before a server timeout.
    // If it is not specified, it is expected that the server will process the data for the maximum amount of time.
    // If the processing time exceeds this time, the server will return the result immediately,
    // regardless of whether there is any remaining data that has not been processed.
                //option.WithServerTimeout(5000 * time.Millisecond),
        }
        return opts
}
```



</Tab>
<Tab zoneid="vyKIlP8XNz" title="Python">
<TabTitle>Python</TabTitle>

```Python
def write_contents_example():
    # The WriteContents API can transfer up to 2,000 items in one request.
    request = _build_write_content_request(1)
    opts = _default_opts(DEFAULT_WRITE_TIMEOUT)
    try:
        #response: WriteResponse = utils.do_with_retry(client.write_contents, request, opts, DEFAULT_RETRY_TIMES)
        response: WriteResponse = client.write_contents(request, *opts)
    except BizException as e:
        log.error("write content occur err, msg:%s", e)
        return
    if is_upload_success(response.status.code):
        log.info("write content success")
        return
    log.error("write content find fail, msg:%s errItems:%s", response.status, response.errors)
    return


def _build_write_content_request(count: int) -> WriteDataRequest:
    request = WriteDataRequest()
    request.stage = STAGE_INCREMENTAL
    contents = mock_contents(count)
    content_str_list = [Optional[str]] * len(contents)
    for i in range(len(contents)):
        content_str_list[i] = json.dumps(contents[i])

    request.data.extend(content_str_list)

    # Optional.
    #request.extra["extra_info"] = "value"
    return request


def _default_opts(timeout: timedelta) -> tuple:
    return (
        Option.with_timeout(timeout),
        Option.with_request_id(str(uuid.uuid1())),   
        # Optional. Add a header to a custom header collection.
        #Option.with_http_header("key", "value"),
        # Optional. Add a query to a custom query collection.
        #Option.with_http_query("key", "value"),
        # Optional. Specify the duration before a server timeout.
        # If it is not specified, it is expected that the server will process the data for the maximum amount of time.
        # If the processing time exceeds this time, the server will return the result immediately,
        # regardless of whether there is any remaining data that has not been processed.
        #Option.with_server_timeout(timedelta(milliseconds=5000))
    )
```



</Tab>
<Tab zoneid="JuKZrVpoeh" title="Java">
<TabTitle>Java</TabTitle>

```Java
public class Main {
    public static void writeContentsExample() {
        // The WriteContents API can transfer up to 2,000 items in one request.
        WriteDataRequest request = buildWriteContentsRequest(1);
        Option[] options = defaultOptions(DEFAULT_WRITE_TIMEOUT);
        WriteResponse response;
        try {
            response = client.writeContents(request, options);
            //response = Utils.doWithRetry(client::writeContents, request, options, DEFAULT_RETRY_TIMES);
        } catch (BizException | NetException e) {
            log.error("write content occur err, msg:{}", e.getMessage());
            return;
        }
        if (StatusHelper.isUploadSuccess(response.getStatus().getCode())) {
            log.info("write content success");
            return;
        }
        log.error("write content find failure info, msg:{} errItems:{}",
                response.getStatus(), response.getErrorsList());
    }

    private static WriteDataRequest buildWriteContentsRequest(int count) {
        List<DemoContent> contents = MockHelper.mockContents(count);
        WriteDataRequest.Builder requestBuilder = WriteDataRequest.newBuilder()
                .setStage(Constant.STAGE_INCREMENTAL);
        for (DemoContent content : contents) {
            requestBuilder.addData(JSON.toJSONString(content));
        }
        return requestBuilder.build();
    }
    
    private static Option[] defaultOptions(Duration timeout) {
        return new Option[]{
                // Required，The Request ID of each request must not repeat.
                // If it is not passed, the SDK will add it to each request by default.
                Option.withRequestID(UUID.randomUUID().toString()),
                // Optional. Specify the duration before a request timeout.
                Option.withTimeout(timeout),
                Option.withHTTPHeader("X-TT-ENV", "preview_prod")
                // Optional. Add a header to a custom header collection.
                //Option.withHTTPHeader("key", "value"),
                // Optional. Add a query to a custom query collection.
                //Option.withHTTPQuery("key", "value"),
                // Optional. Specify the duration before a server timeout.
                // If it is not specified, it is expected that the server will process the data for the maximum amount of time.
                // If the processing time exceeds this time, the server will return the result immediately,
                // regardless of whether there is any remaining data that has not been processed.
                //Option.withServerTimeout(Duration.ofMillis(5000))
        };
    }
}
```



</Tab>
</Tabs>


<span id="67998495"></span>
# WriteUserEvents


<Tabs>
<Tab zoneid="u5VKqELRaS" title="Go">
<TabTitle>Go</TabTitle>

```Go
func writeUserEventsExample() {
        // The WriteUserEvents API can transfer up to 2,000 items in one request.
        request := buildWriteUserEventsRequest(1)
        opts := defaultOptions(DefaultWriteTimeout)
        response, err := client.WriteUserEvents(request, opts...)
        if err != nil {
                logs.Error("write user event occur err, msg:%v", err)
                return
        }
        if core.IsUploadSuccess(response.GetStatus().GetCode()) {
                logs.Info("write user event success")
                return
        }
        logs.Error("write user event find failure info, msg:%s errItems:%+v",
                response.GetStatus(), response.GetErrors())
}

func buildWriteUserEventsRequest(count int) *protocol.WriteDataRequest {
        userEvents := mockUserEvents(count)
        marshalUserEvents := make([]string, 0, len(userEvents))
        for _, userEvent := range userEvents {
                marshalUserEvent, _ := json.Marshal(userEvent)
                marshalUserEvents = append(marshalUserEvents, string(marshalUserEvent))
        }
        return &protocol.WriteDataRequest{
                Stage: content.StageIncremental,
                Data:  marshalUserEvents,
                Extra: map[string]string{"extra_info": "extra"},
        }
}

func defaultOptions(timeout time.Duration) []option.Option {
        // All options are optional.
        opts := []option.Option{
                option.WithRequestID(uuid.NewString()),
                option.WithTimeout(timeout),
                // Optional. Add a header to a custom http header collection.
                //option.WithHTTPHeader("key", "value"),
                // Optional. Add a query to a custom query collection.
                //option.WithHTTPQuery("key", "value"),
    // Optional. Specify the duration before a server timeout.
    // If it is not specified, it is expected that the server will process the data for the maximum amount of time.
    // If the processing time exceeds this time, the server will return the result immediately,
    // regardless of whether there is any remaining data that has not been processed.
                //option.WithServerTimeout(5000 * time.Millisecond),
        }
        return opts
}
```



</Tab>
<Tab zoneid="dxdBg1fcBR" title="Python">
<TabTitle>Python</TabTitle>

```Python
def write_user_events_example():
    # The WriteUserEvents API can transfer up to 2,000 items in one request.
    request = _build_write_user_event_request(1)
    opts = _default_opts(DEFAULT_WRITE_TIMEOUT)
    try:
        #response: WriteResponse = utils.do_with_retry(client.write_user_events, request, opts, DEFAULT_RETRY_TIMES)
        response: WriteResponse = client.write_user_events(request, *opts)
    except BizException as e:
        log.error("write user_event occur err, msg:%s", e)
        return
    if is_upload_success(response.status.code):
        log.info("write user_event success")
        return
    log.error("write user event find failure info, msg:%s errItems:%s", response.status, response.errors)
    return


def _build_write_user_event_request(count: int) -> WriteDataRequest:
    request = WriteDataRequest()
    request.stage = STAGE_INCREMENTAL
    user_events = mock_user_events(count)
    user_event_str_list = [Optional[str]] * len(user_events)
    for i in range(len(user_events)):
        user_event_str_list[i] = json.dumps(user_events[i])

    request.data.extend(user_event_str_list)

    # Optional.
    #request.extra["extra_info"] = "value"
    return request


def _default_opts(timeout: timedelta) -> tuple:
    return (
        Option.with_timeout(timeout),
        Option.with_request_id(str(uuid.uuid1())),
        # Optional. Add a header to a custom header collection.
        #Option.with_http_header("key", "value"),
        # Optional. Add a query to a custom query collection.
        #Option.with_http_query("key", "value"),
        # Optional. Specify the duration before a server timeout.
        # If it is not specified, it is expected that the server will process the data for the maximum amount of time.
        # If the processing time exceeds this time, the server will return the result immediately,
        # regardless of whether there is any remaining data that has not been processed.
        #Option.with_server_timeout(timedelta(milliseconds=5000))
    )
```



</Tab>
<Tab zoneid="fykxbM51pG" title="Java">
<TabTitle>Java</TabTitle>

```Java
public class Main {
    public static void writeUserEventsExample() {
        // The WriteUserEvents API can transfer up to 2,000 items in one request.
        WriteDataRequest request = buildWriteUserEventsRequest(1);
        Option[] options = defaultOptions(DEFAULT_WRITE_TIMEOUT);
        WriteResponse response;
        try {
            response = client.writeUserEvents(request, options);
            //response = Utils.doWithRetry(client::writeUserEvents, request, options, DEFAULT_RETRY_TIMES);
        } catch (BizException | NetException e) {
            log.error("write user events occur err, msg:{}", e.getMessage());
            return;
        }
        if (StatusHelper.isUploadSuccess(response.getStatus().getCode())) {
            log.info("write user events success");
            return;
        }
        log.error("write user events find failure info, msg:{} errItems:{}",
                response.getStatus(), response.getErrorsList());
    }

    private static WriteDataRequest buildWriteUserEventsRequest(int count) {
        List<DemoUserEvent> userEvents = MockHelper.mockUserEvents(count);
        WriteDataRequest.Builder requestBuilder = WriteDataRequest.newBuilder()
                .setStage(Constant.STAGE_INCREMENTAL);
        for (DemoUserEvent userEvent : userEvents) {
            requestBuilder.addData(JSON.toJSONString(userEvent));
        }
        return requestBuilder.build();
    }

    private static Option[] defaultOptions(Duration timeout) {
        return new Option[]{
                // Required，The Request ID of each request must not repeat.
                // If it is not passed, the SDK will add it to each request by default.
                Option.withRequestID(UUID.randomUUID().toString()),
                // Optional. Specify the duration before a request timeout.
                Option.withTimeout(timeout),
                Option.withHTTPHeader("X-TT-ENV", "preview_prod")
                // Optional. Add a header to a custom header collection.
                //Option.withHTTPHeader("key", "value"),
                // Optional. Add a query to a custom query collection.
                //Option.withHTTPQuery("key", "value"),
                // Optional. Specify the duration before a server timeout.
                // If it is not specified, it is expected that the server will process the data for the maximum amount of time.
                // If the processing time exceeds this time, the server will return the result immediately,
                // regardless of whether there is any remaining data that has not been processed.
                //Option.withServerTimeout(Duration.ofMillis(5000))
        };
    }
}
```



</Tab>
</Tabs>


<span id="5044df3b"></span>
# Predict and AckServerImpressions


<Tabs>
<Tab zoneid="glf0xYi7pd" title="Go">
<TabTitle>Go</TabTitle>

```Go
func recommendExample() {
        predictRequest := buildPredictRequest()
        predictOpts := defaultOptions(DefaultPredictTimeout)
        // "home" is the scene name, which is provided by ByteDance.
        response, err := client.Predict(predictRequest, predictOpts...)
        if err != nil {
                logs.Error("predict occur error, msg:%v", err)
                return
        }
        if !core.IsSuccess(response.GetStatus().GetCode()) {
                logs.Error("predict find failure info, msg:%s", response.GetStatus())
                return
        }
        logs.Info("predict success")
        // The content, which are eventually shown to the user, should be sent back to ByteDance for de-duplication.
        alteredContents := recommendWithPredictResult(response.GetContentValue())
        ackRequest := buildAckRequest(response.GetRequestId(), predictRequest, alteredContents)
        ackOpts := defaultOptions(DefaultAckImpressionsTimeout)
        // async ack the actual impressions after this recommendation
        core.AsyncExecute(func() {
                _ = core.DoWithRetry(DefaultRetryTimes, func() error {
                        _, err := client.AckServerImpressions(ackRequest, ackOpts...)
                        return err
                })
        })
}

func buildPredictRequest() *protocol.PredictRequest {
        scene := &protocol.Scene{
                Offset: 10,
        }
        rootContent := mockPredictContent()
        device := mockPredictDevice()
        context := &protocol.PredictRequest_Context{
                RootContent:       rootContent,
                Device:            device,
                CandidateContents: []*protocol.Content{mockPredictContent()},
        }
        return &protocol.PredictRequest{
                ModelId:        modelID,
                UserId:         "1457789",
                Size:           20,
                Scene:          scene,
                ContentContext: context,
                //Extra:     map[string]string{"extra_info": "extra"},
        }
}

func recommendWithPredictResult(
        predictResult *protocol.PredictResult) []*protocol.AckServerImpressionsRequest_AlteredContent {
    // You can handle the recommendation results here, such as filter, insert other items, sort again, and so on.
    // The list of content finally displayed to user and the filtered content should be sent back to ByteDance for de-duplication.
        return conv2AlteredContents(predictResult.GetResponseContents())
}

func conv2AlteredContents(
        contents []*protocol.PredictResult_ResponseContent) []*protocol.AckServerImpressionsRequest_AlteredContent {
        if len(contents) == 0 {
                return nil
        }
        alteredContents := make([]*protocol.AckServerImpressionsRequest_AlteredContent, len(contents))
        for i, aContent := range contents {
                alteredContents[i] = &protocol.AckServerImpressionsRequest_AlteredContent{
                        AlteredReason: "kept",
                        ContentId:     aContent.GetContentId(),
                        Rank:          int32(i + 1),
                }
        }
        return alteredContents
}

func buildAckRequest(predictRequestId string, predictRequest *protocol.PredictRequest,
        alteredContents []*protocol.AckServerImpressionsRequest_AlteredContent) *protocol.AckServerImpressionsRequest {

        return &protocol.AckServerImpressionsRequest{
                ModelId:          predictRequest.GetModelId(),
                PredictRequestId: predictRequestId,
                UserId:           predictRequest.GetUserId(),
    // If the recommendation result is from BytePlus, the traffic_source will be byteplus.
    // If it is the customer's own recommendation result, the traffic_source wull be self.
                TrafficSource:   "byteplus",
                Scene:           predictRequest.GetScene(),
                AlteredContents: alteredContents,
                // Extra:            map[string]string{"ip": "127.0.0.1"},
        }
}

func defaultOptions(timeout time.Duration) []option.Option {
        // All options are optional.
        opts := []option.Option{
                option.WithRequestID(uuid.NewString()),
                option.WithTimeout(timeout),
                // Optional. Add a header to a custom http header collection.
                //option.WithHTTPHeader("key", "value"),
                // Optional. Add a query to a custom query collection.
                //option.WithHTTPQuery("key", "value"),
    // Optional. Specify the duration before a server timeout.
    // If it is not specified, it is expected that the server will process the data for the maximum amount of time.
    // If the processing time exceeds this time, the server will return the result immediately,
    // regardless of whether there is any remaining data that has not been processed.
                //option.WithServerTimeout(5000 * time.Millisecond),
        }
        return opts
}
```



</Tab>
<Tab zoneid="DgcH1azBXu" title="Python">
<TabTitle>Python</TabTitle>

```Python
def recommend_example():
    predict_request = _build_predict_request()
    predict_opts = _default_opts(DEFAULT_PREDICT_TIMEOUT)
    try:
        predict_response = client.predict(predict_request, *predict_opts)
    except (NetException, BizException) as e:
        log.error("predict occur error, msg:%s", e)
        return
    if not is_success(predict_response.status.code):
        log.error("predict find failure info, rsp:\n%s", predict_response)
        return
    log.info("predict success")
    # The content, which are eventually shown to the user, should be sent back to ByteDance for de-duplication.
    altered_contents = do_something_with_predict_result(predict_response.content_value)
    ack_request = _build_ack_impressions_request(predict_response.request_id, predict_request, altered_contents)
    ack_opts = _default_opts(DEFAULT_ACK_IMPRESSIONS_TIMEOUT)
    try:
        utils.do_with_retry(client.ack_server_impressions, ack_request, ack_opts, DEFAULT_RETRY_TIMES)
    except Exception as e:
        log.error("[AckServerImpressions] occur error, msg:%s", e)


def _build_predict_request() -> PredictRequest:
    request = PredictRequest()
    request.model_id = MODEL_ID
    request.user_id = "1457789"
    request.size = 20

    scene = request.scene
    scene.offset = 10

    ctx = request.content_context
    ctx.candidate_contents.extend([mock_predict_content()])
    ctx.root_content.CopyFrom(mock_predict_content())
    ctx.device.CopyFrom(mock_device())

    #request.extra["extra_info"] = "extra"
    return request


def do_something_with_predict_result(predict_result):
    # You can handle the recommendation results here, such as filter, insert other items, sort again, and so on.
    # The list of content finally displayed to user and the filtered content should be sent back to ByteDance for de-duplication.
    return conv_to_altered_contents(predict_result.response_contents)


def conv_to_altered_contents(content_results):
    if content_results is None or len(content_results) == 0:
        return
    size = len(content_results)
    altered_contents = [Optional[AckServerImpressionsRequest.AlteredContent]] * size
    for i in range(size):
        content_result = content_results[i]
        altered_content = AckServerImpressionsRequest.AlteredContent()
        altered_content.altered_reason = "kept"
        altered_content.content_id = content_result.content_id
        altered_content.rank = content_result.rank
        altered_contents[i] = altered_content
    return altered_contents


def _build_ack_impressions_request(predict_request_id: str, predict_request: PredictRequest, altered_contents: list):
    request = AckServerImpressionsRequest()
    request.model_id = predict_request.model_id
    request.predict_request_id = predict_request_id
    request.user_id = predict_request.user_id
    # If the recommendation result is from BytePlus, the traffic_source will be byteplus.
    # If it is the customer's own recommendation result, the traffic_source wull be self.
    request.traffic_source = "byteplus"
    scene: Message = request.scene
    scene.CopyFrom(predict_request.scene)
    request.altered_contents.extend(altered_contents)

    #request.extra["ip"] = "127.0.0.1"
    return request


def _default_opts(timeout: timedelta) -> tuple:
    return (
        Option.with_timeout(timeout),
        Option.with_request_id(str(uuid.uuid1())),
        # Optional. Add a header to a custom header collection.
        #Option.with_http_header("key", "value"),
        # Optional. Add a query to a custom query collection.
        #Option.with_http_query("key", "value"),
        # Optional. Specify the duration before a server timeout.
        # If it is not specified, it is expected that the server will process the data for the maximum amount of time.
        # If the processing time exceeds this time, the server will return the result immediately,
        # regardless of whether there is any remaining data that has not been processed.
        #Option.with_server_timeout(timedelta(milliseconds=5000))
    )
```



</Tab>
<Tab zoneid="PPVnYf8Cqd" title="Java">
<TabTitle>Java</TabTitle>

```Java
public class Main {
    public static void recommendExample() {
        PredictRequest predictRequest = buildPredictRequest();
        Option[] predict_opts = defaultOptions(DEFAULT_PREDICT_TIMEOUT);
        PredictResponse response;
        try {
            response = client.predict(predictRequest, predict_opts);
        } catch (Exception e) {
            log.error("predict occur error, msg:{}", e.getMessage());
            return;
        }
        if (!StatusHelper.isSuccess(response.getStatus().getCode())) {
            log.error("predict find failure info, msg:{}", response.getStatus());
            return;
        }
        log.info("predict success");
        // The content, which are eventually shown to the user, should be sent back to ByteDance for de-duplication.
        List<AlteredContent> alteredContents = doSomethingWithPredictResult(response.getContentValue());
        AckServerImpressionsRequest ackRequest =
                buildAckRequest(response.getRequestId(), predictRequest, alteredContents);
        Option[] ack_opts = defaultOptions(DEFAULT_ACK_IMPRESSIONS_TIMEOUT);
        //Utils.Callable<AckServerImpressionsResponse, AckServerImpressionsRequest> call
        //       = (req, optList) -> client.ackServerImpressions(req, optList);
        try {
            //Utils.doWithRetry(call, ackRequest, ack_opts, DEFAULT_RETRY_TIMES);
            client.ackServerImpressions(ackRequest, ack_opts);
        } catch (Exception e) {
            log.error("[AckServerImpressions] occur error, msg:{}", e.getMessage());
        }
    }

    private static PredictRequest buildPredictRequest() {
        Scene scene = Scene.newBuilder()
                .setOffset(10)
                .build();
        Content rootContent = MockHelper.mockPredictContent();
        Device device = MockHelper.mockDevice();

        List<Content> candidateContents = Arrays.asList(
                MockHelper.mockPredictContent(),
                MockHelper.mockPredictContent()
        );

        PredictRequest.Context context = PredictRequest.Context.newBuilder()
                .setRootContent(rootContent)
                .setDevice(device)
                .addAllCandidateContents(candidateContents)
                .build();

        return PredictRequest.newBuilder()
                .setModelId(MODEL_ID)
                .setUserId("1457789")
                .setSize(20)
                .setScene(scene)
                .setContentContext(context)
                //.putExtra("extra_inio", "extra")
                .build();
    }

    private static List<AlteredContent> doSomethingWithPredictResult(PredictResult predictResult) {
        // The recommendation results are handled here, such as filter, insert other items, sort again, and so on.
        // The list of content finally displayed to user and the filtered content should be sent back to ByteDance for de-duplication.
        return conv2AlteredContents(predictResult.getResponseContentsList());
    }

    @NotNull
    private static List<AlteredContent> conv2AlteredContents(List<ResponseContent> contents) {
        if (Objects.isNull(contents) || contents.isEmpty()) {
            return Collections.emptyList();
        }
        List<AlteredContent> alteredContents = new ArrayList<>(contents.size());
        for (int i = 0; i < contents.size(); i++) {
            ResponseContent responseContent = contents.get(i);
            AlteredContent alteredContent = AlteredContent.newBuilder()
                    .setAlteredReason("kept")
                    .setContentId(responseContent.getContentId())
                    .setRank(i + 1)
                    .build();

            alteredContents.add(alteredContent);
        }
        return alteredContents;
    }

    private static AckServerImpressionsRequest buildAckRequest(
            String predictRequestId,
            PredictRequest predictRequest,
            List<AlteredContent> alteredContents) {

        return AckServerImpressionsRequest.newBuilder()
                .setModelId(predictRequest.getModelId())
                .setPredictRequestId(predictRequestId)
                .setUserId(predictRequest.getUserId())
                .setScene(predictRequest.getScene())
                // If the recommendation result is from BytePlus, the traffic_source will be byteplus.
                // If it is the customer's own recommendation result, the traffic_source wull be self.
                .setTrafficSource("byteplus")
                .addAllAlteredContents(alteredContents)
                //.putExtra("ip", "127.0.0.1")
                .build();
    }

    private static Option[] defaultOptions(Duration timeout) {
        return new Option[]{
                // Required，The Request ID of each request must not repeat.
                // If it is not passed, the SDK will add it to each request by default.
                Option.withRequestID(UUID.randomUUID().toString()),
                // Optional. Specify the duration before a request timeout.
                Option.withTimeout(timeout),
                Option.withHTTPHeader("X-TT-ENV", "preview_prod")
                // Optional. Add a header to a custom header collection.
                //Option.withHTTPHeader("key", "value"),
                // Optional. Add a query to a custom query collection.
                //Option.withHTTPQuery("key", "value"),
                // Optional. Specify the duration before a server timeout.
                // If it is not specified, it is expected that the server will process the data for the maximum amount of time.
                // If the processing time exceeds this time, the server will return the result immediately,
                // regardless of whether there is any remaining data that has not been processed.
                //Option.withServerTimeout(Duration.ofMillis(5000))
        };
    }
}
```



</Tab>
</Tabs>
