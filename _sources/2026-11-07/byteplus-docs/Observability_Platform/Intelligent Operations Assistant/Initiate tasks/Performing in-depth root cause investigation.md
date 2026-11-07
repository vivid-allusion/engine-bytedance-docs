---
title: "Performing in-depth root cause investigation"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/deep-investigate-fault-root-cause"
---

This topic describes how to perform root cause analysis through deep investigation.

## Background

Real\-world faults in production environments often span multiple services and systems. Models can easily fall into the trap of shallow investigation, mistaking symptoms for root causes or producing hallucinations and unreliable conclusions. To address this, deep investigation adds an RCA Harness layer outside the model. It first proposes several root cause hypotheses, then collects evidence in parallel to verify or disprove each one. It drills down iteratively in the direction of the strongest evidence until the root cause and supporting evidence are complete before producing an analysis conclusion.

During this process, key conclusions are verified a second time. Each analysis step records the items checked and the items ruled out in detail. The final output is a reviewable investigation report. When evidence is insufficient, possible causes are ranked by confidence level for human judgment.

## Procedure

1. Log in to the [Intelligent O&M platform](https://console.byteplus.com/observe/devops).

2. In the left navigation pane, select an existing session or click **Launch task** to create a new session.

3. In the lower\-left corner of the chat box, select the agent to execute the task, and select **In\-depth investigation**.

4. Describe the fault or issue to investigate using natural language. The intelligent O&M assistant invokes the in\-depth investigation skill for thorough analysis. It then produces an investigation topology and an investigation report.

   The detailed investigation steps are as follows:

   1. **Build investigation context**: Identify the investigation target and retrieve service metadata. No fault evidence is queried in this step.

   2. **Hypothesis\-Testing loop**: Load domain reference documents to construct multiple rounds of hypotheses. Perform parallel evidence collection to verify or disprove each hypothesis. Drill down iteratively in the direction of the strongest evidence until the root cause and evidence are complete.

   3. **Summarize investigation conclusions**: Aggregate the verification results of all hypotheses. Distill the root cause, impact scope, and key evidence into structured conclusions.

   4. **Generate an investigation report**: Automatically generate a readable report based on the investigation conclusions. The report includes the root cause type, root cause summary, root cause details, evidence chain, and remediation recommendations.

## Other operations

* Click a node tab in the investigation topology to view detailed information about the node. Details include context information, hypothesis details, confidence level, hypothesis node evidence, investigation conclusions, and execution recommendations.

* Click **Investigation report** in the upper\-right corner of the session to view the complete analysis report.
