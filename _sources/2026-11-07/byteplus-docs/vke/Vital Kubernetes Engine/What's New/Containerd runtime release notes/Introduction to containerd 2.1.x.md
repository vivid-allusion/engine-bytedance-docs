---
title: "Introduction to containerd 2.1.x"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Containerd_2-1"
---

VKE supports using containerd 2.1.x on Kubernetes v1.34 or later. This topic describes the main feature updates, deprecated features, and deprecated APIs related to containerd 2.1.x.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For version descriptions and release policies of containerd, see the <a href="https://containerd.io/releases/">official documentation</a>.</div>


<span id="RFVEi6yb"></span>
## **Features**

containerd 2.1 delivers improvements in image security, performance, and stability.


* By default, the experimental feature Node Resource Interface (NRI) is enabled in the containerd configurations, which provides an extension point for more advanced resource management as well as security and monitoring policies.

* By default, Container Device Interface (CDI) is enabled in the containerd configurations, which provides a standardized method of injecting devices into containers and simplifies the use of devices such as GPUs and FPGAs.

* The Sandbox API is supported to enhance the management of the container sandbox throughout the lifecycle.


<span id="Fzj88yuL"></span>
## **Deprecated features and APIs**


* The `registry.configs.tls` parameter has been removed.

* The `registry.auths`, `registry.configs`, and `registry.mirrors` parameters have been deprecated and will be removed in containerd 2.2. You can specify custom configurations for containerd in the VKE console. For details, see [Configuring containerd for node pools](https://docs.byteplus.com/en/docs/vke/Configuring_containerd_for_node_pools).

* Images in the format of Docker Schema 1 are no longer supported, such as `application/vnd.docker.distribution.manifest.v1+json` and `application/vnd.docker.distribution.manifest.v1+prettyjws`. Requests to pull such images will be rejected.

* The `io_uring_*` system calls have been removed from the default Seccomp profile of containerd. Containers no longer have permissions to use `io_uring_*` system calls by default.

* The CRI v1alpha2 API has been removed to align with the evolution of Kubernetes versions. Kubernetes has deprecated this API starting from v1.26.

* The Advanced multi\-layered Unification Filesystem (AUFS) snapshotter has been removed.

* The `[plugins."io.containerd.internal.v1".tracing]` parameter has been removed.
