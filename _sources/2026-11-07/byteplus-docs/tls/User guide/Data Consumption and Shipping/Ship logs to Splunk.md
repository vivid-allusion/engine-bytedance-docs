---
title: "Ship logs to Splunk"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Ship_logs_to_Splunk"
---

This document introduces the basic concepts and sample code for delivering Syslog logs to Splunk through the Log Service.

<span id="B7CJB07C"></span>
## Feature overview

The Log Service provides the capability to deliver Syslog log data to Splunk. After consuming data through the Log Service API interface ConsumeLogs, the data is parsed into the corresponding Syslog format and then written to Splunk.

For calling the ConsumeLogs interface via the Log Service SDK, please refer to [Consuming Logs through ConsumeLogs](https://docs.byteplus.com/en/docs/tls/use_consumelogs_to_consume_logs).

<span id="ju4fAyrn"></span>
## Precautions


* Currently supports Syslog under RFC5424 and RFC3164 standards.

* When sending Syslog log data to the Splunk platform via TCP protocol, Splunk does not strip the priority information originally included in the event, retaining the priority information included in the Syslog data (such as the priority defined by the `PRI` field). For details, please refer to the [official Splunk website](https://help.splunk.com/en/splunk-enterprise/get-started/get-data-in/9.4/get-data-from-network-sources/how-the-splunk-platform-handles-syslog-data-over-the-udp-network-protocol).

* A available Splunk endpoint must be prepared in advance to receive data.


<span id="oWbx46Oo"></span>
## Example code

Refer to the following example to get the consumer group configuration, configure the log service topic, and set up the syslog client. Using RFC5424 Syslog as an example, it demonstrates printing each key\-value pair of every consumed log entry one by one.

```Go
package tls

import (
        "context"
        "crypto/tls"
        "fmt"
        tlsConsumer "github.com/volcengine/volc-sdk-golang/service/tls/consumer"
        "github.com/volcengine/volc-sdk-golang/service/tls/pb"
        "github.com/volcengine/volc-sdk-golang/service/tls/siem"
        "log"
        "os"
        "strconv"
        "time"
)

func ConsumerLogsToSyslogClient() error {
        // Get default consumer configuration.
        consumerCfg := tlsConsumer.GetDefaultConsumerConfig()
        // Configure basic information including Endpoint, Region, AccessKeyID, AccessKeySecret.
        consumerCfg.Endpoint = os.Getenv("VOLCENGINE_ENDPOINT")
        consumerCfg.Region = os.Getenv("VOLCENGINE_REGION")
        consumerCfg.AccessKeyID = os.Getenv("VOLCENGINE_ACCESS_KEY_ID")
        consumerCfg.AccessKeySecret = os.Getenv("VOLCENGINE_ACCESS_KEY_SECRET")
        // Configure project ID and topic ID list.
        consumerCfg.ProjectID = "<YOUR-PROJECT-ID>"
        consumerCfg.TopicIDList = []string{"<YOUR-TOPIC-ID>"}
        // Configure consumer group name (By default, if no consumer group is created, SDK creates a consumer group with a specified name for you).
        consumerCfg.ConsumerGroupName = "<CONSUMER-GROUP-NAME>"
        // Configure consumer name(Different consumer names in the same consumer group must be unique).
        consumerCfg.ConsumerName = "<CONSUMER_NAME>"

        // Set syslog client
        syslogClient := siem.NewSyslogClient()
        // Set client configuration.
        syslogClient.Host = os.Getenv("SPLUNK_HOST")
        syslogClient.Port, _ = strconv.Atoi(os.Getenv("SPLUNK_PORT_UDP"))
        // Configure this parameter when using SSL authentication. Note: the "tls" here is not tls from torch log service.
        syslogClient.SslSettings = &tls.Config{}

        // Start client.
        err := syslogClient.Connect()
        if err != nil {
                log.Fatalf("syslog client connect error %v:", err)
        }

        // Define the log consumption function. You can complete log consumption function for processing LogGroupList based on your business needs.
        // Taking RFC5424 syslog as an example, the following is a code example of printing each key-value pair of each consumed log one by one.
        var handleLogsFunc = func(topicID string, shardID int, l *pb.LogGroupList) {
                for _, logGroup := range l.LogGroups {
                        for _, tlsLog := range logGroup.Logs {

                                // If it is RFC3164, use NewSyslogFormatRFC3164.
                                syslogRFC5424 := siem.NewSyslogFormatRFC5424()

                                for _, content := range tlsLog.Contents {
                                        switch content.Key {
                                        // Replace sample field with actual field.
                                        case "pri":
                                                syslogRFC5424.Priority = content.Value
                                        // Replace sample field with actual field.
                                        case "version":
                                                syslogRFC5424.Version = content.Value
                                        // Replace sample field with actual field.
                                        case "timestamp":
                                                syslogRFC5424.Timestamp, _ = time.Parse(time.RFC3339, content.Value)
                                        // Replace sample field with actual field.
                                        case "hostname":
                                                syslogRFC5424.Hostname = content.Value
                                        // Replace sample field with actual field.
                                        case "appName":
                                                syslogRFC5424.AppName = content.Value
                                        // Replace sample field with actual field.
                                        case "pid":
                                                syslogRFC5424.Pid = content.Value
                                        // Replace sample field with actual field.
                                        case "msgId":
                                                syslogRFC5424.MsgId = content.Value
                                        // Replace sample field with actual field.
                                        case "message":
                                                syslogRFC5424.Message = content.Value
                                        }
                                }

                                syslogRFC5424Format, err := syslogRFC5424.FormatSyslogMessageWithRFC5424()
                                if err != nil {
                                        // Process formatting errors.
                                        log.Printf("NOTICE: syslogRFC5424.FormatSyslogMessageWithRFC5424() failed: %v", err)
                                }

                                // If sending fails, it actively retries sending once.
                                err = syslogClient.Send(syslogRFC5424Format)
                                if err != nil {
                                        // Process the logic of failed sending.
                                        return
                                }

                                fmt.Println("Sent successfully.")
                        }
                }
        }

        tlsConsumerIns, err := tlsConsumer.NewConsumer(context.TODO(), consumerCfg, handleLogsFunc)
        if err != nil {
                log.Fatalf("NewConsumer error %v", err)
        }

        // Start consumer.
        if err := tlsConsumerIns.Start(); err != nil {
                return fmt.Errorf("start consumer failed, error is %v", err)
        }

        // Control consumption exit based on your actual business.
        time.Sleep(300 * time.Second)

        _ = syslogClient.Close()
        tlsConsumerIns.Stop()

        return nil
}
```
