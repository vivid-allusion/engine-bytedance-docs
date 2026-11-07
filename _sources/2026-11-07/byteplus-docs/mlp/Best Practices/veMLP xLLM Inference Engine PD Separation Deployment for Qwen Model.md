---
title: "veMLP xLLM Inference Engine PD Separation Deployment for Qwen Model"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/veMLP_xLLM_Inference_Engine_PD_Separation_Deployment_for_Qwen_Model"
---

xLLM is a high\-efficiency inference framework **self\-developed** by ModelArk, supporting features such as PD separation (Prefiling, Decoding) and elastic scaling, with performance significantly ahead of open\-source frameworks

In the inference service of Byteplus Machine Learning Platform (veMLP), productized support for PD separation deployment functionality using the xLLM inference engine has been implemented Through this article, you can use the xLLM preset image to deploy the Qwen3 model inference service; this article will also provide performance data comparison between the xLLM image and the open\-source version of vLLM

<span id="225ba667"></span>
# Deploy Online Service

**Preset Model Information**


|Model |path |
|---|---|
|Qwen3\-235B\-A22B |tos://preset\-models\-cn\-beijing\-tob\-demo/Qwen/Qwen3\-235B\-A22B\-veMLP/ |
|Qwen3\-32B |tos://preset\-models\-cn\-beijing\-tob\-demo/Qwen/Qwen3\-32B/ |
|Qwen2.5\-32B |tos://preset\-models\-cn\-beijing\-tob\-demo/Qwen/Qwen2.5\-32B\-Instruct/ |
|Qwen2.5\-72B |tos://preset\-models\-cn\-beijing\-tob\-demo/Qwen/Qwen2.5\-72B\-Instruct/ |


> Tips: Note that the image and model path need to be adjusted appropriately according to the Region location e.g., the sample Qwen3\-32B file is located in the cn\-beijing Region, with the TOS path being tos://preset\-models\-cn\-beijing\-tob\-demo/Qwen/Qwen3\-32B; if the file is located in the cn\-beijing2 Region, adjust the TOS path to tos://preset\-models\-cn\-beijing2\-tob\-demo/Qwen/Qwen3\-32B The same applies to the image address


<span id="25a21dc4"></span>
## 1. Create Service

<span id="a9c63ec5"></span>
#### Create Service


* Correctly fill in [Service Name], [Private Network], [API Gateway], 8000 service inference port, 8080 monitoring metric collection port, and other **information.** 


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the POC specifies 8000 and 8080, <strong>do not change the port</strong>, and <strong>double\-check whether the security group and ACL have opened all ports in advance.</strong></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74c80e4504ae459b94c183a315c3b154~tplv-goo7wpa0wc-image.image) </span>

<span id="1f0f12da"></span>
#### Create API Gateway (when creating a service for the first time)


* Correctly fill in **VPC**, **turn on VMP**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e0fe3e7fba74ec1b9327e86d233bf14~tplv-goo7wpa0wc-image.image) </span>

<span id="bf736f56"></span>
## 2. Create Deployment

<span id="655d85d7"></span>
### Add Deployment


* On the Deployment tab page of the service created above, click Add Deployment.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21195e2a40294bf783ba8f3d07108ad6~tplv-goo7wpa0wc-image.image) </span>


* **Correctly fill in the affiliated queue, GPU, and other information.** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea97f69714f5477a9b8e868f21ff68cd~tplv-goo7wpa0wc-image.image) </span>


* Prefill role and Decode role, **both need to correctly fill in the user model path**`$VEPFS_MODEL_PATH/Qwen/Qwen3-32B/` **.** 

* Select [Subnet], [Security Group], click Create, and wait for the instance to be queued and running.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e9e97b0812a46e1b6b88a8b70d7f506~tplv-goo7wpa0wc-image.image) </span>


* Observe the 【decode】 role instance logs: no model loading errors, waiting for model loading and running.

* Obtain the service call address from the Call Guide tab page of the online service. If encryption is required, turn on API Key verification on the current page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3309e9366f774a3aba58ff090a800ba7~tplv-goo7wpa0wc-image.image) </span>

<span id="6dcc58f6"></span>
## Model Deployment Recommendations

**Feature Limitations**


* Does not currently support 128K long text input.

* Does not currently support Function Call

* Does not currently support specifying response_format

* Does not currently support the enable\-thinking request field. You can add  **/think** and  **/no_think** in user prompts or system messages to switch the model's thinking mode.


```Bash
# think
curl -X POST <access address>/v1/chat/completions \
-H "Content-Type: application/json" -d '{
"model": "Qwen/Qwen3-235B-A22B,
"messages": [
{"role": "user", "content": "Help me design a three-day travel itinerary in Beijing /think"}
],
"max_tokens": 800
}'

# no_think
curl -X POST <access address>/v1/chat/completions \
-H "Content-Type: application/json" -d '{
"model": "Qwen/Qwen3-235B-A22B",
"messages": [
{"role": "user", "content": "Help me design a three-day travel itinerary in Beijing /no_think"}
],
"max_tokens": 800
}'
```


<span id="d6e84b7d"></span>
# Model Call

<span id="0174698e"></span>
## Call the model using an OpenAI\-compatible method

Once deployment is complete, a public network service is automatically created, providing HTTP OpenAI API endpoints It can be called using the OpenAI\-compatible API method e.g.:

```Bash
# streaming
curl -X POST <access address>/v1/chat/completions \
-H "Content-Type: application/json" -d '{
"model": "Qwen/Qwen3-32B",
"messages": [
{"role": "user", "content": "Help me design a three-day travel itinerary in Beijing"}
],
"max_tokens": 20,
"stream": true
}'

# non-streaming
curl -X POST <access address>/v1/chat/completions \
-H "Content-Type: application/json" -d '{
"model": "Qwen/Qwen3-235B-A22B",
"messages": [
{"role": "user", "content": "Help me design a three-day travel itinerary in Beijing"}
],
"max_tokens": 800
}'
```


<span id="9582b995"></span>
## Streaming Output Example

```JSON
{"id": "chatcmpl-17399634109****", "choices": [{"index": 0, "delta": {"role": "assistant", "content": "", "reasoning_content": "Okay", "tool_calls": []}, "finish_reason": ""}], "created": 1739963410, "model": "vemlp-deepseek-r1-enc", "system_fingerprint": "fp", "object": "chat.completion.chunk", "usage": {"prompt_tokens": 9, "completion_tokens": 1, "total_tokens": 10, "completion_tokens_details": {"reasoning_tokens": 1}}}
{"id": "chatcmpl-17399634109****", "choices": [{"index": 0, "delta": {"role": "assistant", "content": "", "reasoning_content": ",", "tool_calls": []}, "finish_reason": ""}], "created": 1739963410, "model": "vemlp-deepseek-r1-enc", "system_fingerprint": "fp", "object": "chat.completion.chunk", "usage": {"prompt_tokens": 9, "completion_tokens": 2, "total_tokens": 11, "completion_tokens_details": {"reasoning_tokens": 2}}}
...
```


<span id="01782166"></span>
## Non\-streaming Output Example

```Bash
{"id":"chatcmpl-1739963676****","object":"chat.completion","created":1739963676,"model":"vemlp-deepseek-r1-enc","system_fingerprint":"fp","choices":[{"index":0,"message":{"role":"assistant","content":"\n\nThe following is a three-day classic itinerary designed for you in Beijing, covering historical sites, royal gardens, modern landmarks and local cultural experiences. The itinerary is compact but combines work and rest:\n\n🌟 **Day 1: Classic Tour of the Central Axis**\n","reasoning_content":"Well, the user asked me to help design a three-day tour itinerary in Beijing. First, I need to consider the user's possible background and needs. As the capital of China, Beijing has many classic attractions, such as the Forbidden City, Tiananmen Square, the Great Wall, and so on. The user may be visiting Beijing for the first time and want to see these must-see places. However, it is also possible that they have already visited some attractions and want to experience them more deeply. However, it is usually safer to focus on classic attractions for the first design. \n\nNext, I have to make sure whether the three-day itinerary is reasonable. Beijing is very large, and the transportation time may need to be considered between attractions. For example, the Great Wall is in the suburbs and needs to be arranged separately for one day. The first day may be in the city center, arranging more concentrated places such as Tiananmen Square, the Forbidden City, and Jingshan. On the second day, you can consider the Summer Palace and the Old Summer Palace. Both of them are in Haidian District, a little far from the city center, but they can be placed on the same day. On the third day, you can arrange some cultural experiences, such as Hutong, Nanluoguxiang, 798 Art District, and so on. \n\nAlso pay attention to whether the time allocation is reasonable. For example, the Forbidden City requires half a day, If you add Tiananmen Square and Chairman Mao Memorial Hall, it may take a whole morning. Go to Jingshan Park in the afternoon, and then go to Wangfujing in the evening. Is this arrangement too rushed? It may need to be adjusted. In addition, the user's physical strength should be considered, especially the Great Wall may require a lot of walking in one day, so it may be more appropriate to arrange the Summer Palace and Yuanmingyuan on the second day, and the relatively relaxing cultural attractions on the third day. \n\nIn terms of food, users may want to experience Beijing's specialties, such as roast duck, noodles with soybean paste, shabu-shabu mutton, etc. Therefore, it is necessary to recommend nearby restaurants or snack streets in the daily itinerary. For example, lunch at the Old Town on the first day It may not be convenient to go to the palace, but you can recommend Wangfujing's snack street or nearby restaurants. If you have dinner in Wangfujing, Quanjude is a classic choice, but you may need to make a reservation in advance. \n\nIn terms of transportation, the Beijing subway is more convenient, but some attractions may require taxis or buses. For example, the Great Wall usually requires taking a bus or a tourist line, or joining a one-day tour group. Users should be reminded to pay attention to transportation time and method to avoid delays. \n\nIn addition, seasonal factors should also be considered. If it is summer, pay attention to sun protection and hydration; if it is winter, keep warm. But the user did not mention the specific time , you may need a general reminder. \n\nAlso pay attention to the opening hours and closing days of attractions. For example, the Forbidden City is closed on Mondays, so the itinerary should avoid Mondays. If the user does not know this, he may make a wasted trip. So a reminder is needed in the notes. \n\nPerhaps the user also wants to experience Beijing's culture, such as Hutong and Siheyuan, so the third day is arranged to visit Nanluoguxiang and Houhai, as well as 798 Art District, so that there is both traditional culture and modern art, which is more comprehensive. \n\nFinally, check whether the itinerary covers the main attractions in Beijing and whether three days are enough. Day 1: Tiananmen Square, Forbidden City, Jingshan, Wangfujing. Day 2: Great Wall, Bird's Nest and Water Cube. Day 3: Summer Palace, Old Summer Palace, Nanluoguxiang, Houhai. Or maybe you need to make some adjustments. For example, if you go to the Great Wall on the second day, you may be tired in the afternoon, so you can arrange the night view of the Bird's Nest and Water Cube in the evening. The Summer Palace and Old Summer Palace may be tight on the third day, but you can arrange to visit them in the morning and afternoon respectively. Or should you put the Summer Palace and Old Summer Palace on the second day, and the Great Wall on a separate day? You need to consider whether the route is reasonable. \n\nMaybe you go to the Great Wall on the second day, and go to the Bird's Nest and Water Cube after returning to the city. Cube, this is more convenient, because the Great Wall is in the northern suburbs, and the Bird's Nest is also in the north, which may be more suitable. The Summer Palace and the Old Summer Palace are in the western suburbs, so arrange them there on the third day, and then go to Nanluoguxiang and Houhai in the afternoon. Or vice versa? You need to check the map to confirm the geographical location. \n\nIn addition, users may be interested in watching the flag-raising ceremony, so you can suggest getting up early on the first morning to watch the flag-raising ceremony, but you need to check the time in advance, and you may need to get up very early. For example, the flag-raising ceremony is very early in summer. Are users willing? \n\nIn short, it is necessary to comprehensively consider the distribution of attractions, time arrangements, transportation, food and the user's physical strength to ensure that the itinerary is reasonable and feasible, not too rushed, and can cover the main attractions. \n","tool_calls":[]},"finish_reason":"length"}],"usage":{"completion_len":799,"prompt_len":12,"total_len":811,"completion_tokens_details":{"reasoning_tokens":758}}}
```


<span id="11433fcf"></span>
# Performance Test

<span id="f28be77e"></span>
## Inference Framework Performance Comparison

Take the Qwen3\-235B\-A22B model with 3500: 1500 as an example:


* The single\-machine maximum total throughput of Byteplus xLLM version Qwen3\-235B\-A22B inference can reach 7389 token/s, which is 146% of the vLLM version (4092 token/s).

* Under the SLO of TPOT < 35 ms, the throughput of Byteplus xLLM version is 161% of that of vLLM.


Take the Qwen3\-235B\-A22B model with 2500: 1500 as an example:


* The single\-machine maximum throughput of Byteplus xLLM version DeepSeek inference can reach 7259 tokens/s, with an output throughput of 2722 tokens/s, which is twice the throughput of the vLLM version.

* Under the SLO of TPOT < 35 ms, the single\-machine output throughput of Byteplus xLLM version can reach 1586 tokens/s, 81% higher than that of the vLLM version.


When performing Qwen3\-32B inference under the SLO of TPOT < 40ms, the throughput of xLLM is approximately twice that of the open\-source framework.


* When the input\-output ratio is 3500:1500, the average single\-machine output throughput of Byteplus xLLM version can reach 774 token/s, which is 171% of the performance of the vLLM version.

* When the input\-output ratio is 2500:1500, the average single\-machine output throughput of Byteplus xLLM version can reach 908 token/s, while the single\-machine output throughput of the vLLM version is 557 token/s, an increase of 63%.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6c9b78cc5bb4a3f9348256d051d18b9~tplv-goo7wpa0wc-image.image) </span>

<span id="38255d3c"></span>
## Qwen3\-32B Performance Test

<span id="b584e65e"></span>
### 3500: 1500

<span id="205b3ea0"></span>
#### xLLM torch version


|TPOT |input_len |output_len |Equivalent Single Machine Throughput (req/s) |Equivalent Single Machine Output Throughput (token/s) |Equivalent Single Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 40 |3,500 |1500 |0.52 |773.82 |2579.38 |1289.69 |39.00 |
|< 30 |3,500 |1500 |0.42 |622.90 |2076.35 |1038.17 |27.81 |
|< 20 |3,500 |1500 |0.35 |521.26 |1737.50 |868.75 |18.93 |


<span id="68f5b0e2"></span>
#### vLLM


|TPOT |input_len |output_len |Equivalent Single Machine Throughput (req/s) |Equivalent Single Machine Output Throughput (token/s) |Equivalent Single Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 50 |3,500 |1500 |0.36 |538.51 |1795.03 |897.52 |50.44 |
|< 45 |3,500 |1500 |0.31 |462.17 |1540.57 |770.28 |44.11 |
|< 40 |3,500 |1500 |0.30 |452.99 |1509.97 |754.98 |40.08 |
|< 35 |3,500 |1500 |0.29 |465.94 |1553.13 |776.57 |36.43 |
|< 30 |3,500 |1500 |0.09 |133.61 |445.37 |222.68 |29.58 |


<span id="3b8ba7d5"></span>
### 2500:1500

<span id="6d92d955"></span>
#### xLLM torch version


|TPOT |input_len |output_len |Equivalent Single Machine Throughput (req/s) |Equivalent Single Machine Output Throughput (token/s) |Equivalent Single Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 40 |2500 |1500 |0.60 |908.44 |2422.51 |1211.26 |35.83 |
|< 30 |2500 |1500 |0.53 |789.84 |2106.27 |1053.13 |29.91 |
|< 20 |2500 |1500 |0.39 |578.92 |1543.80 |771.90 |18.23 |


<span id="72785bea"></span>
#### vLLM


|TPOT |input_len |output_len |Equivalent Single Machine Throughput (req/s) |Equivalent Single Machine Output Throughput (token/s) |Equivalent Single Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 40 |2500 |1500 |0.37 |557.37 |1486.32 |743.16 |38.5 |
|< 35 |2500 |1500 |0.36 |543.47 |1449.25 |724.63 |34.72 |
|< 30 |2500 |1500 |0.09 |133.26 |355.36 |177.68 |29.28 |


<span id="68404581"></span>
## Qwen3\-235B\-A22B Performance Test

<span id="40476f2d"></span>
### 3500: 1500

<span id="ace7e2fe"></span>
#### xLLM xperf version


|TPOT |input_len |output_len |Equivalent Single Machine Throughput (req/s) |Equivalent Single Machine Output Throughput (token/s) |Equivalent Single Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 50 |3,500 |1500 |1.90 |2849.55 |9498.51 |831.12 |49.10 |
|< 40 |3,500 |1500 |1.57 |2358.10 |7860.34 |687.78 |39.20 |
|< 30 |3,500 |1500 |0.79 |1189.94 |3966.45 |347.06 |27.71 |


<span id="c2878eaa"></span>
#### vLLM


|TPOT |input_len |output_len |Equivalent Single\-Machine Throughput (req/s) |Equivalent Single\-Machine Output Throughput (token/s) |Equivalent Single\-Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 40 |3,500 |1500 |0.63 |947.88 |3159.60 |394.95 |39.68 |
|< 35 |3,500 |1500 |0.56 |845.16 |2817.20 |352.15 |35.65 |
|< 30 |3,500 |1500 |0.56 |835.88 |2786.27 |348.28 |28.07 |
|< 25 |3,500 |1500 |0.41 |620.07 |2066.90 |258.36 |25.62 |
|< 20 |3,500 |1500 |0.25 |381.56 |1271.87 |158.98 |20.79 |


<span id="5f8115bb"></span>
#### SGLang


|TPOT |input_len |output_len |Equivalent Single Machine Throughput (req/s) |Equivalent Single Machine Output Throughput (token/s) |Equivalent Single Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 40 |3,500 |1500 |0.43 |640.10 |2133.67 |266.71 |40.22 |
|< 35 |3,500 |1500 |0.39 |592.09 |1973.63 |246.70 |34.48 |
|< 30 |3,500 |1500 |0.34 |508.78 |1695.93 |211.99 |29.12 |


<span id="c0b0b0c9"></span>
### 2500: 1500

<span id="a9f7163d"></span>
#### xLLM xperf version


|TPOT |input_len |output_len |Equivalent Single\-Machine Throughput (req/s) |Equivalent Single\-Machine Output Throughput (token/s) |Equivalent Single\-Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 50 |2500 |1500 |2.19 |3278.88 |8743.69 |1092.96 |49.11 |
|< 40 |2500 |1500 |1.86 |2788.16 |7435.14 |929.39 |38.94 |
|< 30 |2500 |1500 |0.67 |997.92 |2661.01 |332.63 |29.39 |


<span id="e1657012"></span>
#### vLLM


|TPOT |input_len |output_len |equivalent single\-machine throughput (req/s) |Equivalent Single Machine Output Throughput (token/s) |Equivalent Single Machine Throughput (token/s) |Equivalent Single Card Throughput (token/s) |Mean TPOT |
|---|---|---|---|---|---|---|---|
|< 35 |2500 |1500 |0.64 |965.49 |2574.64 |321.83 |32.87 |
|< 30 |2500 |1500 |0.56 |841.39 |2243.71 |280.46 |28.26 |
|< 25 |2500 |1500 |0.41 |612.99 |1634.64 |204.33 |25.86 |
|< 20 |2500 |1500 |0.25 |379.04 |1010.77 |126.35 |20.92 |
