---
title: "Programming Experiment - Client Side Local Allocation"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Programming-Experiment-Client-Side-Local-Allocation"
---

The client side local shunt experiment is also a kind of client side experiment. Currently, it is only supported by programming experiments. It is mainly suitable for new user open\-screen experiment scenarios such as applications. It is usually too late to generate the device id (did) and is usually in a non\-login state. At this time, in the programming experiment, select the experiment type as "client side\-local shunt" to build an empty experiment. By implementing shunt inside the client side and calling the client side SDK, the exposure event reporting and subsequent experiment report calculation can be realized. This article introduces the use of client\-side local shunting experiments.

<span id="35dff3a6"></span>
# Prerequisite: Data access

Before starting to create an experiment, you need to complete the tracking event access required for the experiment according to the experimental design. You can access the data through the client side SDK according to the type of experiment. The access operation of the local shunt experiment is similar to the access operation of the general client side SDK. There are a few changes when initializing. The differences between the local shunt experiments are detailed below. Detailed activity details of other SDK access can be found in: [Data Access Overview](https://docs.byteplus.com/docs/DataTester/Data-Access-Overview).

<span id="b85a29c4"></span>
## Android

<span id="f2465951"></span>
### Dependent access


* AppLog access

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Since the local shunting experiment needs to rely on the AppLog main SDK, you can refer to it <a href="https://docs.byteplus.com/docs/DataTester/Android-SDK-Integration">Android SDK Integration</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The local offload plugin needs to cooperate with 6.16.1 and above AppLog version, please make sure that the AppLog version is filled in correctly.   </div>
   

   ```Java
   Dependency warehouse completion:
   //Volcanic components required
   maven{
       url 'https://artifact.bytedance.com/repository/Volcengine/'
   }
   
   AppLog dependency
   //Add 6.16.1 and later version dependencies
   implementation 'com.bytedance.applog:RangersAppLog-Lite-cn:6.16.7'
   ```
   

* Local shunting SDK access:

   ```Java
   //add dependencies
   implementation 'com.bytedance.applog:RangersAppLog-Local-AbTest:1.0.1'
   ```
   


<span id="353ec8f3"></span>
### SDK initialization


* AppLog initialization.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Since local shunting depends on AppLog, initialize AppLog first.</strong>   </div>
   

   ```Java
   AppLog initialization
   InitConfig config = new InitConfig(appId, "test");
   //AB switch must be turned on
   config.setAbEnable(true);
   //SDK log, which will control AppLog + local offload SDK internal log printing
   config.setLogEnable(true);
   //Add data callback with vid changes + server side ab configuration
   AppLog.addDataObserver(this);
   //initialize
   AppLog.init(this, config);
   ```
   

* AB local offload plug\-in initialization.

   ```Java
   //Create an AbClientExperiment instance
   AbClientExperiment abClientExperiment = AbClientExperiment.newInstance();
   //Bind the AppLogInstance instance
   //The global default instance is bound here. If you use multiple instances, please bind the correct instance.
   //Before bindAppLog, please ensure that AppLog has been initialized normally
   abClientExperiment.bindAppLog(this, AppLog.getInstance());
   
   //AppLog multi-instance binding demonstration
   IAppLogInstance appLogInstance = AppLog.newInstance();
   appLogInstance.init(this, new InitConfig("appId", "channel"));
   abClientExperiment.bindAppLog(this, appLogInstance);
   
   //If the corresponding AbClientExperiment cannot be found, it also supports searching through the AppLog instance.
   AbClientExperiment abClientExperiment = AbClientExperiment.findAbClientExperiment(appLogInstance);
   ```
   


<span id="d277ef16"></span>
## IOS

<span id="adfbfac5"></span>
### Dependency access

CocoaPod introduces `ClientABTest`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">File\-mode integration requires the introduction of corresponding library files.</div>


```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        'ClientABTest',
    ]
```


header file reference

```objectivec
//relevant function settings are introduced into the header file
//modular integration @import RangersAppLog;
#import <RangersAppLog/BDAutoTrackClientABTest.h>
```


<span id="85313c0c"></span>
# Create a local offload experiment

Click " **+ Create Experiment**" on the experiment list page, select Programming Experiment, enter the experiment creation process, and refer to the following steps to configure the details of the experiment.

<span id="22cd8f84"></span>
## Step1 Enter basic information

**Experimental basic information** related parameters are mainly used to identify experiments, clear experimental types, etc. The configuration details are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec4317048039450990f6f1c361533c8a~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Type of experiment** |Select **client side \- local offload** experiment. |
|**Experiment duration** |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Since the local triage experiment is controlled by the client side technicians, the experiment time here is only for recording and does not take effect.</div><br><br><br>Refers to the duration of the experiment, generally in order to avoid differences in user behavior in different time periods (weekdays and weekends), it is recommended to observe at least 2 complete test schedules.<br><br>For example, when considering the impact of weekdays and weekends, the test schedule takes at least one week, and the recommended duration of the experiment is 14 days. |


<span id="cecfe542"></span>
## Step2 Sets the effective policy

The local shunting experiment does not require traffic settings, and the client side controls the effective policy independently. You can directly click **Next**.

<span id="37b6d01d"></span>
## Step3 Configure experimental version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The local shunt experiment configuration retains the configuration of the experimental version, which is only used to obtain the VID information of the experimental version after the experiment is created. Since the configuration parameters only depend on the control of the client side technicians, the configuration information here is for information reference only.</div>


<span id="b664c943"></span>
## Step4 Experimental metrics

Configuration details are consistent with normal programming experiments, see [Programming Experiment](https://docs.byteplus.com/docs/DataTester/Programming-Experiment).

<span id="1bdc5938"></span>
# Acquire the experimental VID

After the experiment is created, get the VID information of each experimental version on the experimental details page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e5f43a53fbc4b93a5327b32d78fa4a2~tplv-goo7wpa0wc-image.image) </span>

<span id="b5ab37bc"></span>
# Create experiments on the local client side \- Android

<span id="42cc5fde"></span>
## Create an experiment

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, manual code is supported to create local experiments, which requires specifying the experiment key, layer, experiment grouping information, and so on.</div>


<div data-tips="true" data-tips-type="tip">Currently, SettingKey is supported to create experiments where the default value is not null, and ExperimentKey is supported to create experiments where the default value is null.</div>


```Java
//Experiment of setting the default value not to null
ExperimentKey<Integer> ALIVE_IS_MONITOR_ENABLE = new SettingKey<>("alive_is_monitor_enable", 5555)
        //Set up the experimental layer
        .layer("default_layer")
        //Experimental grouping, the specified traffic is 20%, the vid is 111, and the experimental result is 1.
        .clientGroup(0.2, "111", 1)
         //Experimental grouping, the specified traffic is 20%, the vid is 1111, and the experimental result is 11.
        .clientGroup(0.2, "1111", 11);
        
//Set the default value to null for the experiment
ExperimentKey<String> OTHER = new ExperimentKey<String>("other", String.class, null)
        //Set up the experimental layer
        .layer("other_layer")
        //Experimental grouping, the specified traffic is 20%, the vid is 111, and the experimental result is 1.
        .clientGroup(0.2, "111", "yes")
        //Experimental grouping, the specified traffic is 20%, the vid is 1111, and the experimental result is 11.
        .clientGroup(0.2, "1111", "no");        
```


<span id="de01d833"></span>
## Obtain experimental results

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If there is an experimental key conflict, that is, if both the server side and the local have the same experimental key, then the experimental fetch has priority, follow the following process:</div>


<div data-tips="true" data-tips-type="tip"><strong>Server</strong> <strong>side offload experimental value \- \> client side offload value \- \> default value.</strong></div>


```Java
//Get the experimental results by experiment.getValue (abClientExperiment)
//You need to pass in the corresponding instance of abClientExperiment.
Integer value = ALIVE_IS_MONITOR_ENABLE.getValue(abClientExperiment);
```


<span id="e87e14a7"></span>
## Clear this layer experimental results

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Call the API for any local experimental configuration modification or re\-triggering of local experimental offload results.</div>


```Java
String layer = "default_layer";
//Call clearLayerAssign of abClientExperiment to reset this layer experiment
abClientExperiment.clearLayerAssign(layer);
```


<span id="ac0d4ab5"></span>
## Custom local experiment randomization strategy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The client side shunt defaults to random numbers for local experiments. This method will cause the user group to be unstable after unloading and reloading. It can be customized to be random according to GAID, DID, etc.</div>


```Java
//Built-in two strategies IRandomStrategy:
RandomIntStrategy: use Random().nextInt(1000) to generate
RandomHashStrategy: use AndroidId Hash value combined with experimental key to generate

//Default random strategy
abClientExperiment.updateRandomStrategy(RandomIntStrategy.INSTANCE);

//Random way to combine key with Android Id
abClientExperiment.updateRandomStrategy(RandomHashStrategy.INSTANCE);

//Custom random strategy
abClientExperiment.updateRandomStrategy(new IRandomStrategy() {
    @Override
    public void initStrategy(@NonNull Context context) {
        
    }

    @Override
    public int getNextRandom(@NonNull String s) {
        return 0;
    }
});
```


Clear Local Experiment Vid

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Whether it is server side experiment, or local experiment, all record exposure vid after the event exposure, that is, the corresponding ab_sdk_version in AppLog, but because the local experiment is added by the client side, it is possible that after the experimental code is deleted, vid is still cached in ab_sdk_version and therefore invalidated.</div>


```Java
Currently supports two types of vid input methods
//Pass directly to List
List<String> vidList = new ArrayList<>();
vidList.add("vid1");
vidList.add("vid2");
vidList.add("vid3");
abClientExperiment.clearClientVid(vidList);

//pass in string by splitting
abClientExperiment.clearClientVid("vid1,vid2,vid3");
```


<span id="28902071"></span>
## Set up debug callbacks

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We know the following information from the exposure triggered by the local shunt experiment plug\-in through the callback:</div>



* <div data-tips="true" data-tips-type="tip">Experiment key</div>


* <div data-tips="true" data-tips-type="tip">Experimental results</div>


   <div data-tips="true" data-tips-type="tip">Where did the experimental results come from?   </div>
   

* <div data-tips="true" data-tips-type="tip">Experimental results correspond to vid</div>


* <div data-tips="true" data-tips-type="tip">Experimental group</div>



```Java
//set debug callback
abClientExperiment.setDebugInfoCallback((key, value, from, vid, clientVidList) -> Log.d(
        "[AbClientExperiment]",
        "debugCallback " + key + "，vid：" + vid + "，value：" + value + "，from：" + from + "，clientVidList：" + clientVidList
));

The log output is as follows:
debugCallback alive_is_monitor_enable，vid：111，value：1，from：client，clientVidList：[Pair{111 0.2}, Pair{1111 0.2}]
```


<span id="0b6b550f"></span>
# Create experiments on the local client side \-IOS

<span id="d4cc2cf7"></span>
## Configure local experiments


* layerName: Specify the experimental layer. The experiments under the experimental layer are mutual exclusion. After shunting, only one experimental group hits at most.

* Key: The identification of the experiment. When obtaining the experimental value, the hit experimental group will be found through this identification

* Rate: The ratio of the experimental group to the current experimental layer, the value range is 0~ 1, 0 represents 0%, 1 represents 100%, and the accuracy is 0.01%.

* Vid: A vid generated on ABTest's local experiment page, uniquely labeled for each experiment group, for statistical experiment exposure

* Value: The experimental value of the experiment to which the experimental group belongs. When obtaining the experimental value, if the current experimental group hits, return this value


```objectivec
BDAutoTrackExperiment *experiment1 = [[BDAutoTrackExperiment alloc] initWithKey:@"pageType" groups:@[
    [[BDAutoTrackExperimentGroup alloc] initWithRate:0.4 vid:@"1002" value:@(1)],
    [[BDAutoTrackExperimentGroup alloc] initWithRate:0.4 vid:@"1003" value:@(2)],
]];
[BDAutoTrack.sharedTrack addABClientExperiment:experiment1 layerName:@"layer1"];
```


<span id="3a36e86a"></span>
## Obtain experimental results

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When obtaining experimental results, you should first obtain them from server\-level experiments. If not, you should obtain them from local experiments. Follow these rules:</div>


<div data-tips="true" data-tips-type="tip"><strong>Server</strong> <strong>side offload experimental value \- \> client side offload value \- \> default value</strong></div>


```objectivec
NSNumber *value = [BDAutoTrack.sharedTrack ABTestConfigValueForKey:@"pageType" defaultValue:@(3)];
```


<span id="3951d449"></span>
## Remove exposed Vids from local experiments

The exposed vids of the local experiment will be cached locally. After the experiment is over, the cached vids will still be reported and can be removed through this interface.

```objectivec
[BDAutoTrack.sharedTrack clearABClientExposedVids];
```


<span id="fa7204ee"></span>
## Complete example

A complete example of a local experiment is as follows:

```objectivec
BDAutoTrackExperiment *experiment1 = [[BDAutoTrackExperiment alloc] initWithKey:@"pageType" groups:@[
    [[BDAutoTrackExperimentGroup alloc] initWithRate:0.4 vid:@"1002" value:@(1)],
    [[BDAutoTrackExperimentGroup alloc] initWithRate:0.4 vid:@"1003" value:@(2)],
]];
[BDAutoTrack.sharedTrack addABClientExperiment:experiment1 layerName:@"layer1"];

NSNumber *value = [BDAutoTrack.sharedTrack ABTestConfigValueForKey:@"pageType" defaultValue:@(3)];
NSString *vids = [BDAutoTrack.sharedTrack abExposedVids];
NSLog(@"pageType >>> value: %@, vids: %@", value, vids);
```


<span id="072ac954"></span>
# Debugging experiment

After the experiment is created, you can view the created experiments in the A/B Testing \> Experiments list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4731e7999a4d490f9bd1ce7673f65efb~tplv-goo7wpa0wc-image.image) </span>

**Debugging**: the newly created experiment, the experimental state is **debugging**, the local shunt experiment does not need to be manually opened, and the created completion state is **debugging**.

<span id="c54b8e1b"></span>
# View the experimental report

After the experiment takes effect, you can also click to enter the experimental report page through the experimental operation entrance in the experimental list to view the experimental report.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Local shunt experiments, while debugging, you can also view the experimental report. According to the client side, technical staff need to consider the time of data calculation in the control experimental report by reporting the control data.</div>
