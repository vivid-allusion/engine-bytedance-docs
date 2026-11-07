---
title: "How long does it take to upgrade a cluster?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-long-does-it-take-to-upgrade-a-cluster"
---

The control plane upgrade mainly involves the upgrade of managed add\-ons, such as etcd, kube\-apiserver, kube\-scheduler, and kube\-controller\-manager, which takes about 5 to 10 minutes. The data plane upgrade mainly involves the modification of node kernel parameters and the upgrade of the containerd add\-on and the kubelet add\-on. The upgrade of a single node takes up to 3 minutes. You can upgrade up to 10 nodes at the same time.
