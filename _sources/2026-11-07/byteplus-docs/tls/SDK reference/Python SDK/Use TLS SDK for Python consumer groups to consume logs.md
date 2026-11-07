---
title: "Use TLS SDK for Python consumer groups to consume logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/use_tle_sdk_for_python_consumer_groups_to_consume_logs"
---

Torch Log Service (TLS) SDKs offer the ConsumerGroup feature that allows you to consume log data using consumer groups. This topic describes how to use TLS SDK for Python consumer groups to consume logs.

<span id="749e52ee"></span>
## Before you begin


* Install TLS SDK for Java. For more information, refer to [Install TLS SDK for Java](https://docs.byteplus.com/docs/tls/install_tls_sdk_for_java).

* Add environment variables such as `VOLCENGINE_ACCESS_KEY_ID`. For information on how to configure environment variables, refer to [Configure identity authentication](https://docs.byteplus.com/docs/tls/configuring_identity_authentication).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard\-coded AccessKey information leads to data security risks.   </div>
   

<span id="5eaf4254"></span>
## Configuration description

When you use consumer groups to consume data, TLS automatically allocates shards to balance the consumption capability and progress of each consumer group. Therefore, you do not need to consider internal scheduling, load balancing among consumers, or failovers that may occur. Just focus on your business logic.

For information on the relevant terms, refer to [Use ConsumeLogs to consume logs](https://docs.byteplus.com/docs/tls/use_consumelogs_to_consume_logs).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">TLS SDK consumer groups support automatically retrying failed requests and reporting the checkpoints. Therefore, you only need to focus on the business logic of handling LogGroupList generated after log data is consumed each time.</div>


In TLS SDK for Python, the ConsumerConfig constructor returns the configuration of a consumer group. In the configuration, specify basic information such as the endpoint, Region, AccessKey ID, and AccessKey secret, as well as the project ID, topic ID list, consumer group name, and consumer name.

In addition, you can set other ConsumerConfig parameters as needed. The following table describes the ConsumerConfig parameters:


|Parameter |Type |Example |Description |
|---|---|---|---|
|max_fetch_log_group_count |int |100 |The maximum number of log groups when the consumer consumes log data each time. Default value: 100. Maximum value: 1000. |
|heartbeat_interval_in_second |int |20 |The interval at which the consumer reports a heartbeat. Unit: seconds. |
|data_fetch_interval_in_millisecond |int |200 |The interval at which the consumer consumes log data. Unit: milliseconds. |
|flush_checkpoint_interval_in_second |int |5 |The interval at which the consumer uploads the consumption progress. Unit: seconds. |
|consume_from |str |begin |The default consumer offset when the consumption starts. The value is consistent with that of From in the DescribeCursor API action. The parameter takes effect only when the consumer has not uploaded consumer offsets. |
|ordered_consume |bool |False |Whether to enable consumption in sequence. If enabled, the consumer consumes log data based on the parent\-child relationship of shard splitting.<br><br>For example, Shard 0 is split into Shard 1 and Shard 2, while Shard 1 is then split into Shard 3 and Shard 4. If the feature is enabled, log data is consumed in the sequence of (Shard 0) \> (Shard 1, Shard 2) \> (Shard 2, Shard 3, Shard 4). |


<span id="ad7d0d71"></span>
## Sample code

The following sample code demonstrates how to use TLS SDK for Python to create a consumer group and consumers to consume logs.

```Python
# coding=utf-8
from __future__ import absolute_import
from __future__ import division
from __future__ import print_function

import os
import time

from volcengine.tls.TLSService import TLSService
from volcengine.tls.consumer.consumer import TLSConsumer, LogProcessor
from volcengine.tls.consumer.consumer_model import ConsumerConfig
from volcengine.tls.log_pb2 import LogGroupList


# Implement a class that inherits LogProcessor. Implement a process method to handle LogGroupList generated after log data is consumed each time as needed.
# The following sample code prints each log entry.
class MyLogProcessor(LogProcessor):
    def process(self, topic_id: str, shard_id: int, log_group_list: LogGroupList):
        print(topic_id + " --- " + str(shard_id))

        count = 0

        for log_group in log_group_list.log_groups:
            for log in log_group.logs:
                count += 1
                print("*** Count = {} ***".format(count))

                for content in log.contents:
                    print("{}: {}".format(content.key, content.value))
                print()


if __name__ == "__main__": 
    # When you initialize the client, we recommend that you use environment variables to dynamically get identity authentication information such as BytePlus AccessKey. Otherwise, hard-coded AccessKey information leads to data security risks.  
    # If you use Security Token Service (STS), use a temporary AccessKey ID and AccessKey secret, and set VOLCENGINE_TOKEN. If you do not use STS, leave VOLCENGINE_TOKEN empty. 
    endpoint = os.environ["VOLCENGINE_ENDPOINT"] 
    region = os.environ["VOLCENGINE_REGION"] 
    access_key_id = os.environ["VOLCENGINE_ACCESS_KEY_ID"] 
    access_key_secret = os.environ["VOLCENGINE_ACCESS_KEY_SECRET"]

    # Instantiate the TLS client.
    tls_service = TLSService(endpoint, access_key_id, access_key_secret, region)

    # Set the required parameters of the consumer group. The ConsumerConfig constructor presets some default parameters, which can be changed as needed.
    consumer_config = ConsumerConfig(project_id="your-project-id",,
                                     consumer_group_name="python-consumer-group",
                                     consumer_name="python-consumer",
                                     topic_id_list=["your-topic-id"])
    tls_consumer = TLSConsumer(consumer_config, tls_service, MyLogProcessor())

    # Call tls_consumer.start() to consume log data continuously.
    tls_consumer.start()

    # Call tls_consumer.stop() to end consumption by the consumer group.
    time.sleep(10)
    tls_consumer.stop()
```
