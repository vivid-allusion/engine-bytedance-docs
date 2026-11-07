---
title: "Traffic Shunt Agent"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Traffic-Shunt-Agent"
---

<span id="_1-使用方式"></span>
# 1. How to use


1. The agent is a docker image and needs to be deployed to the business environment

2. Access through the http interface to get the shunt result.

3. Supports the main features of the server side SDK


<span id="_2-服务部署"></span>
# 2. Service deployment


1. Download image, current agent version: v1.0.3


**Privatization**

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c28db17555fb817cb4a42151fbdc1660.gz" name="datatester-docker-agent-onpremise_v1.0.3.tar.gz">datatester-docker-agent-onpremise_v1.0.3.tar.gz</Attachment>



2. Install Docker

3. startup service

4. load image


```bash
#Load mirror
docker  load -i datatester-docker-agent*.tar.gz
#Query the mirror ID of the load
docker  images
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cf0bf94a5cbb3a0dba4521fe1c691727.png) </span>


5. run


<span id="私有化"></span>
#### Privatization


* *Docker* run \-p {host port}: 6789 {image id} {appKey} {metaInterval}


All parameters are required, including appkey:

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">The host port is configured according to business needs</div>


2. <div data-tips="true" data-tips-type="tip">Replace the mirror id with the actual id, refer to c8323aee9721 in the example picture.</div>


3. <div data-tips="true" data-tips-type="tip">MetaInterval is the time interval for pulling metadata, in seconds, it is recommended to set it to 60 seconds</div>


4. <div data-tips="true" data-tips-type="tip">During private deployment, there will be product domain names and reported domain names, productHost will be replaced by product domain names, and eventHost will be replaced by reported domain names</div>



Example:


* docker run \-p 6789:6789 380b4fc3dcf0 7857596a9078f97857596a907 60 http://product.cc https://product.com

* docker run \-p 6789:6789 380b4fc3dcf0 7857596a9078f97857596a907 20 http://product.cc https://product.com


<span id="_3-接口描述"></span>
# 3. Interface description

<span id="_3-1-健康检查接口"></span>
## 3.1 Health check interface

**Interface:/ping**

**Method: GET**

**Description: Health Check**

**Request parameters: none**

**Return value: fixed value**

```json
{
    "message": "pong"
}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Except for the health check interface, all other interfaces are HTTP POST.</div>


<span id="_3-2-activate"></span>
## 3.2 activate

**Interface:/activated**

**Description:**  Get the shunt result of a specific key and report the exposure event

**Request parameters:** 

```json
{
    "variant_key": "variantKey", //specific key, i.e. the parameter name configured in the experiment
    "decision_id": "decisionID", //Local offload user ID, not for event reporting, please replace it with the customer's real user ID
    "track_id": "uuid", //Event reporting user ID, used for event reporting, please replace it with the customer's real user ID
    "attributes": {      //User properties, only for offloading, not with event tracking reports
        "name": "user_name",
        "age": 20,
        "is_android": true,
        "pay": 123.456
    }
}
```


**Return value:**  Return hit variant object

```json
//miss
{
    "data": {},
    "code": 200,
    "message": ""
}
// variant_key="string"
{
    "data": {
        "string": {
            "val": "bbb",
            "vid": "23357"
        }
    },
    "code": 200,
    "message": ""
}
// variant_key="number"
{
    "data": {
        "number": {
            "val": 456,
            "vid": "23357"
        }
    },
    "code": 200,
    "message": ""
}
// variant_key="boolean"
{
    "data": {
        "boolean": {
            "val": false,
            "vid": "23357"
        }
    },
    "code": 200,
    "message": ""
}
// variant_key="json"
{
    "data": {
        "json": {
            "val": {
                "count": 2,
                "ver": "b"
            },
            "vid": "23357"
        }
    },
    "code": 200,
    "message": ""
}
//Parameter error code is 203, message is error message
{
    "data": {},
    "code": 203,
    "message": "variant_key is empty"
}
//Other error code is 205, message is error message
{
    "data": {},
    "code": 205,
    "message": "xxxx"
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">This interface and all interfaces containing the word "WithImpression" will automatically report exposure events</div>


   <div data-tips="true" data-tips-type="tip">2, variant_key, decision_id, track_id must choose   </div>
   


<span id="_3-3-getexperimentconfigs"></span>
## 3.3 getExperimentConfigs

**Interface:/getExperimentConfigs**

**Description:**  Get variant details of a specific experiment hit by the user

**Request parameters:** 

```json
{
    "decision_id": "decisionID", //Local offload user ID, not for event reporting, please replace it with the customer's real user ID
    "track_id": "uuid", //Event reporting user ID, used for event reporting, please replace it with the customer's real user ID
    "attributes": {      //User properties, only for offloading, not with event tracking reports
        "name": "user_name",
        "age": 20,
        "is_android": true,
        "pay": 123.456
    },
    "experiment_id": "123456" //ID of a specific experiment
}
```


**Return value:**  Returns the object that hit the variant, indicating that the user hit the variant details of an experiment, usually only one variant.

```json
//miss experiment
{
    "data": {},
    "code": 200,
    "message": ""
}
//hit experiment
{
    "data": {
        "number": {
            "val": 456,
            "vid": "23357"
        },
        "boolean": {
            "val": false,
            "vid": "23357"
        },
        "string": {
            "val": "bbb",
            "vid": "23357"
        },
        "json": {
            "val": {
                "count": 2,
                "ver": "b"
            },
            "vid": "23357"
        }
    },
    "code": 200,
    "message": ""
}
//Parameter error code is 203, message is error message
{
    "data": {},
    "code": 203,
    "message": "experiment_id is empty"
}
//Other error code is 205, message is error message
{
    "data": {},
    "code": 205,
    "message": "failed to find experiment[333333]"
}
```


<span id="_3-4-getexperimentconfigswithimpression"></span>
## 3.4 getExperimentConfigsWithImpression

**Interface:/getExperimentConfigsWithImpression**

The request response is the same as the interface "getExperimentConfigs" and the exposure event is automatically reported

<span id="_3-5-getallexperimentconfigs"></span>
## 3.5 getAllExperimentConfigs

**Interface:/getAllExperimentConfigs**

**Description:**  Get variant details of all experiments hit by the user

**Request parameters:** 

```json
{
    "decision_id": "decisionID", //Local offload user ID, not for event reporting, please replace it with the customer's real user ID
    "attributes": {      //User properties, only for offloading, not with event tracking reports
        "name": "user_name",
        "age": 20,
        "is_android": true,
        "pay": 123.456
    }
}
```


**Return Value:**  Returns the hit variant details, usually multiple variants.

```json
//miss experiment
{
    "data": {},
    "code": 200,
    "message": ""
}
//hit
{
    "data": {
        "number": {
            "val": 456,
            "vid": "23357"
        },
        "boolean": {
            "val": false,
            "vid": "23357"
        },
        "string": {
            "val": "bbb",
            "vid": "23357"
        },
        "json": {
            "val": {
                "count": 2,
                "ver": "b"
            },
            "vid": "23357"
        },
        "config": {
            "val": "off",
            "vid": "23361"
        }
    },
    "code": 200,
    "message": ""
}
//Parameter error code is 203, message is error message
{
    "data": {},
    "code": 203,
    "message": "decision_id is empty"
}
//Other error code is 205, message is error message
{
    "data": {},
    "code": 205,
    "message": "xxxxx"
}
```


<span id="_3-6-getfeatureconfigs"></span>
## 3.6 getFeatureConfigs

**Interface:/getFeatureConfigs**

**Description:**  Get variant details of a specific feature hit by the user

**Request parameters:** 

```json
{
    "decision_id": "decisionID", //Local offload user ID, not for event reporting, please replace it with the customer's real user ID
    "track_id": "uuid", //Event reporting user ID, used for event reporting, please replace it with the customer's real user ID
    "attributes": {      //User properties, only for offloading, not with event tracking reports
        "name": "user_name",
        "age": 20,
        "is_android": true,
        "pay": 123.456
    },
    "feature_id": "123456" //ID of a specific feature
}
```


**Return value:**  Returns the object that hit the variant, indicating that the user hit the variant details of a feature, usually only one variant.

```json
//miss
{
    "data": {},
    "code": 200,
    "message": ""
}
//hit ff
{
    "data": {
        "feature_str": {
            "val": "false",
            "vid": "20000044"
        }
    },
    "code": 200,
    "message": ""
}
//hit ff
{
    "data": {
        "feature_key_number": {
            "val": 3,
            "vid": "20000058"
        }
    },
    "code": 200,
    "message": ""
}
//Parameter error code is 203, message is error message
{
    "data": {},
    "code": 203,
    "message": "feature_id is empty"
}
//Other error code is 205, message is error message
{
    "data": {},
    "code": 205,
    "message": "failed to find feature[333333]"
}
```


<span id="_3-7-getfeatureconfigswithimpression"></span>
## 3.7 getFeatureConfigsWithImpression

**Interface:/getFeatureConfigsWithImpression**

The request response is the same as the interface "getFeatureConfigs", and the exposure event will be automatically reported.

<span id="_3-8-getallfeatureconfigs"></span>
## 3.8 getAllFeatureConfigs

**Interface:/getAllFeatureConfigs**

**Description:**  Get variant details of all features hit by the user

**Request parameters:** 

```json
{
    "decision_id": "decisionID", //Local offload user ID, not for event reporting, please replace it with the customer's real user ID
    "attributes": {      //User properties, only for offloading, not with event tracking reports
        "name": "user_name",
        "age": 20,
        "is_android": true,
        "pay": 123.456
    }
}
```


**Return Value:**  Returns the hit variant details, usually multiple variants.

```json
//miss
{
    "data": {},
    "code": 200,
    "message": ""
}
//hit
{
    "data": {
        "feature_str": {
            "val": "false",
            "vid": "20000044"
        },
        "feature_key_number": {
            "val": 1,
            "vid": "20000056"
        }
    },
    "code": 200,
    "message": ""
}
//Parameter error code is 203, message is error message
{
    "data": {},
    "code": 203,
    "message": "decision_id is empty"
}
//Other error code is 205, message is error message
{
    "data": {},
    "code": 205,
    "message": "xxxxx"
}
```


<span id="_4-其他"></span>
# 4. Other

<span id="使用场景"></span>
## Usage scenario

The agent is a single node, and the performance is equivalent to a single server side SDK. It is recommended to use it only in the trial stage and in scenarios with relatively small request volume. In scenarios with large traffic access, the server side SDK is preferred.
