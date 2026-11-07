---
title: "Health check log overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Health-check-log-01"
---

## Introduction​

CLB provides health check log capabilities. Health check logs collect backend server health status change records and deliver them to Torch Log Service (TLS) storage for convenient viewing, cause analysis, and quick issue location.

> **tip**

> Health check logs are generated only when backend server health status changes (i.e., from NORMAL to exception or from exception to NORMAL).

## Log fields

The content in health check logs is presented as key\-value pairs, i.e., {key: value}. The fields included in the log and their specific meanings are as follows:

|Field |Explanation |
|---|---|
|cause |Reason for health check failure. This field appears in the health check log when the health check fails. |
|destination |Health Check destination, that is the backend server. Format is: private IP address of the backend server instance: backend port, for example 192.168.3.114:80. |
|domain |Forwarding rule domain name. This field is not available in the health check logs of Layer 4 listeners. |
|instanceId |CLB instance ID. |
|origion |The source of the health check, namely CLB. Format: [Private IPv4 address of the CLB instance, Private IPv6 address of the CLB instance]:listening port, for example [192.168.2.128,2000:1000:dff:ff01:1:1200:2:928]:80. |
|protocol |The protocol type used in the health check, including TCP, UDP, and HTTP. |
|result |Health check result, which is succeed or failed. |
|time |The time when the Health Check message sending is completed, defaulting to Beijing time, for example: 2021\-08\-10T17:39:29 +08:00. |
|url |Forwarding rule URL. No such field in the health check logs of the layer\-4 listener. |

## Billing description

CLB does not charge for generating health check logs; charges apply for Torch Log Service (TLS).

## Limitations

* Each CLB account supports creating only one log project.

* A log project can create up to 100 log topics.

* A log topic can be associated with up to 60 CLB instances.

* Log projects and topics created through CLB cannot be deleted in the Torch Log Service console; deletion is only supported in the CLB console.

## Usage process

1. [Cross-service authorization and log project creation](https://docs.byteplus.com/en/docs/clb/Implementing-cross-service-authorization-and-creating-a-log-project): grant the relevant TLS operation permissions to the cross\-service role ServiceRoleForClbLogDelivery of CLB. After successful authorization, a log project is automatically created.

2. [Create log topic](https://docs.byteplus.com/en/docs/clb/Creating-a-log-topic): create a log topic to store and manage CLB’s health check logs.

3. [View health check logs](https://docs.byteplus.com/en/docs/clb/Viewing-the-health-check-log): view CLB’s health check logs as needed.
