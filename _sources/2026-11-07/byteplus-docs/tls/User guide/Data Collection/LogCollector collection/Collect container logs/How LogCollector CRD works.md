---
title: "How LogCollector CRD works"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/how_logcollector_crd_works"
---

Torch Log Service (TLS) allows you to use custom resource definitions (CRDs) to create collection rules for collecting logs from containers. This topic describes how LogCollector CRD works.

<span id="实现原理"></span>
## Implementation

Beside the console, TLS also allows you to use LogCollector CRDs to quickly create LogCollector collection rules. You can use LogCollector CRDs to define and manage TLS resources in a declarative manner, similar to the method of using CRDs to Kubernetes resources. You can define TLS resources in a YAML file and execute the `kubectl apply` command to create or update resources based on the CRD. TLS then automatically creates or updates log projects, topics, host groups, or collection rules based on the CRD.

The method of using LogCollector CRD to create collection rules is simple and convenient. Using this method, you can create multiple collection rules in batches. However, you must learn how to use the tools and know how to use Kubernetes and CRD. Hence, this method is suitable for advanced Kubernetes users.

<span id="基本概念"></span>
## Terms


|Term |Description |
|---|---|
|LogCollector CRD |LogCollector CRD is a feature offered by the BytePlus TLS for defining Kubernetes resources. The custom resource defined by a LogCollector CRD is known as LogCollector custom resource (CR). After you create and apply a LogCollector CRD in a Kubernetes cluster, the corresponding LogCollector CR is available in the cluster. |
|LogCollector CR |A LogCollector CR is a resource instance defined by a LogCollector CRD. To manage LogCollector collection rules, you can use the kubectl command\-line tool to create, delete, or query LogCollector CRs. For example, you can create a LogCollector CR to create a LogCollector collection rule. |
|LogCollector Controller |The primary role of LogCollector Controller is to monitor the status of LogCollector CRs in Kubernetes clusters and perform corresponding actions. For example, when LogCollector Controller detects a new LogCollector CR, it automatically generates a collection rule based on the definition of the CR; when LogCollector Controller detects that a LogCollector CR is deleted, it automatically deletes the collection rule associated with the CR. |


<span id="实现流程"></span>
## Implementation process

The process of collecting logs from containers according to a LogCollector CRD is as follows:


1. Execute the `kubectl` command to create a LogCollector CRD and a LogCollector CR.

2. LogCollector Controller detects the LogCollector CR.

3. According to the LogCollector CR content, LogCollector Controller automatically sends requests to the TLS server to create log projects, topics, host groups, and collection rules, and automatically binds the collection rules to the host groups.

4. LogCollector periodically sends requests to the TLS server to get the latest collection rules and perform hot loading.

5. LogCollector collects standard outputs or text logs from the specified containers based on the collection rules.

6. LogCollector sends the collected logs to the TLS server.
