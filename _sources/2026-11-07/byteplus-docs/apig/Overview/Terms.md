---
title: "Terms"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Terms-1"
---

This article summarizes the glossary terms involved in using the API gateway to facilitate quick queries and understanding.


|Terms |Description |
|---|---|
|Instance |An instance is equivalent to an API gateway. The instance is responsible for defining the specifications and deployment location of the gateway, and providing the necessary resources such as public network IP, private network IP, public network exit, computing, and storage for handling APIs. |
|Service |Service is a set of Ingress exposed to the external, used to distinguish the source and protocol of traffic, achieving business, environmental, and logical tenant isolation. Each service provides an independent Domain name to manage API access business by domain dimension. The lifecycle of a service depends on its instance. |
|Ingress |Ingress belongs to the Service; by configuring the Service's Ingress rules, requests that comply with the rules are forwarded to the designated Upstream. |
|Upstream |Upstream is the abstraction of the backend. You can abstract backend applications with the same features into an Upstream, achieving decoupling of routing and backend applications, and better supporting scenarios such as canary releases and multi\-version management of backend applications. |
|Backend |The backend is the backend application you deploy. The API gateway currently supports connecting to function services, Elastic Compute Service, and Vital Kubernetes Engine as backend types. |
|Canary release |Canary release, also known as a gray release, is a package update strategy that smoothly transitions from an old version to a new version. This package update strategy first publishes a new version, splitting a small portion of the live traffic from the old version to the new version to test the new version's actual performance in the production environment. After the new version performs as expected in the environment, progressively increase the allocation ratio of traffic until it completely replaces the old version. |
