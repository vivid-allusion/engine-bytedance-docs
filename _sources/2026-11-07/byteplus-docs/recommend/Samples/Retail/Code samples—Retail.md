---
title: "Code samples—Retail"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/samples-retail_code_samples"
---

This section provides the implementation code samples for the Retail/E\-commerce Industry. You can refer to the code samples for your reference.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">There are still a lot of improvements being worked on. We will let you know when there are new updates.</div>


<span id="426394fa"></span>
# Install the client library


<Tabs>
<Tab zoneid="jar4hihmBj" title="Go">
<TabTitle>Go</TabTitle>

```Go
// add this to "go.mod"
require github.com/byteplus-sdk/byteplus-sdk-go-rec latest

//or
go get github.com/byteplus-sdk/byteplus-sdk-go-rec
```



</Tab>
<Tab zoneid="xCE0y006xH" title="Python">
<TabTitle>Python</TabTitle>

```Python
pip install --upgrade byteplus-rec
```



</Tab>
<Tab zoneid="CpyUYEtZJm" title="Java">
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


<span id="a2731bab"></span>
# Import the libraries


<Tabs>
<Tab zoneid="hg2DBNV8iP" title="Go">
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
    "github.com/byteplus-sdk/byteplus-sdk-go-rec/region"
    "github.com/byteplus-sdk/byteplus-sdk-go-rec/retail"
    "github.com/byteplus-sdk/byteplus-sdk-go-rec/retail/protocol"
    "github.com/google/uuid"
)
```



</Tab>
<Tab zoneid="xjAfKFCfcO" title="Python">
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
from byteplus_rec.retail.retail_client import Client
from byteplus_rec.retail.retail_client_builder import ClientBuilder
from byteplus_rec.retail.constant import STAGE_TRIAL, STAGE_PRODUCTION, STAGE_INCREMENTAL
from byteplus_rec.retail.example.mock_helper import mock_users, mock_products, mock_user_events, \
    mock_device, mock_predict_product
from byteplus_rec.retail.protocol import WriteResponse, WriteDataRequest, FinishWriteDataRequest, PredictRequest, \
    AckServerImpressionsRequest, Date
from byteplus_rec_core import utils
from byteplus_rec_core.exception import BizException, NetException
from byteplus_rec_core.http_caller import Config
from byteplus_rec_core.metrics.metrics_option import MetricsCfg
from byteplus_rec_core.option import Option
from byteplus_rec_core.status_helper import is_upload_success, is_success
```



</Tab>
<Tab zoneid="pQjhq89u9N" title="Java">
<TabTitle>Java</TabTitle>

```Java
import com.alibaba.fastjson.JSON;
import com.byteplus.rec.core.*;
import com.byteplus.rec.core.HTTPCaller.Config;
import com.byteplus.rec.core.metrics.MetricsCollector.MetricsCfg;
import com.byteplus.rec.core.metrics.MetricsCollector;
import com.byteplus.rec.sdk.region.Region;
import com.byteplus.rec.sdk.retail.Constant;
import com.byteplus.rec.sdk.retail.RetailClient;
import com.byteplus.rec.sdk.retail.RetailClientBuilder;
import com.byteplus.rec.sdk.retail.example.entity.DemoProduct;
import com.byteplus.rec.sdk.retail.example.entity.DemoUser;
import com.byteplus.rec.sdk.retail.example.entity.DemoUserEvent;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.AckServerImpressionsRequest;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.AckServerImpressionsRequest.AlteredProduct;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.Device;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.PredictRequest;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.PredictResponse;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.PredictResult;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.PredictResult.ResponseProduct;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.Product;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.Scene;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.WriteDataRequest;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.WriteResponse;
import com.byteplus.rec.sdk.retail.protocol.ByteplusSaasRetail.FinishWriteDataRequest;
import lombok.extern.slf4j.Slf4j;
import okhttp3.ConnectionPool;
import okhttp3.OkHttpClient;
import org.jetbrains.annotations.NotNull;

import java.time.Duration;
import java.time.LocalDate;
import java.util.*;
import java.util.concurrent.TimeUnit;
```



</Tab>
</Tabs>


<span id="d73cd59f"></span>
# Initialize a client with AK/SK


<Tabs>
<Tab zoneid="RJvcWrgzgp" title="Go">
<TabTitle>Go</TabTitle>

```Go
var ( 
    client retail.Client 
) 
 
func init() { 
    logs.Level = logs.LevelDebug 
    var err error 
    client, err = retail.NewClientBuilder(). 
        AccountID("***********").      // Required. The BytePlus account ID. 
        ProjectID(projectID). 
        Region(region.SG).             // Required. The region of the server used to provide service. 
        AuthAK("***********").         // Required. Access Key, used to generate request signature. 
        AuthSK("***********").         // Required. Secure key, used to generate request signature. 
        //KeepAlive(true).             // Optional. 
        //CallerConfig(callerConfig).  // Optional. 
        //MetricsConfig(metricsConfig) // Optional. 
        //Schema("https").             // Optional. 
        //Hosts([]string{"rec-api-sg1.recplusapi.com"}). // Optional. 
        Build() 
    if err != nil { 
        panic(fmt.Sprintf("byteplus rec sdk init err:%s", err.Error())) 
    } 
}
```



</Tab>
<Tab zoneid="lmCARfBikU" title="Python">
<TabTitle>Python</TabTitle>

```Python
# Full Parameters
# try:
#     client: Client = ClientBuilder() \
#         .account_id("***********") \
#         .region(Region.SG) \
#         .project_id(PROJECT_ID) \
#         .auth_ak("***********") \ # Access Key, used to generate request signature. Saas Standard projects should use.
#         .auth_sk("***********") \ # Secure Key, used to generate request signature. Saas Standard projects should use.
# #         .air_auth_token("***********") \ # The token of this project. Saas Premium projects should use.
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
        .account_id("***********") \  #Required. The BytePlus account ID. 
        .region(Region.SG) \          #Required. The region of the server used to provide service. 
        .project_id(PROJECT_ID) \ 
        .auth_ak("***********") \     #Required. Access Key, used to generate request signature. 
        .auth_sk("***********") \     #Required. Secure key, used to generate request signature. 
        .build() 
except BizException as clientE: 
    log.error("fail to create byteplus rec client, msg:%s", clientE)
```



</Tab>
<Tab zoneid="ktvU55sKI6" title="Java">
<TabTitle>Java</TabTitle>

```Java
@Slf4j 
public class Main { 
    private static RetailClient client; 
 
    static { 
        try { 
            client = new RetailClientBuilder() 
                    .accountID("*********")      // Required. The BytePlus account ID. 
                    .projectID(PROJECT_ID) 
                    .region(Region.SG)           // Required. The region of the server used to provide service. 
                    .authAK("*********")         // Required. Access Key, used to generate request signature. 
                    .authSK("*********")         // Required. Secure key, used to generate request signature. 
//                    .metricsConfig(metricsCfg) // Optional. 
//                    .keepAlive(true)           // Optional. 
//                    .callerConfig(callerConfig)// Optional. 
//                    .schema("http")            // Optional. 
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


<span id="d4fa7c66"></span>
# Initialize a client with Token


<Tabs>
<Tab zoneid="OriwHhfqTn" title="Go">
<TabTitle>Go</TabTitle>

```Go
var ( 
    client retail.Client 
) 
 
func init() { 
    logs.Level = logs.LevelDebug 
    var err error 
    client, err = retail.NewClientBuilder(). 
        AccountID("***********").      // Required. The BytePlus account ID. 
        ProjectID(projectID). 
        Region(region.SG).             // Required. The region of the server used to provide service. 
        AirAuthToken("*************").  // Required. The token of this project. 
        //KeepAlive(true).             // Optional. 
        //CallerConfig(callerConfig).  // Optional. 
        //MetricsConfig(metricsConfig) // Optional. 
        //Schema("https").             // Optional. 
        //Hosts([]string{"rec-api-sg1.recplusapi.com"}). // Optional. 
        Build() 
    if err != nil { 
        panic(fmt.Sprintf("byteplus rec sdk init err:%s", err.Error())) 
    } 
}
```



</Tab>
<Tab zoneid="quS7jGYWxF" title="Python">
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
<Tab zoneid="CYE8pWG7NY" title="Java">
<TabTitle>Java</TabTitle>

```Java
@Slf4j 
public class Main { 
    private static RetailClient client; 
 
    static { 
        try { 
            client = new RetailClientBuilder() 
                    .accountID("*********")      // Required. The BytePlus account ID. 
                    .projectID(PROJECT_ID) 
                    .region(Region.SG)           // Required. The region of the server used to provide service. 
                    .airAuthToken("***********")      // Required. The token of this project. 
//                    .metricsConfig(metricsCfg) // Optional. 
//                    .keepAlive(true)           // Optional. 
//                    .callerConfig(callerConfig)// Optional. 
//                    .schema("http")            // Optional. 
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


<span id="f7e65c2f"></span>
# WriteUsers


<Tabs>
<Tab zoneid="hnx0ZzT5aJ" title="Go">
<TabTitle>Go</TabTitle>

```Go
func writeUsersExample() {
        // The WriteUsers API can transfer up to 2,000 items in one request.
        request := buildWriteUsersRequest(200)
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
                Stage: retail.StageIncremental,
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
<Tab zoneid="X8Yctd3dcu" title="Python">
<TabTitle>Python</TabTitle>

```Python
def write_users_example():
    # The WriteUsers API can transfer up to 2,000 items in one request.
    request = _build_write_user_request(1)
    opts = _default_opts(DEFAULT_WRITE_TIMEOUT)
    try:
        #response: WriteResponse = utils.do_with_retry(client.write_users, request, opts, DEFAULT_RETRY_TIMES)
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
        # Optional. Specify the duration of a request before a server timeout.
        # If it is not specified, it is expected that the server will process the data for the maximum amount of time.
        # If the processing time exceeds this time, the server will return the result immediately,
        # regardless of whether there is any remaining data that has not been processed.
        #Option.with_server_timeout(timedelta(milliseconds=5000))
    )
```



</Tab>
<Tab zoneid="hx67T49VMc" title="Java">
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
                // Required. The Request ID of each request must not repeat.
                // If it is not passed, the SDK will add it to each request by default.
                Option.withRequestID(UUID.randomUUID().toString()),
                // Optional. Specify the duration before a request timeout.
                Option.withTimeout(timeout),
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


<span id="1166b886"></span>
# WriteProducts


<Tabs>
<Tab zoneid="Wh7ADnbNtx" title="Go">
<TabTitle>Go</TabTitle>

```Go
func writeProductsExample() {
    // The WriteProducts API can transfer up to 2,000 items in one request.
    request := buildWriteProductsRequest(1)
    opts := defaultOptions(DefaultWriteTimeout)
    response, err := client.WriteProducts(request, opts...)
    if err != nil {
        logs.Error("write product occur err, msg:%s", err.Error())
        return
    }
    if core.IsUploadSuccess(response.GetStatus().GetCode()) {
        logs.Info("write product success")
        return
    }
    logs.Error("write product find failure info, msg:%s errItems:%+v",
        response.GetStatus(), response.GetErrors())
}

func buildWriteProductsRequest(count int) *protocol.WriteDataRequest {
    products := mockProducts(count)
    marshalProducts := make([]string, 0, len(products))
    for _, product := range products {
        marshalProduct, _ := json.Marshal(product)
        marshalProducts = append(marshalProducts, string(marshalProduct))
    }
    return &protocol.WriteDataRequest{
        ProjectId: projectID,
        Stage:     retail.StageTrial,
        Data:      marshalProducts,
        Extra:     map[string]string{"extra_info": "extra"},
    }
}

func defaultOptions(timeout time.Duration) []option.Option {
    // All options are optional.
    //var customerHeaders map[string]string
    //var customerQueries map[string]string
    opts := []option.Option{
        option.WithRequestId(uuid.NewString()),
        option.WithTimeout(timeout),
        // Optional. Add a set of headers to the request, which will be overwritten by multiple calls.
        //option.WithHeaders(customerHeaders),
        // Optional. Add a set of queries to the request, which will be overwritten by multiple calls.
        //option.WithQueries(customerQueries),
        // Optional. Add a header to an existing custom header collection.
        //option.WithHeader("key", "value"),
        // Optional. Add a query to an existing custom query collection.
        //option.WithQuery("key", "value"),
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
<Tab zoneid="JFnwE5jzdn" title="Python">
<TabTitle>Python</TabTitle>

```Python
def write_products_example():
    # The WriteProducts API can transfer up to 2,000 items in one request.
    request = _build_write_product_request(1)
    opts = _default_opts(DEFAULT_WRITE_TIMEOUT)
    try:
        response: WriteResponse = client.write_products(request, *opts)
    except BizException as e:
        log.error("write product occur err, msg:%s", e)
        return
    if is_upload_success(response.status.code):
        log.info("write product success")
        return
    log.error("write product find fail, msg:%s errItems:%s", response.status, response.errors)
    return


def _build_write_product_request(count: int) -> WriteDataRequest:
    request = WriteDataRequest()
    request.project_id = PROJECT_ID
    request.stage = STAGE_TRIAL
    products = mock_products(count)
    product_str_list = [None] * len(products)
    for i in range(len(products)):
        product_str_list[i] = json.dumps(products[i])

    request.data.extend(product_str_list)

    # Optional.
    #request.extra["extra_info"] = "value"
    return request


def _default_opts(timeout: timedelta) -> tuple:
    #customer_headers = {}
    #customer_queries = {}
    return (
        Option.with_timeout(timeout),
        Option.with_request_id(str(uuid.uuid1())),
        # Optional. Add a set of customer headers to the request, which will be overwritten by multiple calls.
        #Option.with_headers(customer_headers),
        # Optional. Add a set of customer queries to the request, which will be overwritten by multiple calls.
        #Option.with_queries(customer_queries),
        # Optional. Add a header to an existing custom header collection.
        #Option.with_header("key", "value"),
        # Optional. Add a query to an existing custom query collection.
        #Option.with_query("key", "value"),
        # Optional. Specify the duration before a server timeout.
        # If it is not specified, it is expected that the server will process the data for the maximum amount of time.
        # If the processing time exceeds this time, the server will return the result immediately,
        # regardless of whether there is any remaining data that has not been processed.
        #Option.with_server_timeout(timedelta(milliseconds=5000))
    )
```



</Tab>
<Tab zoneid="mUvf5WAOgS" title="Java">
<TabTitle>Java</TabTitle>

```Java
public class Main {
    public static void writeProductsExample() {
        // The WriteProducts API can transfer up to 2,000 items in one request.
        WriteDataRequest request = buildWriteProductsRequest(1);
        Option[] options = defaultOptions(DEFAULT_WRITE_TIMEOUT);
        WriteResponse response;
        try {
            response = Utils.doWithRetry(client::writeProducts, request, options, DEFAULT_RETRY_TIMES);
        } catch (BizException e) {
            log.error("write product occur err, msg:{}", e.getMessage());
            return;
        }
        if (StatusHelper.isUploadSuccess(response.getStatus().getCode())) {
            log.info("write product success");
            return;
        }
        log.error("write product find failure info, msg:{} errItems:{}",
                response.getStatus(), response.getErrorsList());
    }

    private static WriteDataRequest buildWriteProductsRequest(int count) {
        List<DemoProduct> products = MockHelper.mockProducts(count);
        WriteDataRequest.Builder requestBuilder = WriteDataRequest.newBuilder();
        requestBuilder.setProjectId(PROJECT_ID);
        requestBuilder.setStage(Constant.STAGE_TRIAL);
        for (DemoProduct product : products) {
            requestBuilder.addData(JSON.toJSONString(product));
        }
        return requestBuilder.build();
    }
    
    private static Option[] defaultOptions(Duration timeout) {
        return new Option[]{
                // Required. The Request ID of each request must not repeat.
                // If it is not passed, the SDK will add it to each request by default.
                Option.withRequestID(UUID.randomUUID().toString()),
                // Optional. Specify the duration before a request timeout.
                Option.withTimeout(timeout),
                // Optional. Add a set of customer headers to the request, which will be overwritten by multiple calls.
                //Option.withHeaders(customerHeaders),
                // Optional. Add a set of customer queries to the request, which will be overwritten by multiple calls.
                //Option.withQueries(customerQueries),
                // Optional. Add a header to an existing custom header collection.
                //Option.withHeader("key", "value"),
                // Optional. Add a query to an existing custom query collection.
                //Option.withQuery("key", "value"),
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


<span id="d6a7f798"></span>
# WriteUserEvents


<Tabs>
<Tab zoneid="NhwMpGmvP5" title="Go">
<TabTitle>Go</TabTitle>

```Go
func writeUserEventsExample() {
    // The WriteUserEvents API can transfer up to 2,000 items in one request.
    request := buildWriteUserEventsRequest(2000)
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
        Stage: retail.StageIncremental,
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
<Tab zoneid="Q4loC9RGWv" title="Python">
<TabTitle>Python</TabTitle>

```Python
def write_user_events_example():
    # The WriteUserEvents API can transfer up to 2,000 items in one request.
    request = _build_write_user_event_request(15)
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
<Tab zoneid="HQ1mNN01Bu" title="Java">
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
                // Required. The Request ID of each request must not repeat.
                // If it is not passed, the SDK will add it to each request by default.
                Option.withRequestID(UUID.randomUUID().toString()),
                // Optional. Specify the duration before a request timeout.
                Option.withTimeout(timeout),
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


<span id="034e6b92"></span>
# Predict and AckServerImpressions


<Tabs>
<Tab zoneid="AVZRnw4jKs" title="Go">
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
    // The items, which are eventually shown to the user, should be sent back to ByteDance for de-duplication.
    alteredProducts := recommendWithPredictResult(response.GetValue())
    ackRequest := buildAckRequest(response.GetRequestId(), predictRequest, alteredProducts)
    ackOpts := defaultOptions(DefaultAckImpressionsTimeout)
    // async ack the actual impressions after this recommendation.
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
    rootProduct := mockPredictProduct()
    device := mockPredictDevice()
    context := &protocol.PredictRequest_Context{
        RootProduct:       rootProduct,
        Device:            device,
        CandidateProducts: []*protocol.Product{mockPredictProduct()},
    }
    return &protocol.PredictRequest{
        ModelId: modelID,
        UserId:  "1457789",
        Size:    20,
        Scene:   scene,
        Context: context,
        //Extra:     map[string]string{"extra_info": "extra"},
    }
}

func recommendWithPredictResult(
    predictResult *protocol.PredictResult) []*protocol.AckServerImpressionsRequest_AlteredProduct {
    // You can handle the recommendation results here, such as filter, insert other items, sort again, and so on.
    // The list of goods finally displayed to user and the filtered goods should be sent back to ByteDance for de-duplication.
    return conv2AlteredProducts(predictResult.GetResponseProducts())
}

func conv2AlteredProducts(
    products []*protocol.PredictResult_ResponseProduct) []*protocol.AckServerImpressionsRequest_AlteredProduct {
    if len(products) == 0 {
        return nil
    }
    alteredProducts := make([]*protocol.AckServerImpressionsRequest_AlteredProduct, len(products))
    for i, product := range products {
        alteredProducts[i] = &protocol.AckServerImpressionsRequest_AlteredProduct{
            AlteredReason: "kept",
            ProductId:     product.GetProductId(),
            Rank:          int32(i + 1),
        }
    }
    return alteredProducts
}

func buildAckRequest(predictRequestId string, predictRequest *protocol.PredictRequest,
    alteredProducts []*protocol.AckServerImpressionsRequest_AlteredProduct) *protocol.AckServerImpressionsRequest {

    return &protocol.AckServerImpressionsRequest{
        ModelId:          predictRequest.GetModelId(),
        PredictRequestId: predictRequestId,
        UserId:           predictRequest.GetUserId(),
        // If the recommendation result is from BytePlus, the traffic_source will be byteplus.
        // If it is the customer's own recommendation result, the traffic_source wull be self.
        TrafficSource:   "byteplus",
        Scene:           predictRequest.GetScene(),
        AlteredProducts: alteredProducts,
        //Extra:            map[string]string{"ip": "127.0.0.1"},
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
<Tab zoneid="qeln0PstUE" title="Python">
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
    # The items, which are eventually shown to the user, should be sent back to ByteDance for de-duplication.
    altered_products = do_something_with_predict_result(predict_response.value)
    ack_request = _build_ack_impressions_request(predict_response.request_id, predict_request, altered_products)
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

    ctx = request.context
    ctx.candidate_products.extend([mock_predict_product()])
    ctx.root_product.CopyFrom(mock_predict_product())
    ctx.device.CopyFrom(mock_device())

    #request.extra["extra_info"] = "extra"
    return request


def do_something_with_predict_result(predict_result):
    # You can handle the recommendation results here, such as filter, insert other items, sort again, and so on.
    # The list of goods finally displayed to user and the filtered goods should be sent back to ByteDance for de-duplication.
    return conv_to_altered_products(predict_result.response_products)


def conv_to_altered_products(product_results):
    if product_results is None or len(product_results) == 0:
        return
    size = len(product_results)
    altered_products = [Optional[AckServerImpressionsRequest.AlteredProduct]] * size
    for i in range(size):
        product_result = product_results[i]
        altered_product = AckServerImpressionsRequest.AlteredProduct()
        altered_product.altered_reason = "kept"
        altered_product.product_id = product_result.product_id
        altered_product.rank = product_result.rank
        altered_products[i] = altered_product
    return altered_products


def _build_ack_impressions_request(predict_request_id: str, predict_request: PredictRequest, altered_products: list):
    request = AckServerImpressionsRequest()
    request.model_id = predict_request.model_id
    request.predict_request_id = predict_request_id
    request.user_id = predict_request.user_id
    # If the recommendation result is from BytePlus, the traffic_source will be byteplus.
    # If it is the customer's own recommendation result, the traffic_source wull be self.
    request.traffic_source = "byteplus"
    scene: Message = request.scene
    scene.CopyFrom(predict_request.scene)
    request.altered_products.extend(altered_products)

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
<Tab zoneid="yzhX6v1D9R" title="Java">
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
        // The items, which are eventually shown to the user, should be sent back to ByteDance for de-duplication.
        List<AlteredProduct> alteredProducts = doSomethingWithPredictResult(response.getValue());
        AckServerImpressionsRequest ackRequest =
                buildAckRequest(response.getRequestId(), predictRequest, alteredProducts);
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
        Product rootProduct = MockHelper.mockPredictProduct();
        Device device = MockHelper.mockDevice();

        List<Product> candidateProducts = Arrays.asList(
                MockHelper.mockPredictProduct(),
                MockHelper.mockPredictProduct()
        );

        PredictRequest.Context context = PredictRequest.Context.newBuilder()
                .setRootProduct(rootProduct)
                .setDevice(device)
                .addAllCandidateProducts(candidateProducts)
                .build();

        return PredictRequest.newBuilder()
                .setModelId(MODEL_ID)
                .setUserId("1457789")
                .setSize(20)
                .setScene(scene)
                .setContext(context)
                //.putExtra("extra_inio", "extra")
                .build();
    }

    private static List<AlteredProduct> doSomethingWithPredictResult(PredictResult predictResult) {
        // You can handle the recommendation results here, such as filter, insert other items, sort again, and so on.
        // The list of goods finally displayed to user and the filtered goods should be sent back to ByteDance for de-duplication.
        return conv2AlteredProducts(predictResult.getResponseProductsList());
    }

    @NotNull
    private static List<AlteredProduct> conv2AlteredProducts(List<ResponseProduct> products) {
        if (Objects.isNull(products) || products.isEmpty()) {
            return Collections.emptyList();
        }
        List<AlteredProduct> alteredProducts = new ArrayList<>(products.size());
        for (int i = 0; i < products.size(); i++) {
            ResponseProduct responseProduct = products.get(i);
            AlteredProduct alteredProduct = AlteredProduct.newBuilder()
                    .setAlteredReason("kept")
                    .setProductId(responseProduct.getProductId())
                    .setRank(i + 1)
                    .build();

            alteredProducts.add(alteredProduct);
        }
        return alteredProducts;
    }

    private static AckServerImpressionsRequest buildAckRequest(
            String predictRequestId,
            PredictRequest predictRequest,
            List<AlteredProduct> alteredProducts) {

        return AckServerImpressionsRequest.newBuilder()
                .setModelId(predictRequest.getModelId())
                .setPredictRequestId(predictRequestId)
                .setUserId(predictRequest.getUserId())
                .setScene(predictRequest.getScene())
                // If the recommendation result is from BytePlus, the traffic_source will be byteplus.
                // If it is the customer's own recommendation result, the traffic_source wull be self.
                .setTrafficSource("byteplus")
                .addAllAlteredProducts(alteredProducts)
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
