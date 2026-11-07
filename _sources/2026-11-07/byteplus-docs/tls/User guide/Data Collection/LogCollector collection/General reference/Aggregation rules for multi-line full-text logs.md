---
title: "Aggregation rules for multi-line full-text logs"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Aggregation-rules-for-multi-line-full-text-logs"
---

This topic introduces the aggregation rules and relevant examples when collecting multi\-line logs through the multi\-line full\-text mode of LogCollector.

<span id="53e752ea"></span>
## Aggregation rules

The aggregation rules of the multi\-line full\-text mode of LogCollector are as follows:


* When a certain line of log read exactly matches the first\-line regular expression, if:

   * If there is currently a multi\-line log block, LogCollector will send this multi\-line log block, then create a new multi\-line log block, and use the currently read line of log as the start of the new log block.

   * If there is no multi\-line log block currently, LogCollector will create a new multi\-line log block and use the currently read line of log as the start of the new log block.

* When a certain line of log read does not exactly match the first\-line regular expression, if:

   * If there is currently a multi\-line log block, LogCollector will append the currently read line of log to the end of this multi\-line log block.

   * If there is no multi\-line log block currently, LogCollector will directly send this line of log.

* EOF (end of file) handling:

   If the end\-of\-file symbol (EOF) is read and EOF is read continuously for 5 seconds, then LogCollector will send the existing multi\-line log blocks.


<span id="fffea3f3"></span>
## Typical scenario example


* First\-line regular expression

   ```Plain
   xxx.*
   ```
   

* User\-side original logs

   ```Plain
   xxx1
   yyy11
   yyy12
   xxx2
   yyy21
   yyy22
   ```
   

* The logs finally sent

   ```Plain
   xxx1\nyyy11\nyyy12
   xxx2\nyyy21\nyyy22
   ```
   


The log aggregation steps are as follows:


1. Read the first line log `xxx1`, since it exactly matches the first\-line regular expression `xxx.*` *,*  LogCollector will create a new multi\-line log block and use `xxx1` as the beginning of this log block.

2. Read the second line log `yyy11`, since it does not exactly match the first\-line regular expression `xxx.*`, LogCollector will append the log `yyy11` to the end of the current multi\-line log block.

3. Read the third line log `yyy12`, since it does not exactly match the first\-line regular expression `xxx.*`, LogCollector will append the log `yyy12` to the end of the current multi\-line log block.

4. Read the fourth line log `xxx2`, since it exactly matches the first\-line regular expression `xxx.*`, LogCollector will send the current multi\-line log block `xxx1\ nyyy11\ nyyy12`, and then create a new multi\-line log block, and `xxx2`as the beginning of the new multi\-line log block.

5. Read the fifth line log `yyy21`, since it does not exactly match the first line of regular expression `xxx.*`, LogCollector appends the log `yyy21` to the end of the current multi\-line log block.

6. Read the sixth line log `yy22`, since it does not exactly match the first\-line regular expression `xxx.*`, LogCollector will append the log `yyy22` to the end of the current multi\-line log block.

7. After continuously reading the EOF for 5 seconds, LogCollector sends the current multi\-line log block `xxx2\nyyy21\nyyy22`.


<span id="6b3a0030"></span>
## Special scenario example

<span id="718b96c7"></span>
### Single\-line and multi\-line logs in one file


* First\-line regular expression

   ```Plain
   xxx.*
   ```
   

* User\-side original logs

   ```Plain
   yyy11
   yyy12
   yyy13
   xxx2
   yyy21
   yyy22
   ```
   

* The logs finally sent

   ```Plain
   yyy11
   yyy12
   yyy13
   xxx2\nyyy21\nyyy22
   ```
   


The multi\-row log aggregation rules are as follows:


1. Read the first line log `yyy11`, since it does not exactly match the first\-line regular expression `xxx.*` and there is no multi\-line log block at present. LogCollector will directly send the log `yyy11`.

2. Read the second line log `yy12`, since it does not exactly match the first\-line regular expression `xxx.*` and there is currently no multi\-line log block. LogCollector will send log `yyy12`directly.

3. Read the third line log `line yyy13`, since it does not exactly match the first\-line regular expression `xxx.*`, and there is currently no multi\-line log block. LogCollector will directly send the log `yy13`.

4. The fourth line log `xxx2`, since it exactly matches the first\-line regular expression `xxx.*`, LogCollector will create a new multi\-line log block, and log `xxx2` as the beginning of the new multi\-line log block.

5. Read the fifth line log `yy21`, since it does not exactly match the first\-line regular expression `xxx.*`, LogCollector will append log `yyy21` to the end of the current multi\-line log block.

6. Read the sixth line log `yy22`, since it does not exactly match the first\-line regular expression `xxx.*`, LogCollector will append log `yyy22` to the end of the current multi\-line log block.

7. After continuously reading EOF for 5 seconds, LogCollector sends the current multi\-line log block `xxx2\nyyy21\nyyy22`.


<span id="f9a8e340"></span>
### The size of the multi\-line log exceeds 512 KB.


* First\-line regular expression

   ```Plain
   xxx.*
   ```
   

* User\-side original logs

   ```Plain
   xxx1
   yyy11
   ……    // N lines of logs are omitted here.
   yyy12 // Among them, 1 is the 512KB-th byte of the multi-line log, which means that the characters following 1 will be truncated during collection.
   yyy13
   yyy14
   ```
   

* The logs finally sent

   ```Plain
   xxx1\nyyy11\n……\nyyy1
   2
   yyy13
   yyy14
   ```
   


The multiline log aggregation rules are as follows:


1. Read the first line log `xxx1`, since it exactly matches the first line regular expression `xxx.*`, LogCollector will create a new multi\-line log block, and use `xxx1`as the beginning of the new multi\-line log block.

2. Read the second line log `yyy11`, since it does not exactly match the first\-line regular expression `xxx.*`, LogCollector will append the log `yyy11` to the end of the current multi\-line log block.

3. The collection operation of the N\-line log omitted in the middle is the same as above.

4. Read the log `yy12`, since it does not exactly match the first\-line regular expression `xxx.*`, LogCollector will append the log `yyy12` to the end of the current multi\-line log block. At this time, the size of the multi\-line log block exceeds 512KB, so start truncating from `1` of `yyy12` and send the log block `xxx1\ nyyy11\ n...\ nyyy1`, and then send the log block `2`.

5. Read the log `yy13`, since it does not exactly match the first\-line regular expression `xxx.*`, and there is currently no multi\-line log block. LogCollector will send the log `yyy13`directly.

6. Read the log `yy14`, since it does not exactly match the first\-line of the regular expression `xxx.*`, and there is currently no multi\-line log block, LogCollector will send the log `yy14`directly.


<span id="897ac802"></span>
### The disk\-writing interval of multi\-line logs exceeds 5 seconds


* First\-line regular expression

   ```Plain
   xxx.*
   ```
   

* User\-side original logs

   ```Plain
   xxx1
   yyy11
   // After 5s
   yyy12
   yyy13
   ```
   

* The logs finally sent

   ```Plain
   xxx1\nyyy11
   yyy12
   yyy13
   ```
   


The multi\-line log aggregation rules are as follows:


1. Read the log `xxx1`, since it exactly matches the first\-line regular expression `xxx.*`, LogCollector will create a new multi\-line log block, and `xxx1` as the beginning of the new multi\-line log block.

2. Read the log `yy11`, since it does not exactly match the first\-line regular expression `xxx.*`, LogCollector will append the log `yyy11` to the end of the current multi\-line log block.

3. EOF is still read for 5 seconds, so LogCollector will send the current multi\-line log block `xxx1\ nyyy11`.

4. Read the log `yy12`, since it does not exactly match the first\-line regular expression `xxx.*`, and there is currently no multi\-line log block. LogCollector will send the log `yyy12`directly.

5. Read the log `yy13`, since it does not exactly match the first\-line regular expression `xxx.*`, and there is currently no multi\-line log block. LogCollector will send the log `yyy13`directly.
