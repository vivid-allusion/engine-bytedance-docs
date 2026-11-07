---
title: "Data transferring"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/data_transferring"
---

You can use the data transformation feature of Torch Log Service (TLS) to distribute logs from a source topic to multiple target topics according to your rule. This topic describes typical cases in scenarios in which data is replicated and distributed.

In these scenarios, you can distribute logs from 1 source topic to multiple target topics.

For example, an HTTP service may return status codes 200, 400, and 500. After the service running logs are collected by TLS, you want to distribute logs with different status codes to different topics for subsequent analysis.

<span id="原始日志"></span>
#### Logs

```json
[
    {
        "code":"200",
        "msg": "[2022-12-26 16:35:18,456][3c04c53d-ad24-4853-8603-a6e05f192c3b][INFO] URL: http://xxx.com/CreateTask, userID: 12345",
    },
    {
        "code":"400",
        "msg": "[2022-12-26 16:35:19,456][4eef6955-186a-47c6-9943-ec13fbd2f522][INFO] URL: http://xxx.com/CreateTask, userID: 12346",
    },
    {
        "code":"500",
        "msg": "[2022-12-26 16:35:20,456][63281184-098e-4d34-b2da-2dc258e6a3e5][INFO] URL: http://xxx.com/CreateTask, userID: 12347",
    }
]
```


<span id="配置输出目标"></span>
#### Configuring output targets

Configure the following aliases for three target topics: topic\-200, topic\-400, and topic\-500.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7b00ef52b814e3bbc769aee54545dcd~tplv-goo7wpa0wc-image.image) </span>

<span id="dsl-加工规则"></span>
#### Domain Specification Language (DSL) transformation rules

```python
# Distribute different logs with codes 200, 400, and 500 to different target topics.
c_if(op_eq(v("code"), "200"), e_output("topic-200"), op_eq(v("code"), "400"), e_output("topic-400"), op_eq(v("code"), "500"), e_output("topic-500"))
```


<span id="加工结果"></span>
#### Transformation results

The data written to the topic with the alias topic\-200 is as follows:

```json
[
    {
        "code":"200",
        "msg": "[2022-12-26 16:35:18,456][3c04c53d-ad24-4853-8603-a6e05f192c3b][INFO] URL: http://xxx.com/CreateTask, userID: 12345",
    }
]
```


The data written to the topic with the alias topic\-400 is as follows:

```json
[
    {
        "code":"400",
        "msg": "[2022-12-26 16:35:19,456][4eef6955-186a-47c6-9943-ec13fbd2f522][INFO] URL: http://xxx.com/CreateTask, userID: 12346",
    }
]
```


The data written to the topic with the alias topic\-500 is as follows:

```json
[
    {
        "code":"500",
        "msg": "[2022-12-26 16:35:20,456][63281184-098e-4d34-b2da-2dc258e6a3e5][INFO] URL: http://xxx.com/CreateTask, userID: 12347",
    }
]
```
