---
title: "Allocating costs by project or API Key"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/projects-and-queues"
---

AI MediaKit supports allocating tool usage and costs by project or API Key. Choose a method based on the level of business isolation you need. You can also use projects to separate businesses and then use API Keys to distinguish the costs of applications, environments, or developers within the same project.

<span id="dc36b447"></span>
## Core concepts


|Concept |Description |
|---|---|
|BytePlus account |A BytePlus account, also called a main account, is the fundamental entity for resource ownership, usage metering, and billing. The account pays for and controls the resources that belong to it. |
|Project |A project is the fundamental unit for resource ownership and cost allocation in BytePlus. You can create separate projects for different business lines, products, or environments, such as development, testing, and production, to group resources, manage permissions, and allocate costs. |
|Queue |A queue is the AI MediaKit entity that receives tasks. Each queue belongs to a project. Submitting a task to a queue attributes the task and its costs to the project that owns the queue. |
|API Key |An API Key is a credential used to authenticate requests to AI MediaKit. Only general\-purpose API Keys created in the Identity and Access Management (IAM) console can be used as split items in the BytePlus Billing Center. Service\-specific API Keys created in the AI MediaKit console are not supported as split items. |


<span id="cc602dd7"></span>
## Choose a cost allocation method


|Method |Suitable scenarios |Configuration |Where to view the result |
|---|---|---|---|
|Allocate costs by project |Different clients, business lines, or environments need separate resources, tasks, and costs |Create a project and queue, and pass the project's `queue_id` when submitting a task |View usage by project in the AI MediaKit console and costs by project in the BytePlus Billing Center |
|Allocate costs by API Key |Different applications, test environments, or individual developers in the same project use different API Keys |Create a separate IAM general\-purpose API Key for each cost owner and use the corresponding API Key in the `Authorization` request header |Select API Key as the split dimension on the Split bills page |


You can combine the two methods when you need both cross\-business isolation and more granular cost accounting within a business. For example, create separate projects for production and testing, and then assign independent API Keys to different applications in the production project.

<span id="67adc112"></span>
## Allocate costs by project

Project\-based cost allocation is suitable when you need to isolate both resource management and costs. For example, a SaaS platform can create a project for each client, while an enterprise can create separate projects for different business lines or production and testing environments.

<span id="74149777"></span>
### Step 1: Create a project for each cost owner


1. Sign in to the BytePlus console and go to the [Project](https://console.byteplus.com/iam/resourcemanage/project) page.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/541a7580b133477db85a833a8472452e) </span>

2. Click **Create project**.

3. Enter a project name that identifies the cost owner. For example, use `client-[Client_ID]` to allocate costs by client, or use `production` and `testing` to allocate costs by environment.


After creating projects, use the project selector at the top of the AI MediaKit console to switch projects. The console view and available operations are scoped to the selected project. Usage statistics, tasks, queues, and project\-specific settings, including AI MediaKit service\-specific API Keys and callback configurations, are isolated by project.

<span id="98f6b817"></span>
#### Step 2: Create a queue in the project and obtain its queue ID

A `default` queue is automatically created in each project. You can use it directly or create additional queues for different business needs.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Each account can have up to 10 queues, including default queues.</div>


* <div data-tips="true" data-tips-type="default">A queue name cannot be changed after the queue is created.</div>



To create a queue:


1. Sign in to the [AI MediaKit console](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit?projectName=default).

2. Use the project selector at the top of the console to select the target project.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3e5f38ec42a3438a8cb465a533ffc4c7) </span>

3. In the left navigation pane, click **Queues**.

4. Click **Create queue** and enter a queue name.

5. After the queue is created, copy its queue ID from the queue list, for example, `q00a9731598092652e4a95292434198`.


We recommend storing the mapping between each cost owner and its `queue_id` in your business system. When submitting a task, retrieve the correct queue ID for the current client, business, or environment.

<span id="9874d156"></span>
#### Step 3: Provide the queue ID when submitting a task

Provide the target queue's `queue_id` in the request body of a task submission request. The following example attributes a video quality enhancement task to the project that owns the queue:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://client-a.storage.com/video.mp4",
  "tool_version": "professional",
  "resolution": "1080p",
  "queue_id": "q00a9731598092652e4a95292434198"
}'
```


If the queue belongs to the `client-a` project, the task and its costs are attributed to that project. If you omit `queue_id`, AI MediaKit uses the automatically created default queue, and the task and its costs are attributed to the project that owns that default queue.

<span id="afa8596a"></span>
#### Step 4: View usage and bills

After completing the configuration, view usage and costs by project:


* **View project usage**: Go to the [Usage](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/statistics) page in the AI MediaKit console and select a project from the project selector. The page displays usage data for the selected project.

* **View project costs**: Go to the [Bill details](https://console.byteplus.com/finance/bill/detail) page in the BytePlus Billing Center. Billing data is itemized by project, allowing you to view the costs attributed to projects such as `client-a` and `client-b`.


<span id="bb342b00"></span>
## Allocate costs by API Key

API Key\-based cost allocation is suitable when multiple cost owners exist in the same project. For example, assign different API Keys to business applications, development and testing environments, or individual developers, and separately account for the tool usage and costs generated by each Key.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">NOTE</div>


<div data-tips="true" data-tips-type="warning">Only general\-purpose API Keys created in the <a href="https://console.byteplus.com/iam/keymanage/">Identity and Access Management (IAM) console</a> can be used as split items in the BytePlus Billing Center. Service\-specific API Keys created in the AI MediaKit console are not supported. For information about the two API Key types, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#17a4192d">Prerequisites: obtain and configure your API key</a>.</div>


<span id="e667dc9f"></span>
### Step 1: Create an IAM general\-purpose API Key


1. Go to the [API Access Key](https://console.byteplus.com/iam/keymanage/) page in the IAM console and create a separate API Key for each application, environment, or developer whose costs need to be calculated independently. For IAM API Key creation and permission management instructions, see [Access Key & API Key](https://docs.byteplus.com/en/docs/IAM/about-access-keys).

2. Record the mapping between each API Key ID and its cost owner. Do not record the complete API Key in documentation, logs, or code repositories.


<span id="b85cba8a"></span>
### Step 2: Use the API Key when submitting a task

When submitting a task, use the IAM general\-purpose API Key assigned to the cost owner in the `Authorization` request header. The following example uses that API Key to submit a video quality enhancement task:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
-H 'Authorization: Bearer {IAM_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/video.mp4",
  "tool_version": "professional",
  "resolution": "1080p"
}'
```


No additional cost allocation parameter is required in the request. AI MediaKit records usage and costs against the IAM API Key that authenticates the request.

<span id="6d444647"></span>
### Step 3: Select API Key as the split dimension in the Billing Center


1. Go to the [Split bills](https://console.byteplus.com/finance/bill/split-bill) page in the BytePlus Billing Center. If split bills have not been activated, follow the on\-screen instructions to activate the service.

2. Click **Set product split dimensions** in the upper\-right corner and set the AI MediaKit split dimension to **apikey_id**.

3. Return to the Split bills page, filter for AI MediaKit bills, and view the tool usage and costs associated with each API Key ID.


Split bill data is generated only for new bills after the split bills service is activated and can be delayed by up to two days. The split item displays the API Key ID, not the complete API Key. For details about split bill fields and data rules, see [Split bills](https://docs.byteplus.com/en/docs/byteplus-platform/SplitBills).
