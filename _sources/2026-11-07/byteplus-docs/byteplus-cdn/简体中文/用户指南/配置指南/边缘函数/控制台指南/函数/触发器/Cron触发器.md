---
title: "Cron触发器"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn"
---

本文档介绍如何为函数配置 Cron 触发器。

您可以创建 Cron 触发器来创建定期任务，Cron 触发器会在指定时间自动触发函数代码中的 cron 事件。您需要在代码中监听并处理 cron 事件。

<span id="创建-cron-触发器"></span>
## 创建 Cron 触发器

参见以下步骤创建一个 Cron 触发器。


1. 打开 [函数管理](https://console.byteplus.com/cdn/edge-function/list) 页面。

2. 找到需要创建 Cron 触发器的函数并点击函数的名称。

3. 选择 **触发器** 标签页，然后选择 **Cron** 标签页。

4. 点击 **创建Cron触发器**。

5. 在 **创建Cron触发器** 对话框，参考下方表格填写相关配置后，点击 **保存** 完成。



|配置项 |描述 |
|---|---|
|名称 |填写 Cron 触发器的名称。名称规则如下：<br><br><br>* 只能包含英文字母、数字和连字符（\-）。<br><br>* 最多不能超过 128 个字符。 |
|调度类型 |选择 cron 事件被触发的边缘节点。<br><br><br>* **全球**：cron 事件在所有边缘节点被触发。<br><br>* **单点调度**：cron 事件在随机的一个边缘节点触发。 |
|执行时间 |cron 事件被触发的时间。配置后您可以在右侧 **预计执行时间（UTC）**  查看是否符合预期。<br><br><br>* **Cron表达式**：填写 Cron 表达式，参见 [支持的 Cron 表达式](https://docs.byteplus.com/en/docs/18/20481#supportedcron)。<br><br>* **自定义**：选择 **执行频率** 和 **执行时刻**，边缘函数会自动生成对应的 Cron 表达式。 |
|参数 |输入自定义参数。在函数执行时，边缘函数把该参数传递给 [CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-CronEvent-cn)。 |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fc0cc970bc5b8c2e66ffacec39fe61b0.jpeg) </span>


6. 创建 Cron 触发器后，为了确保 Cron 触发器生效，您还需要：

   * 确保 Cron 触发器的状态为 **启用**。

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a90f5dbbd94389af9aa516790d6e9c76.jpeg) </span>

   * 在函数代码中监听 cron 事件。下面的示例代码展示了如何注册一个事件监听器监听 cron 事件并在 cron 事件被触发时调用回调函数实现定时任务。

      ```JavaScript
      // 注册一个事件监听器，监听 cron 事件
      addEventListener('cron', onCron);
      
      // cron 事件被触发时，被调用的回调函数
      async function onCron(event) {
        // 这里可以添加定时任务的具体代码
          return 'this is log';
      }
      ```
      


&nbsp;

<span id="支持的-cron-表达式"></span>
### 支持的 Cron 表达式

Cron 表达式是一个由 5 个字段组成的字符串。这些字段由空格分隔。Cron 表达式默认在 UTC+8:00 时区运行。

**Cron表达式字段说明**


|第一位 |第二位 |第三位 |第四位 |第五位 |
|---|---|---|---|---|
|分钟 |小时 |日 |月 |星期 |


其中，每个字段都有相应的取值范围：


|字段 |取值范围 |允许的特殊字符 |
|---|---|---|
|分钟 |0\-59的整数 |,\-\*/ |
|小时 |0\-23的整数 |,\-\*/ |
|日 |1\-31的整数（需要考虑月的天数） |,\-\*?/L |
|月 |1\-12的整数或不区分大小写的月份 3 个字母缩写（“JAN”、“aug”等） |,\-\*/ |
|星期 |0\-6的整数或不区分大小写的星期 3 个字母缩写（“MON”、“fri”等）。其中0指星期日，1指星期一，以此类推。 |,\-\*?/L |


**特殊字符说明**


|字符 |含义 |说明 |
|---|---|---|
|\*（星号） |表示选择字段中的所有值 |例如，在“分钟”字段中，表示每分钟执行。 |
|,（逗号） |指定多个值 |例如，在“星期”字段中，“MON,WED,FRI”表示“星期一、星期三和星期五”。 |
|\-（连字符） |指定范围 |例如，在“小时”字段中，“10\-12”，表示从“10点到12点”。 |
|?（问号） |表示不确定的值 |与其他指定值组合使用。例如，指定了每月一个特定的日期，但不需要关注该日期是星期几，那么“星期”字段就可以使用?。 |
|/（正斜杠） |表示增加幅度，n/m表示从n开始，每次增加m |例如，在“分钟”字段中，1/3表示从1分钟开始，每隔3分钟执行一次。 |
|#（井号） |表示每个月第几个星期几，只能出现在“星期”这个字段 |与其他指定值组合使用。例如，在“星期”中，5#2表示某月的第二个星期五，5 表示星期五，2 表示第二个。 |
|L（大写英文字母L） |表示最后，只能出现在“日”和“星期“两个字段 |例如，在“日”字段中，表示每月最后一天。在“星期”这个字段使用 5L，表示在最后的一个星期五触发。 |


**示例**


|Cron表达式 |说明 |
|---|---|
|\* \* \* \* \* |每一分钟执行一次 |
|\* /30 \* \* \* \* |每隔30分钟执行一次 |
|\* 23 \* \* \* |每日23时的每一分钟执行 |
|10,20,30 \* \* \* \* |每个小时的10分，20分，30分执行一次 |
|30 7 \* \* MON\-FRI |周一到周五的每天7:30执行一次 |
|0 8 1 \* \* |每月第一天8:00执行一次 |
|0 8 \* JAN\-JUN \* |1月到6月每天8:00执行一次 |


<span id="查看调度记录"></span>
## 查看调度记录

参见以下步骤查看 Cron 触发器的调度记录。目前，您仅能查看最近 6 个月的调度记录。


1. 打开 [函数管理](https://console.byteplus.com/cdn/edge-function/list) 页面。找到您需要查看的函数，点击函数名称。

2. 选择 **触发器** 标签页，然后选择 **Cron** 标签页。

3. 在 **Cron触发器** 列表中，找到您需要查看的 Cron 触发器，点击触发器名称进入 **调度记录** 页面。

4. 在 **调度记录** 页面查看调度记录信息，包含执行表达式、参数、状态、创建时间等信息。您还可以通过 **表达式** 和 **参数** 字段搜索特定记录。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_80b6e66ad2a8ae4c51a50e5bba919270.jpeg) </span>

5. 点击 **查看日志** 查看函数在各节点执行的日志详情。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_38e46cf2dc4ebd09686ca6222ffdcc15.jpeg) </span>


<span id="启动或停用-cron-触发器"></span>
## 启动或停用 Cron 触发器

您可以启用或停用 Cron 触发器。切换 Cron 触发器的状态后立即生效，您无需重新发布函数。


1. 打开 [函数管理](https://console.byteplus.com/cdn/edge-function/list) 页面。找到您需要查看的函数，点击函数名称。

2. 选择 **触发器** 标签页，然后选择 **Cron** 标签页。

3. 找到需要启用或停用的 Cron 触发器，点击 **状态** 列中的开关，切换 Cron 触发器的启用状态。


<span id="删除-cron-触发器"></span>
## 删除 Cron 触发器

如果您不再需要一个 Cron 触发器，可以删除该 Cron 触发器。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Cron 触发器被删除后无法恢复，请谨慎操作。</div>



1. 打开 [函数管理](https://console.byteplus.com/cdn/edge-function/list) 页面。找到您需要删除的函数，点击函数名称。

2. 选择 **触发器** 标签页，然后选择 **Cron** 标签页。

3. 找到需要启用或停用的 Cron 触发器，点击 **操作** 列中的 **删除**。

4. 在弹出的窗口中确认待删除的 Cron 触发器，点击 **确定** 按钮完成操作。
