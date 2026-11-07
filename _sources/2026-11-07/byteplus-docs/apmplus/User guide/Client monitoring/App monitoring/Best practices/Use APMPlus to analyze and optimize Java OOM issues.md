---
title: "Use APMPlus to analyze and optimize Java OOM issues"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_APMPlus_to_analyze_and_optimize_Java_OOM_issues"
---

This article describes how to view the crash ratio for Java OOM, and how to analyze leaks and large objects using Hprof files reported during Java OOM, ultimately helping you optimize Java OOM issues.

<span id="7a6394ff"></span>
## Step 1: Analyze Java OOM crash ratio


1. View the Java crash ratio.

   
   |Filter criteria |Value retrieval |
   |---|---|
   |crash type |Java crash, Java startup crash |
   

   As shown in the figure, the overall Java crash ratio is `2.27‰`.

2. View Java OOM crash ratio.

   
   |Filter criteria |Values |
   |---|---|
   |crash type |Java crash, Java startup crash |
   |OOM Status |Yes |
   

   As shown in the figure, the overall Java OOM crash ratio is `1.01‱`. In some applications with severe Java OOM issues, Java OOM can account for as much as 50% of Java crashes.

3. Analyze Java OOM Hprof files.

   1. Configure the OOM analysis sampling rate.

      On the **SDK setting** page, set the metric **OOM analysis sampling rate** of the module **memory optimization** to 100%.

      When a Java OOM occurs, the platform dumps an Hprof file, trims it, and then uploads it. To prevent excessive resource consumption, the APMPlus platform limits the number of Hprof files that can be reported per day to a maximum of several hundred.

   2. Filter Java OOM cases with Hprof files for analysis.

      
      |Filter criteria |Get value |
      |---|---|
      |crash type |Java crash |
      |OOM Status |Yes |
      |Hprof File Existence |Yes |
      

      As shown in the figure, Hprof files were reported for two Java OOM crashes.

   3. Click the Java OOM crash in the exception crash list to enter the details page.


<span id="2afe5258"></span>
## Step 2: View Java OOM Hprof file


1. On the Java OOM crash details page, find the **Hprof file** module.

   
   |Filter criteria |Get values |
   |---|---|
   |Hprof File Existence |Yes |
   

2. Click **view Hprof file** to go to the **single device memory detail** page.

3. View the Hprof file for the memory details of a single device

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The single device memory detail is linked to the Hprof file generated during a Java OOM crash using the Device ID. Caution: Make sure the filtered time range matches the crash time.   </div>
   

   1. Click **Download raw data** to download the Hprof file to your local machine.

      After converting with the hprof\-conv command, you can use memory analysis tools such as MAT to further analyze the memory usage and reference chains of any object.

   2. click **+** Expand to view data such as object leaks and single large objects detected after the APMPlus platform automatically parses the Hprof file.

      As shown in the diagram below, a single large object is displayed, including the object class name, the reference trace of the large object, and the retained size of the large object. The current large object occupies a significant amount of memory, totaling 248 MB. It is necessary to optimize this object to reduce memory usage and thereby address Java out\-of\-memory crash issues.


<span id="f514f420"></span>
## Step 3: Optimize OOM by addressing leak and large object issues

Hprof files reported during a Java OOM crash are automatically parsed and analyzed by the APMPlus platform to identify leaks and large objects. The platform aggregates all detected leaks and large objects to help you identify frequent issues and issues that occupy a large amount of memory.

Aggregated leaks and large objects can be found in the **leak analysis** and **large object** modules on the **memory optimization** page. You can prioritize optimizing and resolving memory leak and large object issues, thereby further addressing Java OutOfMemory (OOM) issues.


1. On the leak analysis page, view the list of aggregated leaks.

2. Enter the leak details page and view the leak stack trace. You can resolve the leak issue based on the stack trace.

3. On the large object analysis page, view the list of all aggregated large objects.

   You can sort by number of times, average size, and total size.

4. Go to the large object details page to view its specific reference chain and held objects.

   You can optimize large object memory usage by breaking reference chains or improving the management of held objects.

5. By analyzing and optimizing the objects held by large objects, you can improve memory usage.

   If large objects of tens or even hundreds of megabytes are found, optimizing them can greatly reduce Java OOM crashes.
