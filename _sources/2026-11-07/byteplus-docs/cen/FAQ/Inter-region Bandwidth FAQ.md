---
title: "Inter-region Bandwidth FAQ"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-faq"
---

## Is the upstream and downstream rate of inter\-region bandwidth configured in Cloud Enterprise Network (CEN) the same?

Yes. The inter\-region bandwidth configured in CEN does not distinguish between region directions, so the upstream and downstream rates of inter\-region bandwidth are the same.

## Can the inter\-region bandwidth of CEN be modified? How?

Yes, supported. The inter\-region bandwidth of CEN can be increased or decreased based on actual business needs. When increasing the bandwidth, ensure that the new bandwidth does not exceed the allocable bandwidth of the associated bandwidth package. For detailed procedure, see [Modifying Inter-region Bandwidth](https://docs.byteplus.com/en/docs/cen/Inter-region-bandwidth-02).

## Why is the bandwidth measured using the `iperf` command much lower than the allocated bandwidth?

This is because you are testing single\-threaded traffic, which cannot reach the maximum bandwidth limit. We recommend using multi\-threaded concurrent traffic for testing. Example of a multi\-threaded traffic test command:

```Plain Text
iperf -c 192.168.1.10 -p 80 -u -b 100m -P 10
```

Parameter explanations:

* \-c: Starts iperf in client mode. 192.168.1.10 is the IP address of the server.

* \-p: Specifies the port. 80 is the port number.

* \-u: Uses a UDP connection.

* \-b: Sets the bandwidth per thread. Total bandwidth = Bandwidth per thread × Number of threads. 100m is the bandwidth size, which is typically set to the allocated bandwidth.

* \-P: Specifies the number of threads.

If the bandwidth measured with multi\-threaded concurrent traffic is still much lower than the allocated bandwidth, please contact your account manager.
