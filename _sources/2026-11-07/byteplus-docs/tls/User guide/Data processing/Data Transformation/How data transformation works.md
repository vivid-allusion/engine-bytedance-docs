---
title: "How data transformation works"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/how_data_transformation_works"
---

The data transformation feature of the Torch Log Service (TLS) consumes log data in source topics through consumer groups. The data transformation feature automatically compiles a specified Domain Specific Language (DSL) statement and parses it into a data transformation rule. The data transformation feature calls the rule to transform and process log data, then writes the transformed log data to a specified topic through API actions for writing log data. This topic describes how transformation rules and scheduling in transformation tasks work.

<span id="调度原理"></span>
### How scheduling works

The data transformation feature consumes log data from a source topic in streaming mode by collaborating with a consumer group. Each transformation task corresponds to 1 consumer group. Each consumer group starts 1 or more consumers. Consumers transform and process the consumed log data. Each consumer consumes the shards of one or more source topics. The maximum number of consumers that can be started is the same as that of read and write shards of the source topic.

<span id="加工规则原理"></span>
### How transformation rules work

TLS allows you to write transformation rules by using the built\-in functions offered by TLS DSL. Each statement in a transformation rule represents a transformation process. The rule engine executes each transformation process according to the order of your statements. For example, the following statements define 4 processes executed in sequence.

```python
f_set("user_type", "normal")
f_drop("content")
c_if(f_has("inner_user"), f_set("user_source", "inner"))
c_if(op_eq(v("user_city"), "chengdu"), e_output("target"))
```



|Rule |Description |
|---|---|
|Basic logic |TLS executes each statement defined in the rule sequentially and processes each function in the statement sequentially according to semantics. When each function is executed, TLS modifies log events and returns the processed events.<br><br>For example, `f_set("user_type", "normal")` adds the field `user_type` with the value normal to each event. The events received by the next function are the events to which the field `user_type` is added. |
|Conditional judgment |A data transformation rule allows you to set a condition for each process, and an event that meets a condition can start the process of executing a function.<br><br>For the sample statement `c_if(f_has("inner_user"), f_set("user_source", "inner"))`, TLS first verifies whether the field `inner_user` exists. If this field does not exist, TLS does not perform operations. If this field exists, the field `user_source` is added and the field value is set to `inner`. |
|Output |If the specified condition is met, TLS outputs data. Otherwise, TLS does not output data. If no other processing rules exist, the log event is subsequently deleted.<br><br>For the sample statement `c_if(op_eq(v("user_city"), "chengdu"), e_output("target"))`, if the value of the field `user_city` is `chengdu`, TLS outputs the event to the topic with the alias `target`. |
