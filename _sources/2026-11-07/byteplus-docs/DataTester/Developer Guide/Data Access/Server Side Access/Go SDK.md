---
title: "Go SDK"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Go-SDK"
---

<span id="_1-安装sdk"></span>
# 1. Install the SDK

```go
go get github.com/volcengine/datatester-go-sdk@v1.0.13
```



1. Current SDK version: v1.0.13

2. Go version requirements: go1.14 and above


<span id="_2-代码示例"></span>
# 2. Code example

```go
package main
import (
        "github.com/volcengine/datatester-go-sdk/client"
        "github.com/volcengine/datatester-go-sdk/config"
)
func main() {
        //For the token acquisition method, please refer to the interface description -AbClient.
        abClient := client.NewClient("token")
        config.WithMetaHost(""), //private deployment customers are generally product domain names, please replace according to the actual domain names
        config.WithTrackHost(""), //The private deployment customer reports the applied domain name for event tracking data, please replace it according to the actual domain name.

        /*           client.NewClient("appKey"),           Config.WithWorkerNumOnce (20),//The number of coroutines reported by the event, generally does not need to be set           config. WithFetchInterval (60 * time. Second),//meta update interval, the default is 60s, generally do not need to set           Config. WithAnonymousConfig (true, true),//anonymously report the configuration, the first parameter is on and off           Config. WithLogger (log. NewLogrusAdapt (logrus.New ()))) // custom logging interface, provides default implementation        */

        //attributes: user attributes, only used for streaming, not with event tracking report, please refer to https://www.volcengine.com/docs/6287/65826
        attributes := map[string]interface{}{
        }
        //decisionId (ssid): The local shunt user ID, not used for event reporting, please replace it with the real user ID of the customer
        //trackId (uuid): The user ID for event reporting, please replace it with the real user ID of the customer.
        value, err := abClient.Activate("${experiment_key}", "decisionId", "trackId", true, attributes)
        //In the case of missed experiments and ff, return a fixed err and not null, and return the default value passed in, which can be used on demand
        // if err != nil {
        //
        //}
}
```


<span id="_3-接口描述"></span>
# 3. Interface description

<span id="_3-1-newclient"></span>
## 3.1 NewClient

**Interface:** 

NewClient(token string, configs ...config.Func) \*AbClient

**Description:**  Initialize ABTest offload

**Parameter:** 


* Token: Indicates your Tester application. For security reasons, the token = appKey is used here, not appId.

   Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

   In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Initialize AbClient as early as possible to avoid affecting your triage and event tracking reporting services.   </div>
   

* config. WithMetaHost: The address for obtaining meta information; privatization needs to be set to the product domain name

* config. WithTrackHost: The address for event reporting; privatization needs to be set to the reporting domain name

* config. WithFetchInterval (60 \* time. Second): meta update interval, the default is 60s, generally do not need to set

* Config.WithWorkerNumOnce (20): The number of coroutines reported by the event, generally does not need to be set

* Config. WithAnonymousConfig (true, true): Anonymous reporting configuration, the first parameter is on and off; no setting is required in scenarios where anonymous reporting is not used

* Config. WithLogger (log. NewLogrusAdapt (logrus.New ())): Custom logging interface, provides default implementation


<span id="_3-2-newclientwithuserabinfo"></span>
## 3.2 NewClientWithUserAbInfo

**Interface:** 

NewClientWithUserAbInfo(token string, userAbInfoHandler handler.UserAbInfoHandler, configs ...config.Func) \*AbClient

**Description:**  Initialize the ABTest triage class, pass a custom userAbInfoHandler, userAbInfoHandler See the end of the document for details

<span id="_3-3-activate"></span>
## 3.3 Activate

**Interface:**  func (t \* AbClient) Activate (variantKey, decisionId, trackId string, defaultValue interface {}, attributes map [string] interface {}) (interface {}, error)

**Description:**  Get the shunt result of a specific key and report the exposure event

**Parameter:** 

VariantKey: The key of the variant

decisionId: local offload user ID

TrackId: Event reporting user ID

defaultValue: variant default value

Attributes: user attributes

**Return value:**  The function returns the hit variant object, and the default value object when missed

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">This interface and all interfaces containing the word "WithImpression" will automatically report exposure events. Users can specify the domain when AbClient is initialized and adjust the event reporting address.</div>


2. <div data-tips="true" data-tips-type="tip">Please be sure to fill in the trackId field, otherwise the report will be invalid</div>



<span id="_3-4-getexperimentvariantname"></span>
## 3.4 GetExperimentVariantName

**Interface:**  func (t \* AbClient) GetExperimentVariantName (experimentId, decisionId string, attributes map [string] interface {}) (string, error)

**Description:**  Gets the version name of a specific experiment hit by the user

**Parameter:** 

experimentId: The experimental Id for specifying the shunt

decisionId: local offload user ID

Attributes: user attributes

**Return value:**  This function returns the version name of the particular experiment that the user hit

<span id="_3-5-getexperimentconfigs"></span>
## 3.5 GetExperimentConfigs

**Interface:**  func (t \* AbClient) GetExperimentConfigs (experimentId, decisionId string, attributes map [string] interface {}) (map [string] map [string] interface {}, error)

**Description:**  Get variant details of a specific experiment hit by the user

**Parameter:** 

experimentId: The experimental Id for specifying the shunt

decisionId: local offload user ID

Attributes: user attributes

**Return value:**  This function returns the details of the variant of an experiment that the user hit, usually only one variant can be hit

**Example return value** :

```json
{
    "1324": {
       "val": "3",
       "vid": "27028"
    },
    "father_code": {
       "val": "father_code_2",
       "vid": "27028"
    },
    "grey_rollout": {
        "val": false,
        "vid": "27028"
    },
    "os_name": {
         "val": "android_f",
         "vid": "27028"
     }
 }
```


<span id="_3-6-getallexperimentconfigs"></span>
## 3.6 GetAllExperimentConfigs

**Interface:**  func (t \* AbClient) GetAllExperimentConfigs (decisionId string, attributes map [string] interface {}) (map [string] map [string] interface {}, error)

**Description:**  Get variant details of all experiments hit by the user

**Parameter:** 

decisionId: local offload user ID

Attributes: user attributes

**Return value:**  This function returns the variant details of all experiments hit by the user, usually multiple variants hit

**Example of return value:** 

Same as GetExperimentConfigs return structure

<span id="_3-7-getfeatureconfigs"></span>
## 3.7 GetFeatureConfigs

**Interface:**  func (t \* AbClient) GetFeatureConfigs (characterureId, decisionId string, attributes map [string] interface {}) (map [string] map [string] interface {}, error)

**Description:**  Get variant details of a specific feature hit by the user

**Parameter:** 

featureId：feature Id

decisionId: local offload user ID

Attributes: user attributes

**Return value:**  This function returns the details of the variant of a feature that the user hit, usually only one variant can be hit

**Example of return value:** 

```json
{
   "feature_key":{
        "val" : "prod",
        "vid" : "20006421"
    }
}
```


<span id="_3-8-getallfeatureconfigs"></span>
## 3.8 GetAllFeatureConfigs

**Interface:**  func (t \* AbClient) GetAllFeatureConfigs (decisionId string, attributes map [string] interface {}) (map [string] map [string] interface {}, error)

**Description:**  Get variant details of all features hit by the user

**Parameter:** 

decisionId: local offload user ID

Attributes: user attributes

**Return value:**  This function returns the variant details of all features hit by the user, usually multiple variants

**Example of return value:** 

Same structure as GetFeatureConfigs

<span id="_3-9-getexperimentvariantnamewithimpression"></span>
## 3.9 GetExperimentVariantNameWithImpression

Same interface "GetExperimentVariantName" (report exposure events)

<span id="_3-10-getallexperimentconfigswithimpression"></span>
## 3.10 GetAllExperimentConfigsWithImpression

Same interface "GetAllExperimentConfigs" (report exposure events)

<span id="_3-11-getexperimentconfigswithimpression"></span>
## 3.11 GetExperimentConfigsWithImpression

Same interface "GetExperimentConfigs" (report exposure events)

<span id="_3-12-getfeatureconfigswithimpression"></span>
## 3.12 GetFeatureConfigsWithImpression

Same interface "GetFeatureConfigs" (report exposure event)

<span id="_4-其他"></span>
# 4. Other

<span id="_4-1-userabinfohandler"></span>
## 4.1 UserAbInfoHandler

User information processing interface, used in scenarios of freezing experiments and not entering groups

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Freezing experiments and entering groups without groups requires persisting the user's incoming group information, and the default implementation provided by the SDK does not perform data persistence;</div>


<div data-tips="true" data-tips-type="tip">If there is a business need, implement the UserAbInfoHandler interface, combine Redis or other external storage to persist the user group information, and pass it in when initializing AbClient.</div>


<div data-tips="true" data-tips-type="tip">How to use:</div>



1. <div data-tips="true" data-tips-type="tip">When initializing AbClient with NewClient, the empty implementation is used by default, and the "enter group but not group" function is not enabled.</div>


2. <div data-tips="true" data-tips-type="tip">Inherit the UserAbInfoHandler interface and implement persistent storage by yourself; use NewClientWithUserAbInfo to initialize AbClient and pass in the self\-implemented UserAbInfoHandler class to enable the "group not group" function.</div>



Example of using Redis cache (for reference only)

```go
client.NewClientWithUserAbInfo("token", NewRedisUserAbInfoHandler())

type RedisAbInfoHandler struct{}

func (u *RedisAbInfoHandler) Query(decisionID string) string {
    // need to implement it yourself
    return redis.get(decisionID);
}

func (u *RedisAbInfoHandler) CreateOrUpdate(decisionID, experiment2Variant string) bool {
    // need to implement it yourself
    return redis.set(decisionID, experiment2Variant);
}

func (u *RedisAbInfoHandler) NeedPersistData() bool {
    // return true if customize this interface
    return true
}

func NewRedisUserAbInfoHandler() *RedisAbInfoHandler {
        return &RedisAbInfoHandler{}
}
```


<span id="_4-2-匿名上报"></span>
## 4.2 Anonymous reporting

Users who cannot get uuid can report events by filling device_id or web_id


1. When setting the anonymous reporting configuration for NewClient, the first parameter (true/on, false/off) is anonymous reporting, and the second parameter (false/privatization) is.


```go
client.NewClient("appKey", config.WithAnonymousConfig(true, true))
```



2. Add device_id, web_id, bddid to user attributes attributes, trackId fixed pass empty string ""


```php
trackId = "";
attributes["device_id"] = 1234; int64
attributes["web_id"] = 5678; int64
attributes["bddid"] = "91011"; string
```



3. Request Activate or other'WithImpression 'interfaces to report anonymously.
