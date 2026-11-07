---
title: "Print"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Print"
---

When you need to verify whether the job can operate normally and whether the logic is correct, to reduce external system overhead and avoid interference, you can choose to use some debug\-specific Connectors.

The Print connector is a system\-built debug\-specific results table that outputs job results and prints them to the Stdout (standard output) log.

<span id="b476f663"></span>
## Precautions

Please do not use the Print debug connector in official production tasks as it may affect task performance and has the risk of filling up the disk.

<span id="4ad6cea0"></span>
## DDL Definition

```SQL
CREATE TABLE print_sink (
    name String,
    score INT
 ) WITH (
     'connector' = 'print',
     'print-identifier' = 'out',     --The prefix identifier set for the output data.
     'print-sample-ratio' = '0.01'      --The sampling rate of the output.
 );
```


<span id="0bed4ff0"></span>
## WITH Parameters


|**Parameter** |**Is it mandatory?**  |**Default value** |**Data type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specify the connector in use, here it is the Print connector. |
|print\-identifier |No |(none) |String |Set a prefix for the output data to more accurately distinguish the printed data. |
|print\-sample\-ratio |No<br><br>(Required in Flink 1.11) |0.01 |Double |The output sampling rate ranges from 0 to 1.<br><br>Description<br><br><br>* The output sampling rate is only supported in Flink 1.11 engine version, not in Flink 1.16 version. This parameter must be set in the Flink 1.11 engine version.<br><br>* The sampling rate is set to the default value of 0.01, meaning one out of every 100 pieces of data is output; set to 1 means every data is output. |
|sink.parallelism |No |(none) |Integer |Parallelism. Maintain consistency with the parallelism of upstream and downstream operators.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It's advisable to set the parallelism to <strong>1</strong> to prevent Stdout outputs from each TaskManager.</div><br> |


<span id="16bbac8d"></span>
## Sample Code

```SQL
CREATE TABLE datagen_source (
     siteid INT,
     citycode SMALLINT,
     username VARCHAR,
     pv BIGINT
     )
WITH (
  'connector' = 'datagen',
  'rows-per-second' = '5',                
  'fields.username.length' = '30',            
  'fields.siteid.max' = '1000',   
  'fields.siteid.min' = '100'        
);
CREATE TABLE print_sink (
    siteid INT,
    citycode SMALLINT,
    username VARCHAR,
    pv BIGINT
    )
WITH (
     'connector' = 'print',
     'print-identifier' = 'out',
     'print-sample-ratio' = '0.01'    
);
INSERT INTO print_sink
SELECT * FROM datagen_source;
```


<span id="1f52b532"></span>
## Common Issues

**How to view the results of Print output?** 

Currently, there are two ways to view Print output results: you can view them in the TaskManager running logs in the console; or you can view them in the Stdout output logs on the Flink UI.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you don't see Print output results, it might be because the print sample ratio is set too low.</div>



<Tabs>
<Tab zoneid="w1DiUMLDyU" title="Check in the TaskManager operation logs on the console.">
<TabTitle>Check in the TaskManager operation logs on the console.</TabTitle>

1. In the navigation bar on the left side of the project, select **Task Operations \> Task Management**.

2. Under the **Flink Task** tab, filter for the target task, then click on the task's name.

3. Under the **Logs** tab, select to view **TaskManager** logs, then click on the logs.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bff42d4babe46e090ef832033b9d64a~tplv-goo7wpa0wc-image.image) </span>


4. Search the logs based on the **output data prefix** you set, then review the Print output results.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b3cd626c76a4e5fa6a9e989cb21cf31~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="sDc4PhhvrG" title="Check in the Stdout output logs on the Flink UI.">
<TabTitle>Check in the Stdout output logs on the Flink UI.</TabTitle>

1. Select **Task Operation \> Task Management** from the navigation bar on the left side of the project.

2. Under the **Flink Task** tab, filter for the target task, then click on **Flink UI** behind the target task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bc0925f2a474e82abb07f3d8be727dc~tplv-goo7wpa0wc-image.image) </span>

3. In the Flink UI left navigation bar, select **Task Managers**, then click on logs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1520323c6c4e466e9e948e9e49c3821c~tplv-goo7wpa0wc-image.image) </span>

4. Click on the **Stdout** tab, then search the logs based on the **output data prefix** you set and review the Print output results.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8497ae0207f944c785f41239856439ec~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>
