---
title: "Java SDK"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Java-SDK"
---

<span id="_1-安装sdk"></span>
# 1. Install the SDK

<span id="_1-1-下载sdk"></span>
## 1.1 Download the SDK

Current SDK version: v2.0.24

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b456afeb39704123b1d8fd6b4d200e5e~tplv-goo7wpa0wc-image.image" name="datatester-java-sdk-2.0.24.jar">datatester-java-sdk-2.0.24.jar</Attachment>


&nbsp;

<span id="_1-2-添加jar包"></span>
## 1.2 Add jar package


1. Java version requirements: Java 8 and higher

2. Import method: Add the jar file to the project Modules


Taking the mainstream IDE (IntelliJ IDEA) as an example, the jar package adds an example:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a41ac6b5214f8e9ba1f51933bcaffe5c.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_009d4740db7e76c34b3ed32087b424fe.png) </span>

<span id="_1-3-maven依赖导入"></span>
## 1.3 Maven dependency import

After successfully adding the jar package, you need to add the necessary dependencies through maven management.

Add dependencies: Add the following code to the project pom.xml

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">Be sure to add all necessary dependencies.</div>


2. <div data-tips="true" data-tips-type="warning">Please ensure that the dependency version you are using is greater than or equal to the official default version of Tester.</div>


3. <div data-tips="true" data-tips-type="warning">December 10, 2021 log4j exposed p0 vulnerability , lookup has code injection risk, please update the red dependency in the maven repository to the version shown in the document.</div>


4. <div data-tips="true" data-tips-type="warning">January 2022, Gson 2.8.6 version exposed security bugs, SDK has been upgraded to 2.8.9 version of support, please ensure that the project depends on not less than the official website security version 2.8.9.</div>



```xml
<dependencies>
    <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>2.8.9</version>
    </dependency>

    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.76</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-core</artifactId>
        <version>2.11.4</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-annotations</artifactId>
        <version>2.11.4</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.11.4</version>
    </dependency>

    <dependency>
        <groupId>com.google.guava</groupId>
        <artifactId>guava</artifactId>
        <version>27.0.1-jre</version>
    </dependency>
    
    <dependency>
        <groupId>com.github.zafarkhaja</groupId>
        <artifactId>java-semver</artifactId>
        <version>0.9.0</version>
    </dependency>

    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.21</version>
    </dependency>
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-slf4j-impl</artifactId>
        <version>2.15.0</version>
    </dependency>
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-core</artifactId>
        <version>2.15.0</version>
    </dependency>
    <dependency>
        <groupId>org.apache.logging.log4j</groupId>
        <artifactId>log4j-api</artifactId>
        <version>2.15.0</version>
    </dependency>
    <dependency>
        <groupId>com.lmax</groupId>
        <artifactId>disruptor</artifactId>
        <version>3.4.2</version>
    </dependency>

    <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpclient</artifactId>
        <version>4.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.apache.httpcomponents.client5</groupId>
        <artifactId>httpclient5</artifactId>
        <version>5.0.1</version>
    </dependency>

    <dependency>
        <groupId>com.google.protobuf</groupId>
        <artifactId>protobuf-java</artifactId>
        <version>2.5.0</version>
    </dependency>
    <dependency>
        <groupId>com.googlecode.protobuf-java-format</groupId>
        <artifactId>protobuf-java-format</artifactId>
        <version>1.4</version>
    </dependency>

</dependencies>
```


<span id="_2-代码示例"></span>
# 2. Code example

```java
import com.bytedance.tester.AbClient;
import com.bytedance.tester.model.User;
import com.bytedance.tester.model.common.Variable;
import com.bytedance.tester.abInfo.UserAbInfoHandler;
import com.bytedance.tester.abInfo.MemoryHandler;
import java.util.HashMap;
    
public class Example {
    public static void main(String[] args) {
        /** Initialize the ABTest shunt class. For the appKey acquisition method, please refer to the interface description.         AbClient initializes the environment information, where:         1. meta_host: get the address of meta information, privatization users need to modify;         2. track_host: Event reporting address, privatization users need to modify;         3. setOnpremise (true) : Whether to specify the above two domain names, if the designation is set to true         **/
         AbClient abClient = new AbClient.Builder("2b47a1f318d78fd71854815*********").setMetaHost("xxx").setTrackHost("xxxx").setOnpremise(true).build();
        //Enable debug mode to print user information that missed the experiment by default
        abClient.setDebugMode(true); 
        //Declare a user, decisionID for offloading, trackID for event reporting
        //decisionID: Local offload user ID, not for event reporting, please replace it with the customer's real user ID
        //trackID: Event reporting user ID, used for event reporting, please replace it with the customer's real user ID
        //add: add user properties, only for streaming, not with event tracking reports
        //build: generate User object
        User user = new User.UserBuilder().create("decisionID", "trackID")
                .setDeviceId(6981329701821561868L) Optional, not necessary
                .add("gender", "male")
                .add("phone", null)
                .add("is_vip", false)
                .add("version", "1.2.2")
                .add("age", 18)
                .build();
        //Enter the group but not the group memory to implement the interface. If the user does not configure the following code, the "Enter the group but not the group" function will not be enabled by default
        //Persistent storage of group information, please implement the UserAbInfoHandler interface by yourself (recommended)
        //MemoryHandler is memory storage, for testing only, do not use in production environment
        UserAbInfoHandler memoryHandler = MemoryHandler.getInstance(); 
        abClient.setUserAbInfoHandler(memoryHandler);
        //recommended interface
        String defaultValue = null; //Default version value, return this value when the shunt misses, note: the return value is the wrapped object, not the defaultValue itself, you still need to use the get method to get it
        Variable variable1 = abClient.activate("variantKey", user, defaultValue);
        if(null == variable1) {
            return;
        }
        Object value1 = variable1.getValue();
        if(null == value1) {
            return;
        }
        if(value1.equals("a")){
        }
        else if(value1.equals("b")){
        }
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In a privatized environment, if you want to use user grouping as an audience condition, you can initialize <code>new AbClient</code>by adding <code>.setCohortClient (new HttpCohortClient (app_id, metaHost))</code>configuration.</div>


<span id="_3-核心类介绍"></span>
# 3. Introduction to core classes

<span id="_3-1-user"></span>
## 3.1 User

**Description:**  User object, used to indicate the detailed properties of the offload user

**How to use:**  As an imported parameter when calling the shunt interface, the usage method is as follows

```java
//First create the user object through the Builder class, trackId is the default value, empty is allowed
User.UserBuilder userBuilder = new User.UserBuilder().create("decisionId", "trackId");
//Fill the device id to bind users who have not yet generated a uuid (optional)
userBuilder.setDeviceId(6981329701821561868L);
//populate the Builder with user attributes
userBuilder.add("age", 18);
userBuilder.add("name", "小明");
userBuilder.add("is_vip", true);
//Generate User Object
User user = userBuilder.build();
```


<span id="_3-2-variable"></span>
## 3.2 Variable

**Description: A** variant object that indicates the detailed properties of the shunt result

**How to use:**  The return object base class of the shunt interface is used as follows

```java
String vid = variable.vid; //variant ID
String type = variable.type; //The data type of the variant value, consistent with the Tester platform configuration

//General method, get Object object, the specific data type needs to be judged by the user
Object o = variable.getValue();
Exact data type
String vStr = variable.getString(); //Non-string types return null by default
int vInt = variable.getInteger(); //Non-int type returns 0 by default
double vDouble = variable.getDouble(); //Non-double type returns 0.0 by default
boolean vBoolean = variable.getBoolean(); //Non-boolean types return false by default
```


<span id="_3-3-userabinfohandler"></span>
## 3.3 UserAbInfoHandler

Description: Enter the group but not the group interface

Interface content:

```java
public interface UserAbInfoHandler {
    /**          * Obtain group entry information          *@param decisionId user offload ID          *@return Key: Experiment ID value: Variant ID of the incoming group          */
    HashMap<String, String> query(String decisionId);

    /**          * Update incoming group information          *@param decisionId user offload ID          *@param abInfo user entry information, < experimentID, versionID >          *@return Was the update successful?          */
    boolean createOrUpdate(String decisionId, HashMap<String, String> abInfo);
}
```


How to use:


1. If UserAbInfoHandler is not specified when initializing AbClient, an empty implementation is used by default, and the "in\-group\-out\-of\-group" function is not enabled.

2. setUserAbInfoHandler is executed when initializing AbClient, implementing MemoryHandler using the memory provided by default (see code example for usage).

3. Inherit the UserAbInfoHandler interface and implement persistent storage by yourself; pass in through setUserAbInfoHandler when initializing AbClient.


<span id="_3-4-性能参数（私有化专用）"></span>
## 3.4 Performance parameters (for privatization only)

AbClient.eventDispatcher.properties

```java
AbClient abClient = new AbClient.Builder("appKey").setMetaHost("MetaHost").setTrackHost("TrackHost").setOnpremise(true).build();
abClient.setThreadCount(4);
abClient.setQueueSize(102400);
```


<span id="_4-接口说明"></span>
# 4. Interface description

<span id="_4-1-abclient"></span>
## 4.1 AbClient

**Interface:** 

new AbClient.Builder(String appKey).setMetaHost(String metaHost).setTrackHost(String trackHost).setOnpremise(boolean isOnpremise).build();

**Description:**  Initialize the ABTest shunt class.

**Parameter:** 


* appKey: Indicates your Tester application. For security reasons, please use appKey instead of appID to identify your app.

   Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

   In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.   </div>
   

* metaHost: Fill in the address to obtain meta information. Privatization customers need to modify the domain name, usually rangers.

* trackHost: Fill in the address of the event report. Privatization customers need to modify the domain name, usually reported for SDK events. If you are not clear, please consult the front office or deploy your classmates.

* isOnpremise (default = false): Indicates whether your app is privatized, which depends on whether the event tracking report you use is correct


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Please initialize AbClient as soon as possible to avoid affecting your triage service and event tracking report service.</div>


2. <div data-tips="true" data-tips-type="tip">Each application has one and only one shunt class, AbClient. Please ensure that it is unique among all threads.</div>



<div data-tips="true" data-tips-type="tip">
---

</div>


<div data-tips="true" data-tips-type="tip">The Meta meta information service uses the domestic online address of the BytePlus A/B platform by default, please modify it carefully. Privatized customers need to change to the mount domain name of the AB service at the time of deployment.</div>


<div data-tips="true" data-tips-type="tip">
---

</div>


<div data-tips="true" data-tips-type="tip">The event tracking report service uses the domestic online address of the BytePlus A/B platform by default, please modify it carefully. The privatization client needs to modify the domain name to be mounted on the AppLog service at deployment time.</div>


<span id="_4-2-activate"></span>
## 4.2 activate

**Interface:**  Variable activate (String variantKey, User user, Object defaultValue)

**Description:**  Get the shunt result of a specific key and report the exposure event

**Parameter:** 

VariantKey: The key of the variant

User: user object

defaultValue: variant default value

**Return value:**  The function returns the hit variant object, and the default value object when missed

```java
public class Variable {
    String vid; //variant id
    Object val; //Variant value
    String type; The data type of the variant value
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">This interface and all interfaces containing the word "WithImpression" will automatically report exposure events. Users can specify trackHost when AbClient is initialized to adjust the event reporting address.</div>


2. <div data-tips="true" data-tips-type="tip">For the event reporting interface, please be sure to fill in the trackID field in User, otherwise the reporting will be invalid.</div>



<span id="_4-3-getabinfo"></span>
## 4.3 getABInfo

**Interface:**  HashMap < String, Variable \> getABInfo (User user)

**Description:**  Get triage results for experiments and features

**Parameter:** 

User: user object

**Return value:**  This function returns the Map object of the hit variant in the following format

```json
{
  "key1": {
    "vid": "123",
    "value": "v1",
    "type": "string"
  },
  "key2": {
    "vid": "456",
    "value": false,
    "type": "boolean" 
  },
  "key3": {
    "vid": "789",
    "value": 123.45,
    "type": "double" 
  }   
}
```


<span id="_4-4-getexperimentvariantname"></span>
## 4.4 getExperimentVariantName

**Interface:**  String getExperimentVariantName (String experimentId, User user)

**Description:**  Get the name of the experimental version hit by the user

**Parameter:** 

experimentId: Specify the experiment ID for the shunt

User: user object

**Return value:**  This function returns the name of the experimental version hit by the user

<span id="_4-5-getexperimentconfigs"></span>
## 4.5 getExperimentConfigs

**Interface:**  HashMap < String, Variable \> getExperimentConfigs (String experimentId, User user)

**Description:**  Get variant details of a specific experiment hit by the user

**Parameter:** 

experimentId: Specify the experiment ID for the shunt

User: user object

**Return value:**  This function returns the Map object that hit the variant, indicating that the user hit the variant details of an experiment, usually only one variant.

<span id="_4-6-getallexperimentconfigs"></span>
## 4.6 getAllExperimentConfigs

**Interface:**  HashMap < String, Variable \> getAllExperimentConfigs (User user)

**Description:**  Get variant details of all experiments hit by the user

**Parameter:** 

User: user object

**Return Value:**  This function returns the Map object that hit the variant, indicating that the user hit the variant details for all experiments, usually multiple variants.

<span id="_4-7-getfeatureconfigs"></span>
## 4.7 getFeatureConfigs

**Interface:**  HashMap < String, Variable \> getFeatureConfigs (String pecuureId, User user)

**Description:**  Get variant details of a specific feature hit by the user

**Parameter:** 

featureId：feature ID

User: user object

**Return value:**  This function returns the Map object that hit the variant, indicating that the user hit the variant details of a feature, usually only one variant.

<span id="_4-8-getallfeatureconfigs"></span>
## 4.8 getAllFeatureConfigs

**Interface:**  HashMap < String, Variable \> getAllFeatureConfigs (User user)

**Description:**  Get variant details of all features hit by the user

**Parameter:** 

User: user object

**Return Value:**  This function returns a Map object that hits the variant, indicating that the user hit the variant details for all features, usually multiple variants.

<span id="_4-9-getexperimentvariantnamewithimpression"></span>
## 4.9 getExperimentVariantNameWithImpression

Same interface "getExperimentVariantName" (report exposure events)

<span id="_4-10-getexperimentconfigswithimpression"></span>
## 4.10 getExperimentConfigsWithImpression

Same interface "getExperimentConfigs" (report exposure events)

<span id="_4-11-getfeatureconfigswithimpression"></span>
## 4.11 getFeatureConfigsWithImpression

Same interface "getFeatureConfigs" (report exposure event)

<span id="_4-12-setinterval"></span>
## 4.12 setInterval

**Interface:**  void setInterval (int n)

**Description:**  Set the interval for meta information updates

**Parameter:** 

N: Meta information automatic update interval (unit: seconds)

<span id="_4-13-setthreadcount"></span>
## 4.13 setThreadCount

**Interface:**  void setThreadCount (int n)

**Description:**  Set the maximum number of threads for the event tracking report service

**Parameter:** 

N: Maximum number of threads (default is 4)

<span id="_4-14-getsuccessevents"></span>
## 4.14 getSuccessEvents

**Interface:**  int getSuccessEvents ()

**Description:**  Get the number of successfully reported events, use to monitor the event report callback results

**Return value:**  Number of successful events reported

**Note: The** privatized version does not support callbacks

<span id="_4-15-getfailevents"></span>
## 4.15 getFailEvents

**Interface:**  int getFailEvents ()

**Description:**  Get the number of failed events to report, used to monitor the event report callback results

**Return value:**  number of failed events reported

<span id="_4-16-getqueueevents"></span>
## 4.16 getQueueEvents

**Interface:**  int getQueueEvents ()

**Description:**  Gets the number of events remaining in the thread pool to monitor the number of events that have not been reported

**Return value:**  number of unreported events

<span id="_4-17-logger"></span>
## 4.17 Logger

ABTest server level SDK uses file logging. If you want to modify the log configuration, edit the file log4j2.xml, which has the default log address./logs.

<span id="_5-常见问题处理"></span>
# 5. Common problem handling

<span id="如何使用redis实现进组不出组逻辑？"></span>
## **How to use Redis to implement group\-in\-group\-not\-group logic?** 

Please refer to the integration example, redis implementation

```java
/**  Implement the UserAbInfoHandler interface and implement the methods declared in the interface  * Enter the group but not the group, Redis realizes it.  */
public class NotOutGroupRedisImplement implements UserAbInfoHandler {
    /**          * Store offload results          *@param userId User ID          *@param hashMap shunt result parameters and values, key = shunt parameters, value = corresponding version identifier          *@return
     */
    @Override
    public boolean createOrUpdate(String userId, HashMap<String, String> hashMap) {
        long res = 0 ;
        for (Map.Entry<String, String> entry : hashMap.entrySet()) {
             res = JedisUtils.getJedis().hset(userId, entry.getKey(), entry.getValue());
        }
        return res > 0 ;
    }
    /**          * Query the group corresponding to the user          *@param userId          *@return The shunt result corresponding to the user key = shunt parameter, value = the identification of the corresponding version          */
    @Override
    public HashMap<String, String> query(String userId) {
        Map<String, String> resMap = JedisUtils.getJedis().hgetAll(userId);
        return (HashMap<String, String>) resMap;
    }
}
```


Configure the logic of inbound and inbound groups in AB split code

```java
AbClient abClient = new AbClient.Builder(appKey).build();
NotOutGroupRedisImplement notOutGroupHandler = new NotOutGroupRedisImplement();
abClient.setUserAbInfoHandler(notOutGroupHandler);
Variable variable1 = abClient.activate("variantKey", user, defaultValue);
```


<span id="如果获取不到uuid，或者想做匿名用户的服务端实验，如何设置？"></span>
## If I can't get the uuid, or want to do server level experiments with anonymous users, how do I set it up?

The decisionid in the user class needs to use the user's unique identifier, such as client side device id, ssid, trackid. If it is a real name, set the corresponding real name user id, if it is anonymous, it is an empty string, and the device id needs to be set through the setDeviceId or setWebId method.

```json
User user = new User.UserBuilder().create("decisionID", "") //trackId has a value to set the corresponding value, but no value to set the empty string.
        .setDeviceId(6981329701821561868L) Private deployment uses this method
        .setWebId(7018215618686981329L) //Web and Mini Programs use this method
        .build();
```
