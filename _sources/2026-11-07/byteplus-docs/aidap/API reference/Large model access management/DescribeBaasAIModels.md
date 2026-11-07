---
title: "DescribeBaasAIModels"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/DescribeBaasAIModels"
---

Call the DescribeBaasAIModels API to query the model list supported by the AI models access function.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

This API can only be used to operate the workspace using the Supabase engine.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|WorkspaceId |String |Yes |vivid\-onion\-1122\*\*\*\* |ID of the workspace. |
|BranchId |String |Yes |br\-dandy\-cusk\-d7b1\*\*\*\* |Branch ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Models |Array of [AIModel](https://docs.byteplus.com/en/docs/330/114170#aimodel) |Refer to the sample response. |Model list. |


<span id="aimodel"></span>
### AIModel


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Description |String |Refer to the sample response. |Description of the model. |
|DisplayName |String |Doubao\-Seed\-2.0\-pro |Model's display name |
|Domains |Array of String |Refer to the sample response. |Model domain list. Values: `LLM`, `ComputerVision`, `Audio` and `Embedding`. |
|Introduction |String |Refer to the sample response. |Model introduction. |
|Name |String |bytedance/doubao\-seed\-2.0\-pro |The official name of the model. |
|ShortName |String |Refer to the Sample response. |Abbreviation of the model. |
|TaskTypes |Array of String |Refer to the sample response. |List of task types supported by the model. Values: `Chat`, `TextToImage`, `TextToVideo`, `ImageTo3D`, `ImageToImage`, `ImageToVideo`, `VisualQuestionAnswering`, `SpeechToSpeech`, `TextEmbedding`, `ImageEmbedding`, and `MultimodalEmbedding`. |
|VendorName |String |ByteDance |Model developer. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```JSON
POST /?Action=DescribeBaasAIModels&Version=2025-10-01
Content-Type: application/json
Host: aidap.cn-beijing.byteplusapi.com.cn
X-Date: 20251001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20251001/cn-beijing/aidap/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "WorkspaceId": "vivid-onion-1122****",
    "BranchId": "br-dandy-cusk-d7b1****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260707114942C83FBEEECE235EECEB6A-f99354",
        "Action": "DescribeBaasAIModels",
        "Version": "2025-10-01",
        "Service": "aidap",
        "Region": "cn-beijing"
    },
    "Result": {
        "Models": [
            {
                "Description": "旗舰级全能通用模型，面向 Agent 时代的复杂推理与长链路任务执行场景。强调多模态理解、长上下文推理、结构化生成与工具增强执行。复杂指令与多约束执行能力突出，可稳定应对多步复杂规划、复杂图文推理、视频内容理解与高难度分析等场景。",
                "DisplayName": "Doubao-Seed-2.0-pro",
                "Domains": [
                    "LLM"
                ],
                "Introduction": "Doubao-Seed-2.0 系列，围绕大规模生产环境下的使用需求做了系统性优化，旨在帮助突破真实世界中的复杂任务，通过 [pro](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-pro\u0026Tab=model-info)、 [lite](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-lite\u0026Tab=model-info)、 [mini](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-mini\u0026Tab=model-info) 、 [Code/preview](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-code\u0026Tab=model-info) 全系列尺寸，为不同规模与复杂度的应用场景提供专业级支持。\n# Doubao-Seed-2.0-pro 介绍\nDoubao-Seed-2.0-pro是旗舰级全能通用模型，面向 Agent 时代的复杂推理与长链路任务执行场景。强调多模态理解、长上下文推理、结构化生成与工具增强执行。复杂指令与多约束执行能力突出，可稳定应对多步复杂规划、复杂图文推理、视频内容理解与高难度分析等场景。\n# 新特性说明\n- **企业级 Agent 编排与交付能力升级**：面向知识密集型流程，复杂检索、工具调用与多步任务可自动编排并稳定交付；代码能力进一步“智能体化”，代码向智能体版本进一步优化，覆盖工程化拆解与端到端应用开发。\n- **更可靠的复杂指令执行**：提升了指令遵循表现，并强化了对多约束、多步骤、长链路任务的理解与执行能力，已具备支撑高价值任务的能力基础。\n- **多模态理解与推理升级**：视觉感知、视觉推理与空间理解全面增强，对复杂版式文档、图表与图形等非结构化输入的解析更稳；多模态长上下文融合能力更强，支持更高保真结构化输出。\n- **长视频与实时视频流能力升级**：支持小时级长视频的连贯理解与高精度推理，并具备流式实时分析与主动反馈能力，实现从被动问答到主动指导的交互升级。\n- **ToB 高频任务与垂直场景适配**：在信息抽取、参考问答、文本分析等高频企业工作流上整体能力提升，并通过长尾领域知识与多源信息融合增强垂直领域可用性，覆盖更复杂的数据处理、分析与客服类 Agent 任务。\n- **视觉质量与预算策略可控更可控**：提供分档的图像质量与资源预算策略（`low`, `high`, `xhigh`），默认高质量模式提升可预期性，并支持更高质量档位以应对高密度文本、复杂图表与细节丰富场景。\n\n# Coding场景\n在Coding场景下，优先推荐[Doubao-Seed-2.0-Code](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-code\u0026Tab=model-info)。其在 Seed 2.0 优秀的 Agent、VLM 能力基础上，特别增强了代码能力，不仅前端能力表现出众，也对企业常见的多语言编码需求做了特别优化，适合接入各种 AI 编程工具使用。\n\n# 260215版本说明\n## 支持隐式缓存\n**无需额外配置，自动开启缓存命中**，适合Agentic等复杂上下文场景。请求内容的公共前缀会被自动缓存，但不保证缓存命中。通常需要累计至少 1024 个 tokens 才会触发缓存命中。对命中缓存的部分，按输入缓存命中刊例价计费。\n\n## temperature 、top_p 参数说明\n**为保障输出效果的稳定性**，系统将参数固定为 `temperature = 1`、`top_p = 0.95`，并忽略 API 请求中对上述参数的传入设置（以系统固定值为准）。\n\n## reasoning_effort 参数说明\n**支持思考程度可调节（reasoning effort）**：分为 `minimal`、`low`、`medium`、`high` 四种模式，其中`minimal`为不思考 \n```bash\ncurl https://ark.cn-beijing.volces.com/api/v3/chat/completions \\\n  -H \"Content-Type: application/json\" \\\n  -H \"Authorization: Bearer $ARK_API_KEY\" \\\n  -d $'{\n    \"model\": \"doubao-seed-2-0-pro-260215\",\n    \"reasoning_effort\": \"medium\",\n    \"messages\": [\n        {\n            \"content\": [\n                {\n                    \"image_url\": {\n                        \"url\": \"https://ark-project.tos-cn-beijing.ivolces.com/images/view.jpeg\"\n                    },\n                    \"type\": \"image_url\"\n                },\n                {\n                    \"text\": \"图片主要讲了什么?\",\n                    \"type\": \"text\"\n                }\n            ],\n            \"role\": \"user\"\n        }\n    ]\n}'\n\n```\n\n# 服务协议\n- 豆包模型服务协议：https://docs.byteplus.com/en/docs/82379/1142195\n- BytePlus方舟平台体验服务规则说明：https://docs.byteplus.com/en/docs/82379/1108564\n- BytePlus方舟平台安全信任服务协议：https://docs.byteplus.com/en/docs/83458/1108217\n\n",
                "Name": "bytedance/doubao-seed-2.0-pro",
                "ShortName": "",
                "TaskTypes": [
                    "Chat",
                    "VisualQuestionAnswering"
                ],
                "VendorName": "字节跳动"
            },
            {
                "Description": "面向真实编程环境优化的 Coding 模型，能稳定调用 Claude Code 等常见 IDE 中的工具。模型特别优化了前端能力，在使用常见的前端框架时能有良好表现。模型支持使用 Skills，可以配合多种自定义技能使用。",
                "DisplayName": "Doubao-Seed-2.0-Code",
                "Domains": [
                    "LLM"
                ],
                "Introduction": "Doubao-Seed-2.0 系列，围绕大规模生产环境下的使用需求做了系统性优化，旨在帮助突破真实世界中的复杂任务，通过 [pro](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-pro\u0026Tab=model-info)、 [lite](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-lite\u0026Tab=model-info)、 [mini](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-mini\u0026Tab=model-info)、 [Code/preview](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-code\u0026Tab=model-info)  全系列尺寸，为不同规模与复杂度的应用场景提供专业级支持。\n# Doubao-Seed-2.0-Code 介绍\nDoubao-Seed-2.0-Code 面向企业级编程需求优化，在 Seed 2.0 优秀的 Agent、VLM 能力基础上，特别增强了代码能力，不仅前端能力表现出众，也对企业常见的多语言编码需求做了特别优化，适合接入各种 AI 编程工具使用。\n# 新特性说明\n- **基于强大基座模型**：基于 Seed 2.0 的基座模型，Doubao-Seed-2.0-Code 有优秀的 Agentic 能力，支持 Skills 调用和自定义工具使用；VLM 能力优秀，支持基于图片的 Browser Use 等工具使用\n- **面向编程任务优化**：特别优化了使用各种编程语言和编程工具的能力，在多轮长程任务下表现出色；\n- **复杂指令遵循**：能理解长而复杂的编程指令，稳定交付符合预期的产物\n- **支持隐式缓存**：无需额外配置，自动开启缓存命中，适合Agentic等复杂上下文场景。请求内容的公共前缀会被自动缓存，但不保证缓存命中。通常需要累计至少 1024 个 tokens 才会触发缓存命中。对命中缓存的部分，按输入缓存命中刊例价计费\n\u003cspan style=\"background-color: #FEF9C2;\"\u003e**注意：对于个人开发场景，推荐订阅 [Coding Plan 套餐](https://www.byteplus.com/en/activity/codingplan)，接入教程参见[Coding Plan快速开始](https://docs.byteplus.com/en/docs/82379/1928261)。**\u003c/span\u003e\n\n# 方舟Coding Plan接入方式\n方舟 Coding Plan 是为广大开发者量身打造的AI  Coding场景订阅服务，支持最新的 Doubao-Seed-Code模型与多款主流 AI 编码工具，为开发者提供畅快、顶尖、无忧的编码体验，大幅提升代码编写效率与质量。\n\n## 活动入口\n点击访问[方舟Coding Plan活动官网](https://www.byteplus.com/en/activity/codingplan)，参与活动\n\n## 套餐概览\n| 套餐 | 适用场景 | 套餐价格 | 用量说明* |\n| :---: | :---: | :--- | :--- |\n| \u003cb\u003eLite 套餐\u003c/b\u003e | 中等强度的开发任务，适合大多数开发者 | 首购首月：9.9USD\u003cbr\u003e续费：40USD/月 | - 每5小时：最多约 1,200 次请求\u003cbr\u003e- 每周：最多约 9,000 次请求\u003cbr\u003e- 每月：最多约 18,000 次请求 |\n| \u003cb\u003ePro 套餐\u003c/b\u003e | 复杂项目开发，适合高强度工作的开发者 | 首购首月：49.9USD\u003cbr\u003e续费：200USD/月 | Lite套餐的5倍\u003cbr\u003e- 每5小时：最多约 6,000 次请求\u003cbr\u003e- 每周：最多约 45,000 次请求\u003cbr\u003e- 每月：最多约 90,000 次请求 |\n\u003e **注意**\n\u003e - 请求次数为模型调用次数预估值，通常一次用户提问会触发多次模型调用，且每次模型调用均会计入一次额度消耗，因此实际消耗的请求次数一般会多于用户提问次数。\n\u003e - 实际可用量会因项目复杂度、代码库规模、是否启用自动接受、是否开启 thinking 等因素而有所不同。\n## 配置编程工具\nCoding Plan 支持 Claude Code、Cursor、Cline、Codex CLI、veCLI等编程工具。下面以Claude Code为例介绍如何使用 Coding Plan。\n接入其他编程工具，请参见[接入AI编程工具](https://docs.byteplus.com/en/docs/82379/1928262)。\n## 安装Claude Code\n前提条件:\n-安装 [Node.js 18 或更新版本环境](https://nodejs.org/en/download/)。\n-Windows 用户需安装 [Git for Windows](https://git-scm.com/download/win)。\n\n在命令行界面，执行以下命令安装 Claude Code。\n```Bash\nnpm install -g @anthropic-ai/claude-code\n```\n\n安装结束后，执行以下命令查看安装结果，若显示版本号则安装成功。\n```Bash\nclaude --version\n```\n\n## 配置环境变量\n\n完成Claude Code安装后，配置以下环境变量。\n**ANTHROPIC_BASE_URL**：`https://ark.cn-beijing.volces.com/api/coding`\n**ANTHROPIC_AUTH_TOKEN**：[获取API Key](https://console.byteplus.com/ark/region:ark+cn-beijing/apikey)。\n**ANTHROPIC_MODEL**: `doubao-seed-code-preview-latest`。\n\n\n\u003cdiv type=\"doc-tabs\"\u003e\n1.在终端执行以下命令进入Claude Code配置文件。\n    \n   ```Bash\n   vim ~/.claude/settings.json\n   ```\n\n2.编辑配置文件，文件内容如下，请替换对应的环境变量值。\n   ```JSON\n   {\n       \"env\": {\n           \"ANTHROPIC_AUTH_TOKEN\": \"ARK_API_KEY\",\n           \"ANTHROPIC_BASE_URL\": \"https://ark.cn-beijing.volces.com/api/coding\",\n           \"API_TIMEOUT_MS\": \"3000000\",\n           \"CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC\": 1,\n           \"ANTHROPIC_MODEL\": \"doubao-seed-2.0-code\"\n       }\n   }\n   ```\n\u003e 注意：\n    以上model_id：`doubao-seed-2.0-code`仅支持Coding Plan访问\n    企业客户配置方法请参考[接入第三方工具](https://docs.byteplus.com/en/docs/82379/2160841?lang=zh)\n\n3.打开一个新的终端窗口，环境变量才能生效。\n\n4.使用Claude Code\n-进入项目目录，执行`claude`命令，即可开始使用Claude Code。\n   ```Bash\n   cd my-project\n   claude\n   ```\n\n-模型状态验证：输入`/status`确认模型状态。\n   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66ac411648f34406ad71214db090d86d~tplv-goo7wpa0wc-image.image)\n   如果提示信息如下，可能是由于之前已登录过Claude Code，可输入`/logout`退出登录，然后再启动Claude Code。\n   ```JSON\n   {\n       \"error\": {\n           \"code\": \"AuthenticationError\",\n           \"message\": \"The API key format is incorrect. Request id:0217xxxxxxx\",\n           \"param\": \"\",\n           \"type\": \"Unauthorized\"\n       }\n   }\n   ```\n\n\u003c/div\u003e\n\n# API按量付费接入方式\n企业客户使用按tokens后付费方式接入，请参考以下API文档：\n- Chat API 文档详见：[API参考/对话(Chat) API](https://docs.byteplus.com/en/docs/82379/1494384)\n- Responses API 文档详见：[API参考/Responses API](https://docs.byteplus.com/en/docs/82379/1569618)\n- 其他第三方工具 文档详见：[接入第三方工具](https://docs.byteplus.com/en/docs/82379/2160841)\n\n\n# 服务协议\n- 豆包模型服务协议：https://docs.byteplus.com/en/docs/82379/1142195\n- BytePlus方舟平台体验服务规则说明：https://docs.byteplus.com/en/docs/82379/1108564\n- BytePlus方舟平台安全信任服务协议：https://docs.byteplus.com/en/docs/83458/1108217\n\n",
                "Name": "bytedance/doubao-seed-2.0-code",
                "ShortName": "",
                "TaskTypes": [
                    "Chat",
                    "VisualQuestionAnswering"
                ],
                "VendorName": "字节跳动"
            },
            {
                "Description": "面向高频企业场景兼顾性能与成本的均衡型模型，综合能力超越上一代Doubao-Seed-1.8。胜任非结构化信息处理、内容创作、搜索推荐、数据分析等生产型工作，支持长上下文、多源信息融合、多步指令执行与高保真结构化输出。在保障稳定效果的同时显著优化成本。",
                "DisplayName": "Doubao-Seed-2.0-lite",
                "Domains": [
                    "LLM"
                ],
                "Introduction": "Doubao-Seed-2.0 系列，围绕大规模生产环境下的使用需求做了系统性优化，旨在帮助突破真实世界中的复杂任务，通过 [pro](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-pro\u0026Tab=model-info)、 [lite](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-lite\u0026Tab=model-info)、 [mini](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-mini\u0026Tab=model-info) 、 [Code/preview](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-code\u0026Tab=model-info) 全系列尺寸，为不同规模与复杂度的应用场景提供专业级支持。\n# Doubao-Seed-2.0-lite 介绍\nDoubao-Seed-2.0-lite 是面向高频企业场景兼顾性能与成本的均衡型模型，综合能力超越上一代Doubao-Seed-1.8。胜任非结构化信息处理、内容创作、搜索推荐、数据分析等生产型工作，支持长上下文、多源信息融合、多步指令执行与高保真结构化输出。在保障稳定效果的同时显著优化成本。\n# 新特性说明\n- **Agent 可用性增强**：对比上一代模型 Doubao-Seed-1.8 能力大幅增强，指令遵循、推理、工具调用等能力优势显著，综合能力适配企业主流任务。\n- **多模态能力更实用**：面向常见图文输入的信息抽取、视频时空理解、grounding能力等表现更强，满足大多数文档/图表分析/视频caption需求。\n- **面向规模化部署**：保持能力优势的同时更低成本，适合高频调用与广覆盖场景。\n- **视觉质量与预算策略可控更可控**：提供分档的图像质量与资源预算策略（`low`, `high`, `xhigh`），默认高质量模式提升可预期性，并支持更高质量档位以应对高密度文本、复杂图表与细节丰富场景。\n\n# Coding场景\n在Coding场景下，优先推荐[Doubao-Seed-2.0-Code](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-code\u0026Tab=model-info)。其在 Seed 2.0 优秀的 Agent、VLM 能力基础上，特别增强了代码能力，不仅前端能力表现出众，也对企业常见的多语言编码需求做了特别优化，适合接入各种 AI 编程工具使用。\n\n# 260215版本说明\n## 支持隐式缓存\n**无需额外配置，自动开启缓存命中**，适合Agentic等复杂上下文场景。请求内容的公共前缀会被自动缓存，但不保证缓存命中。通常需要累计至少 1024 个 tokens 才会触发缓存命中。对命中缓存的部分，按输入缓存命中刊例价计费。\n\n## temperature 、top_p 参数说明\n**为保障输出效果的稳定性**，系统将参数固定为 `temperature = 1`、`top_p = 0.95`，并忽略 API 请求中对上述参数的传入设置（以系统固定值为准）。\n\n## reasoning_effort 参数说明\n**支持思考程度可调节（reasoning effort）**：分为 `minimal`、`low`、`medium`、`high` 四种模式，其中`minimal`为不思考 \n```bash\ncurl https://ark.cn-beijing.volces.com/api/v3/chat/completions \\\n  -H \"Content-Type: application/json\" \\\n  -H \"Authorization: Bearer $ARK_API_KEY\" \\\n  -d $'{\n    \"model\": \"doubao-seed-2-0-lite-260215\",\n    \"reasoning_effort\": \"medium\",\n    \"messages\": [\n        {\n            \"content\": [\n                {\n                    \"image_url\": {\n                        \"url\": \"https://ark-project.tos-cn-beijing.ivolces.com/images/view.jpeg\"\n                    },\n                    \"type\": \"image_url\"\n                },\n                {\n                    \"text\": \"图片主要讲了什么?\",\n                    \"type\": \"text\"\n                }\n            ],\n            \"role\": \"user\"\n        }\n    ]\n}'\n\n```\n\n# 服务协议\n- 豆包模型服务协议：https://docs.byteplus.com/en/docs/82379/1142195\n- BytePlus方舟平台体验服务规则说明：https://docs.byteplus.com/en/docs/82379/1108564\n- BytePlus方舟平台安全信任服务协议：https://docs.byteplus.com/en/docs/83458/1108217\n\n",
                "Name": "bytedance/doubao-seed-2.0-lite",
                "ShortName": "",
                "TaskTypes": [
                    "VisualQuestionAnswering",
                    "Chat"
                ],
                "VendorName": "字节跳动"
            },
            {
                "Description": "面向低时延、高并发与成本敏感场景，提供极致的模型推理速度。模型效果与Doubao-Seed-1.6相当。支持256k上下文、4档思考长度和多模态理解，适合成本和速度优先的轻量级任务。",
                "DisplayName": "Doubao-Seed-2.0-mini",
                "Domains": [
                    "LLM"
                ],
                "Introduction": "Doubao-Seed-2.0 系列，围绕大规模生产环境下的使用需求做了系统性优化，旨在帮助突破真实世界中的复杂任务，通过 [pro](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-pro\u0026Tab=model-info)、 [lite](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-lite\u0026Tab=model-info)、 [mini](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-mini\u0026Tab=model-info)、 [Code/preview](https://console.byteplus.com/ark/region:ark+cn-beijing/model/detail?Id=doubao-seed-2-0-code\u0026Tab=model-info)  全系列尺寸，为不同规模与复杂度的应用场景提供专业级支持。\n# Doubao-Seed-2.0-mini 介绍\nDoubao-Seed-2.0-mini 面向低时延、高并发与成本敏感场景，提供极致的模型推理速度。模型效果与Doubao-Seed-1.6相当。支持256k上下文、4档思考长度和多模态理解，适合成本和速度优先的轻量级任务。\n# 新特性说明\n- **高频简单场景的极致性价比**：面向高并发、短链路、标准化任务，强调“推理更快、部署更灵活”。非思考模式的综合表现达思考模式效果85%，但tokens消耗量只有1/10，在简单高频场景中实现快速响应与极致性价比。\n- **整体表现相比1.6-flash大幅度提升**：在内容识别和知识推理上相较上一代flash小尺寸模型大幅提升，超越Doubao-Seed-1.6-pro综合表现，代码和agent表现也有显著提高，满足企业常见图文输入的理解与结构化输出需求。\n- **ToB任务能力更强更稳定**：在图像审核、图像分类、视频巡检等tob常见领域的识别能力显著提升，异常模式相比 Doubao-Seed1.6-flash下 降40%，冗余问题有明显改善。\n- **视觉质量与预算策略可控更可控**：提供分档的图像质量与资源预算策略（`low`, `high`, `xhigh`），默认高质量模式提升可预期性，并支持更高质量档位以应对高密度文本、复杂图表与细节丰富场景。\n\n# 260215版本说明\n## 支持隐式缓存\n**无需额外配置，自动开启缓存命中**，适合Agentic等复杂上下文场景。请求内容的公共前缀会被自动缓存，但不保证缓存命中。通常需要累计至少 1024 个 tokens 才会触发缓存命中。对命中缓存的部分，按输入缓存命中刊例价计费。\n\n## reasoning_effort参数说明\n- **支持思考程度可调节（reasoning effort）**：分为 `minimal`、`low`、`medium`、`high` 四种模式，其中`minimal`为不思考\n  \n```bash\ncurl https://ark.cn-beijing.volces.com/api/v3/chat/completions \\\n  -H \"Content-Type: application/json\" \\\n  -H \"Authorization: Bearer $ARK_API_KEY\" \\\n  -d $'{\n    \"model\": \"doubao-seed-2-0-mini-260215\",\n    \"reasoning_effort\": \"medium\",\n    \"messages\": [\n        {\n            \"content\": [\n                {\n                    \"image_url\": {\n                        \"url\": \"https://ark-project.tos-cn-beijing.ivolces.com/images/view.jpeg\"\n                    },\n                    \"type\": \"image_url\"\n                },\n                {\n                    \"text\": \"图片主要讲了什么?\",\n                    \"type\": \"text\"\n                }\n            ],\n            \"role\": \"user\"\n        }\n    ]\n}'\n\n```\n\n# 服务协议\n- 豆包模型服务协议：https://docs.byteplus.com/en/docs/82379/1142195\n- BytePlus方舟平台体验服务规则说明：https://docs.byteplus.com/en/docs/82379/1108564\n- BytePlus方舟平台安全信任服务协议：https://docs.byteplus.com/en/docs/83458/1108217\n\n",
                "Name": "bytedance/doubao-seed-2.0-mini",
                "ShortName": "",
                "TaskTypes": [
                    "VisualQuestionAnswering",
                    "Chat"
                ],
                "VendorName": "字节跳动"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/aidap/error_code).
