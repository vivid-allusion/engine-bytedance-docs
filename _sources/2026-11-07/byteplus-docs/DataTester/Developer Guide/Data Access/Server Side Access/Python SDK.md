---
title: "Python SDK"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Python-SDK"
---

<span id="_1-安装sdk"></span>
# 1. Install the SDK

<span id="_1-1-下载sdk"></span>
## 1.1 Download the SDK

Current SDK version: v3.0.0

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ade252bfc79448ebfd245768392f549~tplv-goo7wpa0wc-image.image" name="datatester_python_sdk-3.0.0-py3-none-any.whl">datatester_python_sdk-3.0.0-py3-none-any.whl</Attachment>


&nbsp;

<span id="_1-2-pip"></span>
## 1.2 pip

Supported range: Linux + python ≥ 3.7, ≤ 3.14

```bash
pip install datatester_python_sdk-3.0.0-py3-none-any.whl
```


<span id="_2-代码示例"></span>
# 2. Code example

<span id="dc760cff"></span>
## 2.1 Initializing the Client

Privatization customers need to specify meta_host and track_host as domain names configured at deployment time. Also specify is_onpremise as True

```python
from client import client

#Initialize the ABTest offload client side, please pay attention to modify the token parameters
#meta_host and track_host please modify the domain name configured at deployment time
ab_client = client.AbClient(
    "token"
    meta_host="",
    track_host="",
    is_onpremise=True
)
"""
Parameter:
    token: The detailed method of acquisition can be seen in AbClient
    meta_host: domain name configured in Private deployment
    track_host: domain name configured in Private deployment
    is_onpremise: configuration should be True in private deployment environment
    user_info_handler: Default value, user information object, this handler needs to be implemented for joining groups but not leaving groups
    max_workers: Default value, number of event reporting threads, default is 4
"""
```


<span id="59c8ecf9"></span>
## 2.2 Request offloading and get results

```Python
from client import client

#Specific parameters can be viewed 2.1 Initialize Client
ab_client = client.AbClient("token")  

#Define the parameters carried in the request when shunting
attributes = {    
    "state": "Nanjing",
    "likes_donuts": True,
}

#Recommended interface
#Get the experimental configuration after shunting according to the variant key
variable = ab_client.activate(
        "{variant_key}", 
        "{decision_id}", 
        "{track_id}", 
        "{default_value}", 
        attributes
        )
"""
Parameter:
    variant_key: variant key    
    decision_id: Local diversion user identifier, not used for event reporting, please replace with the customer's real user identifier    
    track_id: Event reporting user ID, used for event reporting, please replace with the customer's real user ID
    default_value: When the diversion fails to hit, return this value. It can be used according to business needs and passed as None
    attributes: user property, only used for diversion, not reported with buried points, can refer to https://www.volcengine.com/docs/6287/65826
"""       
#Examples of various types of parameters
# number
#control group = 123 experimental group = 456
if variable == 123:
    pass
elif variable == 456:
    pass
else:
    pass 
#control group = 111.23 experimental group = 444.56
if variable == 111.23:
    pass
elif variable == 444.56:
    pass
else:
    pass 

# string
#control group = "aaa" experimental group = "bbb"
if variable == "aaa":
    pass
elif variable == "bbb":
    pass
else:
    pass 

# bool
#control group = true experimental group = false
if isinstance(variable, bool) and variable:
    pass
else:
    pass

# json
#control group = {"key": "value_a"} experimental group = {"key": "value_b"}
if not isinstance(variable, dict):
    return
if variable.get("key", None) == "value_a":
    pass
elif variable.get("key", None) == "value_b":
    pass
else:
    pass
```


<span id="_3-接口描述"></span>
# 3. Interface description

<span id="_3-1-abclient"></span>
## 3.1 Abclient initialization method

<span id="描述：初始化abtest分流类"></span>
#### Description: Initialize the ABTest triage class

```python
def __init__(self, token=None, meta_host=None, track_host=None, is_onpremise=False, 
            user_info_handler=None，max_workers=4):
    """
    Parameter:
        token: To indicate your Tester application. For security reasons, token=appKey is used here instead of appId.
        meta_host: Set the address for obtaining meta information. Private users should pay attention to modifying it
        track_host: Set the address for event reporting. Private users should pay attention to modifying it
        is_onpremise: Default value, whether the SDK is a private deployment version        
        user_info_handler: Default value, user information object, this handler needs to be implemented for joining groups but not leaving groups
        max_workers: Default value, number of event reporting threads, default is 4
    """
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Please initialize AbClient as soon as possible to avoid affecting your triage service and event tracking report service.</div>


2. <div data-tips="true" data-tips-type="tip">Each application has one and only one shunt class, AbClient. Please ensure that it is unique among all threads.</div>



Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="_3-2-user-info-handler"></span>
## 3.2 user_info_handler

<span id="描述：进组不出组用户分组信息存储"></span>
#### Description: In and out of groups User group information storage

How to use:


1. If the user_info_handler is not specified when initializing AbClient, the empty implementation is used by default, and the function of "entering the group but not the group" is not enabled.

2. Implement the following UserInfoHandler class to implement persistent storage by yourself; when initializing AbClient, pass in the UserInfoHandler object through user_info_handler parameters.


```python
class UserInfoHandler:
    def query(decision_id):
        """
        Parameter:
            decision_id: local traffic division user identifier
        Return value:
            user join group information, same as the input parameter abInfo of create_or_update
        """
        
    def create_or_update(decision_id, abInfo):
        """
        Parameter:
            decision_id: local traffic division user identifier
            abInfo: string type, user join group information
        Return value:
            type boolean, whether update successfully
        """
```


<span id="_3-3-activate"></span>
## 3.3 activate

<span id="描述：获取特定key的分流结果，并上报曝光事件"></span>
#### Description: Get triage results for specific keys and report exposure events

```python
def activate(self, variant_key, decision_id, track_id, default_value, attributes):
    """
    Parameter:
        variant_key: variant key
        decision_id: local traffic division user identifier
        track_id: event reporting user identifier
        default_value: variant default value
        attributes: user attributes
    
    Return value:rn value:
        This function returns the parameter values of the hit version, and returns the default values when not hit
    """
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Interfaces containing the words "with_impression" will automatically report exposure events.</div>


   <div data-tips="true" data-tips-type="tip">2, event reporting interface must fill in the track_id field, otherwise it will lead to reporting failure.   </div>
   


<span id="返回值示例："></span>
#### Example of return value:

```plain
Parameter type is string，return value is str "a".
Parameter type is number，return value is int  123(also could be float 444.56).
Parameter type is boolean，return value is boolean type value--True.
Parameter type is json，return value is dict {'key': 1}.
```


<span id="_3-4-get-experiment-variant-name"></span>
## 3.4 get_experiment_variant_name

<span id="描述：获取用户命中的特定实验的版本名称"></span>
#### Description: Get the version name of the specific experiment that the user hit

```python
def get_experiment_variant_name(self, experiment_id, decision_id, attributes):
    """
    Parameter:
        experiment_id: Specify the experimental ID for the diversion
        decision_id: local traffic division user identifier
        attributes: user attributes
    
    Return value:
        This function returns the version name of the specific experiment hit by the user,
        If the user is not in the experiment or the experiment has not started, return None.
    """
```


<span id="返回值示例："></span>
#### Example of return value:

The return value is string "Comparison Version"/"Experimental Version 1"

<span id="_3-5-get-experiment-configs"></span>
## 3.5 get_experiment_configs

<span id="描述：获取用户命中的特定实验的变体详情"></span>
#### Description: Get variant details of specific experiments hit by users

```python
def get_experiment_configs(self, experiment_id, decision_id, attributes):
    """
    Parameter:
        experiment_id: Specify the experimental ID for the diversion
        decision_id: local traffic division user identifier
        attributes: user attributes
    
    Return value:
        This function returns the variant details of a feature hit by the user, usually one variant can be hit,
        If the user is not in the experiment or the experiment has not started, return an empty dict {}.
    """
```


<span id="返回值示例："></span>
#### Example of return value:

```json
// dict
{'age': {'val': 12, 'vid': '160528'}, 'configure': {'val': {'settings': 1}, 'vid': '160528'}, 'fromCN': {'val': True, 'vid': '160528'}, 'name': {'val': 'asd', 'vid': '160528'}}
```


<span id="_3-6-get-all-experiment-configs"></span>
## 3.6 get_all_experiment_configs

<span id="描述：获取用户命中的所有实验的变体详情"></span>
#### Description: Get variant details of all experiments hit by the user

```python
def get_all_experiment_configs(self, decision_id, attributes):
    """ 
    Parameter:
        decision_id: local traffic division user identifier
        attributes: user attributes
    
    Returns:
        This function returns the variant details of a feature hit by the user, usually multiple variants can be hit,
        If the user is not in the experiment or the experiment has not started, return an empty dict {}.
    """
```


<span id="返回值示例："></span>
#### Example of return value:

Same as get_experiment_configs return structure

```json
{'go': {'val': 'v1', 'vid': '83580'}, 'age': {'val': 12, 'vid': '160528'}, 'configure': {'val': {'settings': 1}, 'vid': '160528'}, 'fromCN': {'val': True, 'vid': '160528'}, 'name': {'val': 'asd', 'vid': '160528'}}
```


<span id="_3-7-get-feature-configs"></span>
## 3.7 get_feature_configs

<span id="描述：获取用户命中的特定feature的变体详情"></span>
#### Description: Get variant details of specific features hit by users

```python
def get_feature_configs(self, feature_id, decision_id, attributes):
    """ 
    Parameter:
        feature_id: feature的ID
        decision_id: local traffic division user identifier
        attributes: user attributes
    
    Return value:
        This function returns the variant details of a feature hit by the user, usually only one variant can be hit,
        if the user is not in the feature or the feature is unavailable, return None.
    """
```


<span id="返回值示例："></span>
#### Example of return value:

```json
{'servergo': {'val': False, 'vid': '20100615'}}
```


<span id="_3-8-get-all-feature-configs"></span>
## 3.8 get_all_feature_configs

<span id="描述：获取用户命中的所有feature的变体详情"></span>
#### Description: Get variant details of all features hit by the user

```python
def get_all_feature_configs(self, decision_id, attributes):
    """ 
    Parameter:
        decision_id: local traffic division user identifier
        attributes: user attributes

    Return value:
        This function returns the variant details of a feature hit by the user, usually multiple variants can be hit,
        If the user is not in the feature or the feature is unavailable, return None.
    """
```


<span id="返回值示例："></span>
#### Example of return value:

Same as get_feature_configs return structure

```json
{'servergo': {'val': False, 'vid': '20100615'}, 'python_key': {'val': 'bbb', 'vid': '20108187'}}
```


<span id="_3-9-get-experiment-variant-name-with-impression"></span>
## 3.9 get_experiment_variant_name_with_impression

Same interface: "get_experiment_variant_name" (while reporting exposure events, need to pass in track_id)

<span id="_3-10-get-experiment-configs-with-impression"></span>
## 3.10 get_experiment_configs_with_impression

Same interface: "get_experiment_configs" (while reporting exposure events, need to pass in track_id)

<span id="_3-11-get-feature-configs-with-impression"></span>
## 3.11 get_feature_configs_with_impression

Same interface: "get_feature_configs" (while reporting exposure events, need to pass in track_id)
