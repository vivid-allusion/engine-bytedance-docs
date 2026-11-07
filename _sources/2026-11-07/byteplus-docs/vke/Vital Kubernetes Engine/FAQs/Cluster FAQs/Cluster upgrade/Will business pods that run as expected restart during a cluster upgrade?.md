---
title: "Will business pods that run as expected restart during a cluster upgrade?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Do-running-pods-restart-during-a-cluster-upgrade"
---

If your cluster contains workloads with readiness and/or liveness probes, a cluster upgrade might cause pod probe or lifecycle hook failures. It could also trigger in\-place pod restarts. If no readiness or liveness probes are configured, cluster upgrades will not affect workloads. Before upgrading a cluster, check whether the cluster is healthy and whether business traffic is in off\-peak hours. Then, decide whether to upgrade nodes. For more information, see [Best practices for cluster upgrade](https://docs.byteplus.com/en/docs/vke/Cluster-upgrade-best-practices).
