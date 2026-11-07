---
title: "alb-ingress-controller"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/alb-ingress-controller-add-on"
---

alb\-ingress\-controller is an Ingress controller add\-on that provides Layer 7 traffic access and routing management capabilities based on Application Load Balancer (ALB). This topic describes how to install and upgrade the alb\-ingress\-controller add\-on and provides relevant considerations.

<span id="2EIpbIXT"></span>
## Add\-on overview

alb\-ingress\-controller is the core Layer 7 (HTTP/HTTPS) traffic gateway add\-on provided by VKE for cloud\-native scenarios. It deeply integrates ALB capabilities, monitors and parses Ingress configurations, and dynamically converts these configurations into ALB forwarding rules. Compared with the native Nginx Ingress, this add\-on delivers superior performance and stability while eliminating the burden of separate O&M on gateway nodes. It provides a robust north\-south application traffic management solution.

As a managed add\-on, it does not run additional Controller Pod workloads in your business cluster or consume computing resources on nodes. After the add\-on is installed, the following CRD is created in your cluster:


|**Resource name** |**Resource type** |**Resource description** |
|---|---|---|
|albinstance |CRD |The CRD resource that manages and monitors the lifecycle of ALB instances. For details, see [Creating ALB Ingresses by using kubectl](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl). |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>


<span id="JCuebjEq"></span>
## Installing add\-ons

This add\-on is mandatory for clusters. It is automatically installed upon cluster creation, requiring no manual installation.

<span id="cwtpvXkA"></span>
## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="WZk4BUqg"></span>
## Related documentation


* [Ingress overview](https://docs.byteplus.com/en/docs/vke/Ingress-overview)

* [ALB Ingress](https://docs.byteplus.com/en/docs/vke/ALB-Ingress)
