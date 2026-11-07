---
title: "Troubleshooting and solution for high disk load of ECS instance with Linux system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Troubleshoot_and_solution_for_high_disk_load_issues_on_Linux_system_ECS_instances"
---

This topic describes how to troubleshoot and handle the `No space left on device` error that may occur due to high disk load (usage) when you create a file or application on a Linux instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5p-l55yL5b2T5YmN56OB55uY5L2_55So546H55qE5L2_55So5oOF5Ya1"></span>
### View details of current disk usage


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current disk usage.

   ```Plain Text
   df -h
   ```
   

   Sample output

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d934b8a64ff74f4ef149eb9a7284b755.png) </span>

3. View disk usage details for each directory level by level.

   > This topic starts from the root directory `/` as an example.   
   

   1. Execute the following command to enter the root directory.

      ```Plain Text
      cd /
      ```
      

   2. Execute the following command to view the folder in the current directory that uses the most disk space.

      ```Plain Text
      du -sh *
      ```
      

      Sample output

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e70ca3e62d2e2b4f0dee3ecd98b3024c.png) </span>

   3. Execute the following command to enter the usr directory.

      > In the example provided in this topic, the large file is in the `usr` directory. Replace it with the actual directory path.      
      

      ```Plain Text
      cd usr/
      ```
      

   4. Execute the following command to view the folder in the current directory that occupies the most disk space.

      ```Plain Text
      du -sh *
      ```
      

      Sample output

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0269eda216d352089b3ab410f3ca1754.png) </span>

   5. Repeat steps c and d until you locate the file that uses a large amount of space. After this, confirm whether the target file is used by the system or for business purposes.

      * **File cleanup cannot be performed**

         If the target large file is necessary for your business or system and cannot be cleaned up, you can upgrade your instance configuration, expand the volume capacity, or change the volume specification. This ensures that programs can run normally without being limited by the performance of the volume. For operation details, refer to [Changing instance types](https://docs.byteplus.com/en/docs/ecs/Overview-2), [Expanding volumes](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux), and [Changing volume specifications](https://docs.byteplus.com/en/docs/ecs/Modify-volume-type).



&nbsp;

      * **File cleanup can be performed**

         If the target large file is not necessary, you can execute the following command to forcibly delete the file and free up disk space.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Deletion is irreversible. Please proceed with caution.         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Replace <code>/usr/local/test_large_file</code> in the command with the actual path of the target file.         </div>
         

         ```Plain Text
         rm -rf /usr/local/test_large_file
         ```
         


<span id=".5p-l55yL5b2T5YmN56OB55uYSW5vZGXkvb_nlKjnjofnmoTkvb_nlKjmg4XlhrU="></span>
### View Inode usage of current disk


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the Inode usage.

   ```Plain Text
   df -i
   ```
   

   Sample output

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c116fc721b66a4518a840a92050a6cb4.png) </span>

3. If the Inode usage rate reaches or is close to 100%, you need to clean up files or directories with high Inode usage.

   1. Execute the following commands to confirm the number of files in the root directory `/` .

      ```Plain Text
      cd /
      for i in ./*; do echo $i; find $i | wc -l; done
      ```
      

      Sample output

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0dec313b3fa9c627c3a0c04896cf845e.png) </span>

   2. Execute the following command to enter the directory with the largest number of files.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">A greater number of files indicates higher Inode usage.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the example provided in this topic, the <code>usr</code> directory stores the largest number of files.      </div>
      

      ```Plain Text
      cd usr/       
      ```
      

   3. Execute the following command to view which directory in the current directory stores the largest number of files.

      ```Plain Text
      for i in ./*; do echo $i; find $i | wc -l; done
      ```
      

      Sample output

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5038ce20065d99e46a7fbed0e626aaa6.png) </span>

   4. Repeat steps b and c to enter the directory with the highest Inode usage (which indicates the largest number of files) level by level until you locate the files or directories with excessive space usage.

      * **Cleanup cannot be performed**

         If the target file or directory is necessary for business or the system and cannot be cleaned up, you can expand the volume capacity or change the volume specification. This ensures that programs can run normally without being limited by the performance of the volume. For operation details, refer to [Expanding volumes](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux) and [Changing volume specifications](https://docs.byteplus.com/en/docs/ecs/Modify-volume-type).

      * **Cleanup can be performed**

         If the target file or directory is not necessary, you can execute the following command to forcibly delete the target file and free up disk space.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Deletion is irreversible. Please proceed with caution.         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Replace <code>/usr/local/test_large_file</code> in the command with the actual path of the target file.         </div>
         

         ```Plain Text
         rm -rf /usr/local/test_large_file
         ```
