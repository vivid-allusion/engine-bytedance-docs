---
title: "Will business traffic be interrupted during the cluster control plane upgrade?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Does-upgrading-the-control-plane-of-a-cluster-cause-business-traffic-interruption"
---

Traffic will not be interrupted for a long period of time. However, brief interruptions may occur before reconnection, typically lasting a few seconds.

The upgrade of the control plane mainly involves the upgrade of add\-ons, such as etcd, kube\-apiserver, kube\-scheduler, and kube\-controller\-manager. The rolling upgrade is performed. In this way, the existing pods will be deleted only if new pods start as expected. In scenarios where custom add\-ons or system add\-ons connect to kube\-apiserver, transient traffic interruption may occur because kube\-apiserver uses a persistent‑connection mechanism. In this case, a quick retry may be required.
