---
title: "BytePlus Recommend API SDK authentication"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-api_authentication"
---

To prove the legitimacy of your identity and to avoid any malicious interception of a request during transfer, you must first calculate a signature and send the signed request to the server. The server calculates the request signature and compares it to the one you provided. If the signatures do not match, the request is rejected.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on API authentication through SDKs, reach out to the BytePlus Recommend team.</div>


<span id="fff64bf9"></span>
# Obtaining an AccessKey (AK) and a SecretKey (SK)

You can generate your tokens through the BytePlus Recommend console. The generated SecretAccessKey is your Token for using a BytePlus Recommend API or SDK. You can view your SecretAccessKey later by toggling the **Show** button behind each AccessKey.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Users need to have a BytePlus account before proceeding. For users that don't have a BytePlus account, refer to <a href="https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account">Signing up for a BytePlus account</a>.</div>


**To generate a token:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click your username \> **IAM**.

   The Identity management screen appears.

3. Click **Key Management**.

4. In the Token Management section, click **Create new access key**.

   The security risk alert pop\-up window appears.

5. Click **Continue**.

   An AccessKey is created, and the notification pop\-up window appears.

6. (Optional) Click **Download key certificate** to locally save the certificate of the generated AccessKey.


For more information, refer to [Managing keys](https://docs.byteplus.com/byteplus-platform/docs/managing-keys).

<span id="9e904017"></span>
# SDK authentication code samples—AK/SK

SDK authentication code samples are pre\-written code snippets that developers can use as a reference to implement authentication in their applications using the Byteplus Recommend SDK. These code samples typically include instructions on how to integrate the SDK into the developer's code, how to set up authentication credentials, and how to make authenticated requests to the Byteplus Recommend API.

<span id="4ae9e0b5"></span>
## SDK authentication—Retail industry

These are the code samples for SaaS standard clients in the Retail industry:


<Tabs>
<Tab zoneid="FZYL3hg8BR" title="Go">
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
<Tab zoneid="F4J5AjnM1q" title="Python">
<TabTitle>Python</TabTitle>

```Python
try: 
    client: Client = ClientBuilder() \ 
        .account_id("***********") \ 
        .region(Region.SG) \ 
        .project_id(PROJECT_ID) \ 
        .auth_ak("***********") \ 
        .auth_sk("***********") \ 
        .build() 
except BizException as clientE: 
    log.error("fail to create byteplus rec client, msg:%s", clientE)
```



</Tab>
<Tab zoneid="HHXZVhEaLP" title="Java">
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


<span id="9b8e5cbd"></span>
## SDK authentication—Content industry

These are the code samples for SaaS standard clients in the Content industry:


<Tabs>
<Tab zoneid="yJ2f3cQaSt" title="Go">
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
<Tab zoneid="B8iufD4UGX" title="Python">
<TabTitle>Python</TabTitle>

```Python
try: 
    client: Client = ClientBuilder() \ 
        .account_id("***********") \ 
        .region(Region.SG) \ 
        .project_id(PROJECT_ID) \ 
        .auth_ak("***********") \ 
        .auth_sk("***********") \ 
        .build() 
except BizException as clientE: 
    log.error("fail to create byteplus rec client, msg:%s", clientE)
```



</Tab>
<Tab zoneid="sTt1yo3DXl" title="Java">
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


<span id="dc404071"></span>
# SDK authentication code samples—Token

Token authentication is an alternative method of authentication used in Byteplus Recommend Premium for accessing its API. It involves generating a token, which is a unique string of characters that is used to authenticate API requests. SDK authentication code samples provide pre\-written code snippets that developers can use as a reference to implement token authentication in their applications using the Byteplus Recommend SDK.

These code samples typically include instructions on how to generate a token and create a client instance using the SDK. The token authentication method is often used by Recommend Premium customers who require a higher level of security and flexibility in their authentication process.

<span id="7b96a423"></span>
## SDK authentication—Retail industry

These are the code samples for SaaS Premium clients in the Retail industry:


<Tabs>
<Tab zoneid="kgWddkqt7M" title="Go">
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
<Tab zoneid="XY4tAD4sPz" title="Python">
<TabTitle>Python</TabTitle>

```Python
try: 
    client: Client = ClientBuilder() \ 
        .account_id("***********") \  #Required. The BytePlus account ID. 
        .region(Region.SG) \          #Required. The region of the server used to provide service. 
        .project_id(PROJECT_ID) \ 
        .air_auth_token("***********")\ # Required. The token of this project. 
        .build() 
except BizException as clientE: 
    log.error("fail to create byteplus rec client, msg:%s", clientE)
```



</Tab>
<Tab zoneid="MuM8VIKxRQ" title="Java">
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


<span id="002d27aa"></span>
## SDK authentication—Content industry

These are the code samples for SaaS Premium clients in the Content industry:


<Tabs>
<Tab zoneid="UvHsx9Ac3b" title="Go">
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
<Tab zoneid="IaUYjyrobO" title="Python">
<TabTitle>Python</TabTitle>

```Python
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
<Tab zoneid="KySxHCQ4dP" title="Java">
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
