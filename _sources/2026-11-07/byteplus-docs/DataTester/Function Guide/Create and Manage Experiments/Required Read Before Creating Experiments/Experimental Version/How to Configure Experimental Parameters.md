---
title: "How to Configure Experimental Parameters"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/How-to-Configure-Experimental-Parameters"
---

<span id="一-概述"></span>
# 1. Overview

The experimental parameters are a supplement to the experimental version. Generally, it is a functional control configuration item used to distinguish between the control group and the experimental group. The experimental parameters need to be obtained and parsed by the developer to take effect. When creating an experiment, by configuring the experimental parameters, not only can the experimental flow be achieved, but also a good experimental parameter design can help the experimental creator to conduct more flexible experiments without increasing the development workload.


* For example, a short video e\-commerce recommendation operator made a hypothesis: after users see the video with goods, they may directly slide away or even exit the APP, that is, the display timing of the product card will affect the user's consumption time of the video.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/603ce7aaf78047818a9b5e7c03e09f3a~tplv-goo7wpa0wc-image.image) </span>


Experiments can be designed as follows:


> * Control group: Show the product card immediately when the video starts playing

> * Experimental group 1: Display the product card after 5 seconds of video playback

> * Experimental group 2: Display the product card after 10 seconds of video playback


With the help of the experimental parameter configuration function, first parse the goods_card_show_time parameters in the code and display the product card after video playback {goods_card_show_time} seconds, and then configure the control group/experimental group 1/experimental group 2 goods_card_show_time = 0/5/10 when creating the experiment, you can complete the online of the experiment.

If you want to experiment with the effect of "showing the product card after 8 seconds of video playback" later, you don't need to modify the code, just configure the experimental parameters to goods_card_show_time = 8 when creating the experiment, and even create multiple groups of experiments by configuring different parameter values and then take the optimal goods_card_show_time value to publish.

<span id="二-参数类型及示例"></span>
# 2. Parameter types and examples

<span id="number"></span>
## Number

> Example: In the e\-commerce recommendation scenario, the product card display timing experiment

> * Control group: Show the product card immediately when the video starts playing

> * Experimental group: Display the product card after 5 seconds of video playback


In the code implementation, the analysis experimental parameters goods_card_show_time the video playback time. When creating an experiment, the parameters of configuring the control group and the experimental group are as follows:

```plain
Control group configuration:
        "goods_card_show_time": 0
Experimental group configuration:
        "goods_card_show_time": 5
```


<span id="string"></span>
## **String**

> Example: A video recommendation prompts users to follow a copywriting experiment

> * Control group: no guidance

> * Experiment Group 1: Follow the spike

> * Experimental Group 2: Multiple friends follow


In the code implementation, the parsing experiment parameter follow_guide_tips string, which means to guide the user to pay attention to the copy. When creating an experiment, the parameters of configuring the control group and the experimental group are as follows:

```plain
Control group configuration:
        "follow_guide_tips": ""
Experimental group 1 configuration:
        "follow_guide_tips": "关注飙升" //followers increasing
Experimental group 2 configuration:
        "follow_guide_tips": "多位好友关注" //multiple friends followed
```


<span id="boolean"></span>
## **Boolean**

> Example: Video recommendation scene, control whether to show interactive guidance

> * Control group: do not show interactive guidance

> * Experimental Group: Demonstration Interactive Initiation


In the code implementation, the parsing experiment parameters show_interact_guide boolean values, indicating whether to display interactive guidance. When creating an experiment, the parameters for configuring the control group and the experimental group are as follows:

```plain
Control group configuration:
        "show_interact_guide": false
Experimental group configuration:
        "show_interact_guide": true
```


<span id="json"></span>
## **Json**

It is generally used in scenarios of multi\-functional joint experiments, where multiple parameter combinations are required to control the experimental logic.

> Example: Video recommendation scene, controlling whether to display interactive guidance, and interactive guidance display timing and display duration experiment

> * Control group: do not show interactive guidance

> * Experimental group 1: show interactive guidance, and show interactive guidance for 3 seconds when there are 10 seconds left in the video playback

> * Experimental Group 2: Show interactive guidance, and show interactive guidance for 5 seconds when there are 15 seconds left in the video playback


Code implementation, parsing JSON format experimental parameters, where show_interact_guide indicates whether to show interactive guidance, show_interact_guide_duration indicates interactive guidance display duration, play_video_countdown indicates video playback countdown. When creating an experiment, the parameters for configuring the control group and the experimental group are as follows:

```plain
Control group configuration:
{
        "show_interact_guide": false
}

Experimental group 1 configuration:
{
        "show_interact_guide": true,
        "show_interact_guide_duration": 3,
        "play_video_countdown": -10
}
Experimental group 2 configuration:
{
        "show_interact_guide": true,
        "show_interact_guide_duration": 5,
        "play_video_countdown": -15
}
```


<span id="三-参数设计"></span>
# 3. Parameter design

The experimental parameters are a functional control configuration from the perspective of the developer, so it is necessary to avoid a misunderstanding when designing AB parameters, and do not design parameters according to the experimental design. For example, the following experiment:

> Experimental group:

> * Experiment Group 1: Dissimilation after only manipulating information for 5 seconds

> * Experimental group 2: Scroll up in plan 1, and alienate after 5 seconds without operation information

> * Experimental Group 3: Plan 1 + Operation Information After 5 Seconds

> * Experimental group 4: Only the effect of plan 2 (hover together and then scroll together), dissimilation after 5 seconds without operation information

> * Experiment Group 5: Effect of Plan 2 + Operation Information Alienation after 5 seconds


An inappropriate experimental parameter design scheme is to enumerate all experimental groups (as follows preview_expose_style design). At this time, the control of functions can only be handled by hardcoding. If it involves experimental scheme adjustment, or other experiments need to reuse some functions, it needs to be developed separately.

```json
{
    "webcast": {
        "preview_expose_style": 1, //1/2/3/4/5 correspond to different experimental groups 1/2/3/4/5
    }
}
```


The appropriate AB parameter design should be designed according to the functional control perspective. For the above experiment, the following control parameters can be designed, and then the effect of the experimental group can be achieved by combining these parameters.

```json
{
    "webcast": {
        "guide_change": 1, //Is the operation information alienated?
        "guide_change_after": 5000, //Operation information X milliseconds after alienation
        "preview_expose_style": 1, //1,2 corresponds to the effect of plan 1 and plan 2 respectively
    }
}
```


Experimental Group 1:

```json
{
    "webcast": {
        "guide_change": 1,
        "guide_change_after": 5000
    }
}
```


Experiment Group 2:

```json
{
    "webcast": {
        "preview_expose_style": 1
    }
}
```


Experiment Group 3:

```json
{
    "webcast": {
        "guide_change": 1,
        "guide_change_after": 5000,
        "preview_expose_style": 1
    }
}
```


Experiment Group 4:

```json
{
    "webcast": {
        "preview_expose_style": 2
    }
}
```


Experiment Group 5:

```json
{
    "webcast": {
        "guide_change": 1,
        "guide_change_after": 5000,
        "preview_expose_style": 2
    }
}
```
