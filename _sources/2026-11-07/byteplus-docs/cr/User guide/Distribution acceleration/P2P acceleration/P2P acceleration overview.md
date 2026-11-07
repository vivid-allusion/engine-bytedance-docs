---
title: "P2P acceleration overview"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/p2p-acceleration-overview"
---

CR supports P2P acceleration that distributes container images among nodes by leveraging the internal network bandwidth of the worker nodes.

P2P (Peer\-to\-Peer) technology: In a P2P network, after a **node** (Peer) downloads data from the server side (Server), ** it** can also act as a server for other **peers** to download. The P2P acceleration feature of CR utilizes this model, enabling image distribution among nodes directly over the internal bandwidth of the nodes.

When a large\-scale container cluster pulls an image, the network bandwidth of the image registry storage can become a performance bottleneck, causing slow image pulls. CR P2P acceleration addresses this by leveraging the bandwidth of your worker nodes to distribute images among nodes. This significantly reduces the load on the container registry storage, accelerates image pulls, and shortens application deployment time.

P2P acceleration is currently supported in the following scenarios:


* [Using P2P acceleration in VKE](https://docs.byteplus.com/en/docs/cr/use-p2p-acceleration-in-vke)

* [Use P2P acceleration in VCI](https://docs.byteplus.com/en/docs/cr/use-p2p-acceleration-in-vci)
