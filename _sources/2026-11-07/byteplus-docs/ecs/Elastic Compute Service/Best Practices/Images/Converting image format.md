---
title: "Converting image format"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Converting-image-file-formats"
---

This topic describes how to use qemu\-img to convert the format of an existing image file to RAW, QCOW2, VHD, or VMDK.

## Applicable scenario

The BytePlus platform allows you to import image files in RAW, QCOW2, VHD, VMDK formats as custom images. If you have an image file in another format, you need to convert the file format yourself before you import the image file.

You can use the qemu\-img tool to convert image files between formats such as RAW, QCOW2, VHD, and VMDK.

> **tip**

> You cannot use qemu\-img to convert image files in ISO format to RAW or QCOW2 format. Follow the [image creation](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images) guidelines and use a virtual machine to create RAW or QCOW2 image files from the ISO image files.

## Procedure

### Convert image format in the Linux operating system

1. Execute the following command on the server where your image file is stored to install qemu\-img.

   * CentOS

      ```Plain Text
      yum install -y qemu-img
      ```

   * Ubuntu/Debian

      ```Plain Text
      apt-get update
      apt-get install -y qemu-utils
      ```

2. Execute the following command to convert the format of the image file.

   ```Plain Text
   qemu-img convert -f <source image file format> -O <target image file format> <source image file name> <target file name>
   ```

   Parameter descriptions:

   |Parameter |Description |Sample value |
   |---|---|---|
   |Source image file format |The format of the source image file to be converted. |raw |
   |Target image file format |The format of the new image file format after conversion. |qcow2 |
   |Source image file name |The full name of the source image file to be converted. |CentOS7.raw |
   |Target file name |The full name of the new image file format after conversion. |CentOS7.qcow2 |

3. After the format is converted, the new image file is stored in the directory where the source image file is located.

### Convert format in the Windows operating system

1. On the server where your image file is stored, use a browser to access the [qemu-img](https://qemu.weilnetz.de/w64/) site.

2. Select the required version of qemu\-img and click the filename to download it to your local machine.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b0c2c4dcaac49cb876d39159b949e844.png)

3. Double\-click the downloaded .exe file and follow the instructions to install qemu.

   > Make sure to record the installation directory path of qemu.

4. Configure the environment variables for qemu.

   > In this practice, the Windows Server 2022 Datacenter Edition 64 bit operating system is used as an example.

   1. Click the "Windows" icon, and select "Windows System".

   2. Right\-click "This PC", and then select "More \> Properties".

   3. Select "About" from the directory tree on the left, and at the bottom of the "About" page under "Related settings", click the "Advanced system settings" button.

   4. On the "Advanced" tab of the "System Properties" page, click the "Environment Variables" button.

   5. On the "Environment variables" page, select the `Path` variable in the "System variables" section, and click the "Edit" button.

   6. On the "Edit environment variable" page, click the "New" button and enter the qemu installation directory path specified in Step 3.

   7. Click the "OK" button on each configuration page one by one to complete the configuration.

   8. Open a new PowerShell dialog box, and execute the following command to verify whether qemu\-img can be used as expected.

      ```Plain Text
      qemu-img --version
      ```

5. In the PowerShell dialog box, execute the following command to switch to the directory where the source image file is located.

   ```Plain Text
   cd <The directory of the source image file>
   ```

6. Execute the following command to convert the format of the source image file.

   ```Plain Text
   qemu-img convert -f <source image file format> -O <target image file format> <source image file name> <target file name>
   ```

   Parameter descriptions:

   |Parameter |Description |Sample value |
   |---|---|---|
   |Source image file format |The format of the source image file to be converted. |raw |
   |Target image file format |The format of the new image file format after conversion. |qcow2 |
   |Source image file name |The full name of the source image file to be converted. |CentOS7.raw |
   |Target file name |The full name of the new image file format after conversion. |CentOS7.qcow2 |

7. After the format is converted, the new image file is stored in the directory where the source image file is located.

## Subsequent steps

After a successful conversion, you can import the obtained image file into BytePlus as a custom image. For more information, see [Importing custom images](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1).
