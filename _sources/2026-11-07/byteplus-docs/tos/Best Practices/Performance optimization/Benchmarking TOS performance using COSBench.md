---
title: "Benchmarking TOS performance using COSBench"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/COSBench-user-guide"
---

COSBench (Cloud Object Storage Benchmark) is a benchmarking tool developed by the Intel team in Java to measure object storage service performance. You can use the COSBench tool to test read and write performance for TOS, helping you evaluate the performance of object storage TOS and ensure business stability.

<span id="20651291"></span>
## Operating environment

It is recommended to run the COSBench tool on CentOS 7.6 or higher; other environments may cause unexpected issues.

<span id="69534617"></span>
## Using COSBench


1. Download the [COSBench tool package for TOS](https://tos-tools.tos-cn-beijing.volces.com/third-party/cosbench-tos.zip) and extract it locally.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The COSBench tool cannot directly benchmark TOS. Before use, you need to modify the COSBench source code, then create the TOS COSBench tool package using the modified source code. For details, refer to <a href="https://docs.byteplus.com/docs/tos/COSBench-user-guide#9314c35d">Appendix: Creating the TOS COSBench Tool Package</a>.   </div>
   

2. Run the following command to install COSBench dependencies.

   ```Plain
   sudo yum install nmap-ncat java curl java-1.8.0-openjdk-devel -y
   ```
   

3. Edit the `s3-config-sample.xml` file in the COSBench package to configure the benchmarking task details.

   Example code is as follows:

   ```XML
   <workload name="s3-sample" description="sample benchmark for s3">
   
     <storage type="s3" config="accesskey=***;secretkey=***;endpoint=http://tos-s3-ap-southeast-1.ibytepluses.com;path_style_access=false;" />
   
     <workflow>
   
       <workstage name="init" closuredelay="90">
         <work type="init" workers="1" config="cprefix=examplebucket;containers=r(1,2)" />
       </workstage>
   
       <workstage name="prepare">
         <work type="prepare" workers="10" config="cprefix=examplebucket;containers=r(1,2);objects=r(1,1000);sizes=c(4)KB" />
       </workstage>
   
       <workstage name="main">
         <work name="main" workers="100" runtime="300">
           <operation type="read" ratio="80" config="cprefix=examplebucket;containers=u(1,2);objects=u(1,1000)" />
           <operation type="write" ratio="20" config="cprefix=examplebucket;containers=u(1,2);objects=u(1001,2000);sizes=c(4)KB" />
         </work>
       </workstage>
   
       <workstage name="cleanup">
         <work type="cleanup" workers="10" config="cprefix=examplebucket;containers=r(1,2);objects=r(1,2000)" />
       </workstage>
   
       <workstage name="dispose">
         <work type="dispose" workers="1" config="cprefix=examplebucket;containers=r(1,2)" />
       </workstage>
   
     </workflow>
   
   </workload>
   ```
   

   The stress test task configuration includes 5 phases. You need to configure parameters for each phase, as explained below:

   * init phase: Initializes bucket resources and creates the bucket.

   * prepare phase: Prepares test data by writing data to the bucket. You must specify the size and quantity of objects to write for reading in the main phase. If the main phase does not include read operations, this phase can be skipped.

   * main phase: Defines test behavior, specifying the task duration and operation types.

   * cleanup phase: Cleans test data by deleting uploaded objects.

   * dispose phase: Releases bucket resources by deleting the created bucket.

      Below are some of the parameters:

   
   |Parameter |Description |
   |---|---|
   |accesskey |Access Key ID information for the BytePlus account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed steps to view AK/SK information, see <a href="https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey">Get the Access Key for the current identity</a>.</div><br> |
   |secretkey |Secret Access Key for your BytePlus account. |
   |endpoint |S3 endpoint address. For details, see [regions and access domains](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint). |
   |cprefix |Prefix for the bucket name. |
   |csuffix |Optional suffix for the storage name. |
   |containers |Number and naming rules for buckets, such as setting `containers=r(1,2)`, `cprefix=examplebucket`, which means creating 2 buckets named `examplebucket1` and `examplebucket2`. |
   |objects |Number and naming rules for objects to write in each bucket. |
   |sizes |Set the size of the object. |
   |ratio |The proportion of different operation types in the test, for example, setting the `ratio` for write operations to `80` and the `ratio` for read operations to `20` means that write operations account for 80% of total operations and read operations account for 20% during the test. |
   |runtime |Test duration in seconds. |
   |workers |Number of worker threads for the corresponding stage. |
   

4. Edit the `cosbench-start.sh` file to add the following parameters, adjusting the buffer size and disabling the md5 checksum. The buffer size must be at least as large as the test object size. Set this value according to your actual needs.

   ```Plain
   -Dcom.amazonaws.sdk.s3.defaultStreamBufferSize=104857600 -Dcom.amazonaws.services.s3.disableGetObjectMD5Validation=true -Dcom.amazonaws.services.s3.disablePutObjectMD5Validation=true
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8297b58e1473481f86881c3838baed9c~tplv-goo7wpa0wc-image.image) </span>

5. Run the following command to start the COSBench tool.

   ```Plain
   sudo bash start-all.sh
   ```
   

   On operating systems like Debian, the nc command's probe may fail due to different nmap tool versions, affecting COSBench startup. If you encounter this issue, edit the cosbench\-start.sh file and add the `-q 1` parameter to the `nc` probe command to resolve it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6efdf54341de442bac69bbcd0f1352c7~tplv-goo7wpa0wc-image.image) </span>

6. Run the following command to submit the test task.

   ```Plain
   sudo bash cli.sh submit conf/s3-config-sample.xml
   ```
   

7. Open `http://ip:19088/controller/index.html` in a browser (replace ip with the stress test server's ip) to view the test task status.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29eec773066f4db0b9c2249dc8db64b2~tplv-goo7wpa0wc-image.image) </span>

8. After completing the test, run the following command to stop the COSBench tool.

   ```Plain
   sudo bash stop-all.sh
   ```
   


<span id="9314c35d"></span>
## Appendix: Creating the TOS COSBench Tool Package

The COSBench tool cannot be used directly for stress testing TOS. Before use, you need to modify the COSBench source code and then create the TOS COSBench tool package using the modified source.

<span id="4faeb667"></span>
### Environment preparation

This article demonstrates creating the TOS COSBench tool package in the following environment for your reference.


* Operating system: macOS x86_64

* IDE version: Eclipse 4.15

* JDK version: 1.8


<span id="250dc0d6"></span>
### Procedure


1. Download the COSBench source code archive from the [GitHub website](https://github.com/intel-cloud/cosbench/releases/tag/v0.4.2.c4) and extract it locally.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12624d1f02144592baae5fe89354b88f~tplv-goo7wpa0wc-image.image) </span>

2. Import the COSBench source code into Eclipse.

   1. In Eclipse, click **File \> Import...**   **\> Existing Projects into Workspace**.

   2. In the **Import Projects** dialog, select the dev directory in the COSBench source code and click **Finish**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74675bcae13c4899b3850c612e1060d7~tplv-goo7wpa0wc-image.image) </span>

   3. Click **Eclipse \> Settings...**   **\> Plug\-in Development \> Target Platform**.

   4. In the **Target Platform** dialog, click **Add...** .

   5. In the **Target Content** dialog, customize the platform name at **Name**.

   6. Click **Add...**   **\> Directory**, sequentially add the main, osgi, and osgi/libs folders from the COSBench source dist directory, then click **Finish**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fc81ce2bc2b48d28a361189b0ed8910~tplv-goo7wpa0wc-image.image) </span>

   7. In the **Target Platform** dialog, select the custom platform and click **Apply and Close**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13d7a7e5da3e46369fadf07608b8195d~tplv-goo7wpa0wc-image.image) </span>

3. Configure the S3Storage.java file.

   1. Locate the S3Storage.java file in the cosbench\-s3 folder.

   2. Modify the value of `clientConf.withSignerOverride` in the S3Storage.java file to `AWSS3V4SignerType` to specify using the AWS V4 signer. The modified example is as follows:

   ```Plain
   clientConf.withSignerOverride("AWSS3V4SignerType");
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84d6b8a498484c1bb3c003058e1c37dc~tplv-goo7wpa0wc-image.image) </span>

   3. Modify the value of `client.setS3ClientOptions` in the S3Storage.java file to add `disableChunkedEncoding` and disable chunked encoding. The modified example is as follows:

   ```Plain
   client.setS3ClientOptions(new S3ClientOptions().withPathStyleAccess(parms.getBoolean(PATH_STYLE_ACCESS_KEY)).disableChunkedEncoding());
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb689d32bc064ec5823d0b0047178601~tplv-goo7wpa0wc-image.image) </span>

   4. Change the value of `client.putObject` in the S3Storage.java file to enable uploading objects using BufferedInputStream. The modified example is as follows:

   ```Plain
   client.putObject(container, object, new BufferedInputStream(data), metadata);
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90457849f2e04951bb6f39c20f326078~tplv-goo7wpa0wc-image.image) </span>

4. Generate the COSBench toolkit.

   1. In Eclipse, click **File \> Export...**   **\> Plug\-in Development \> Deployable plugins and fragments**.

   2. In the **Deployable plug\-ins and fragments** dialog, click **Select All** and set **Directory** to the dist/osgi directory in the COSBench source code.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8956402c9b04ae6a57c89925b3d220d~tplv-goo7wpa0wc-image.image) </span>

   3. Click the **Options** tab, select **Use class files compiled in the workspace**, then click **Finish**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bbedaaf2a574c2aa4cbaa748d244839~tplv-goo7wpa0wc-image.image) </span>

5. In the COSBench source directory, run the following command to create the delivery package.

   ```Plain
   sh pack.sh cosbench-tos
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d230c1408964f5b98cfe0929b669b51~tplv-goo7wpa0wc-image.image) </span>

6. Execute the following command to package the COSBench toolkit.

   ```Plain
   zip -r -X cosbench-tos.zip cosbench-tos
   ```
