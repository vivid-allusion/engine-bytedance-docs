---
title: "Handling Remote Procedure Calls (RPCs) correctly"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/resources-handling_rpcs_correctly"
---

This section provides answers to frequently\-asked questions about Remote Procedure Calls (RPCs) correctly.

<span id="How do I troubleshoot for an RPC?"></span>
# How do I troubleshoot for an RPC?

To troubleshoot when calling an RPC, you should first check the RPC response code. If the response code is a value other than 200, then the RPC failed due to network failure. However, even if the code is 200, it does not mean that the call succeeded. You should continue to look for the XXXResponse.status.code for more details. Any non\-zero value indicates detailed failures. You can check XXXResponse.status.message for the actual reasons.

<span id="How do I understand the error codes returned by an RPC?"></span>
# How do I understand the error codes returned by an RPC?

We mostly use standard HTTPS error codes, with a few exceptions. For more details, refer to Error codes.

<span id="How do I understand the HTTPS headers in an RPC?"></span>
# How do I understand the HTTPS headers in an RPC?

We require you to add a few HTTPS headers. For more details, refer to HTTPS header. For a complete example, refer to Code samples.

<span id="When should I try calling an RPC again?"></span>
# When should I try calling an RPC again?

Generally, for all 4XX error codes, you should retry with a different request or with an exponential backoff. Meanwhile, a 500 error code indicates that the failure is persistent. If it happens frequently enough, reach out to the BytePlus Recommend team for help.
