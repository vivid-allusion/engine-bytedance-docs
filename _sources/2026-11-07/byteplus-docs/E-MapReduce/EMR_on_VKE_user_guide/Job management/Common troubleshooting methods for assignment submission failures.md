---
title: "Common troubleshooting methods for assignment submission failures"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Common_troubleshooting_methods_for_assignment_submission_failures"
---

This document is intended to provide common troubleshooting approaches for failures when submitting SparkApplication jobs and RayJob jobs.

<span id="b2940769"></span>
# Errors caused by job YAML fields

When submitting a job field that is not yet supported (as shown below).

```JSON
rayClusterSpec:
  demoNotExistsKey: "key1"
  rayVersion: '2.9.3' # should match the Ray version in the image of the containers
  # Ray head pod template
  headGroupSpec:
```


The following error may occur:

```JSON
error: error validating "ray/ray-job-v1.0.0.yaml": error validating data: ValidationError(RayJob.spec.rayClusterSpec): unknown field "demoNotExistsKey" in io.ray.v1.RayJob.spec.rayClusterSpec; if you choose to ignore these errors, turn validation off with --validate=false
```


The above error indicates that your job YAML file contains fields that are not yet supported by the CRD. You can identify the unsupported field names based on the error message.

SparkApplication and RayJob are both CRD resources. Supported fields can be obtained by viewing the CRD details.

<span id="ce763816"></span>
# Job not executed after submission

After a job is submitted correctly, if there is no output for an extended period, you can go to the VKE console to check the actual execution status of the corresponding job Pod. You can first observe the status of the job Pod to see if there are indications such as "ImagePullBackOff" or "PENDING". If these appear, it means the container has not started, as shown below:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbc75c31357d4f11afa38d45a98fbe34~tplv-goo7wpa0wc-image.image" width="2710px" /></div>


When an abnormal status occurs, you can go to the corresponding Pod page to view the event information and troubleshoot the issue.

Common solutions are as follows:


1. Job encounters ImagePullBackOff: This is usually caused by using a custom image without configuring a Secret. You can configure the image repository pull secret according to the Kubernetes standard procedure and then retry.

2. Job encounters Pending: This is usually due to insufficient resources. You can wait for preceding jobs to complete and then observe whether the Pod starts normally, or directly scale up the node pool so that the Pod can be scheduled properly.
