---
title: "Product specifications"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Product-specifications"
---

This article introduces the positioning, applicable scenarios, capacity specifications, protocols and other information of each specification of file storage PFS.


|Project |100MB/s/TiB_Edition |Performance_Edition |Intelligent_Computing_Edition |
|---|---|---|---|
|Product Positioning |High performance, high IOPS, low latency, suitable for high\-performance computing services. ||Intelligent computing solutions designed to deliver exceptional performance and scalability with ultra\-high performance and ultra\-high IOPS. |
|Business recommendations |HPC high\-performance computing, AI artificial intelligence training/inference, energy exploration, industrial simulation, film and television rendering, life science, meteorological analysis |||
|Maximum I/O bandwidth |**Read/Write** **bandwidth**: min{100\*storage capacity （TiB），20000}MBps |* **Read** **bandwidth**: min{300\*storage capacity （TiB），230000}MBps<br><br>* **Write** **bandwidth**: min{150\*storage capacity （TiB），115000}MBps |* **RDMA mode**<br><br>   * **Read bandwidth**: Min {220 \* Storage capacity (TiB), 3,000,000} MB/s<br><br>   * **Write bandwidth**: Min {100 \* Storage capacity (TiB), 1,400,000} MB/s<br><br>* **VPC mode**<br><br>   * **Read bandwidth**: Min {150 \* Storage capacity (TiB), 2,000,000} MB/s<br><br>   * **Write bandwidth**: Min {100 \* Storage capacity (TiB), 1,400,000} MB/s |
|Maximum IOPS |**Read/Write** **IOPS**: min{10000\*storage capacity （TiB），1800000} |* **Read** **IOPS**: min{4500\*storage capacity （TiB），4000000}<br><br>* **Write** **IOPS**: min{2000\*storage capacity （TiB），1770000} |* **Read IOPS**: Min {3,000 \* Storage capacity (TiB), 45,000,000}<br><br>* **Write IOPS**: Min {1,500 \* Storage capacity (TiB), 22,500,000} |
|Capacity specification |* **Starting** **capacity**: 6TiB<br><br>* **Maximum** **capacity**: 200TiB<br><br>* **Expansion** **step** **size**: 2TiB |* **Starting** **capacity**: 48TiB<br><br>* **Maximum** **capacity**: 960TiB<br><br>* **Expansion** **step** **size**:<br><br>   * When the capacity is in the range of 80\*N+[48,80), the expansion step is 8TiB. <br><br>   * When the capacity = 80\*N, capacity expansion starts from 48TiB.  |* **Starting capacity**: 480 TiB<br><br>* **Maximum capacity**: 19,760 TiB<br><br>* **Expansion step size**:<br><br>   * Capacity at 1,040 \* N + [480,1,040), scale\-out step size 80 TiB<br><br>   * Capacity = 1,040 \* N, scale\-out step size from 480 TiB |
|Protocol |POSIX |||


&nbsp;

&nbsp;
