---
title: "What is the general process for running applications by using VKE?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-is-the-general-process-of-running-applications-using-VKE"
---

The general process for running applications by using VKE is as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed processes and operations, see <a href="https://docs.byteplus.com/en/docs/vke/Quick-guide">Getting started</a>.</div>



1. Write application code.

2. Use a Dockerfile to build an image, which includes the description of the application, dependencies, and the logic for running the application.

3. Run the `docker image build` command on the current Dockerfile.

4. Upload the image to CR.

5. Create a containerized application workload by using the specified image from CR.
