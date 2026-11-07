---
title: "FTP/SFTP"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/FTP_SFTP"
---

<span id="_1-产品概述"></span>
# 1. Product overview

On the client side, an FTP/SFTP server is deployed. Data from the data warehouse is regularly pushed to the FTP/SFTP server in the form of files. The CDP/ABI system connects to the FTP/SFTP server to download the data, then maps the file structure to the corresponding table structure so that the CDP/ABI system can recognize and read the data.


* **FTP**: Suitable for transferring non\-sensitive data, mainly used in trusted internal network environments.

* **SFTP**: Suitable for transferring sensitive data, especially in public networks or scenarios with strict security requirements.


<span id="ab092156"></span>
# 2. Usage scenarios

<span id="19ee21a7"></span>
## 2.1 When to use FTP?


* No encryption required: In a secure internal network environment where file transfer does not require encrypted communication, FTP is a simple and efficient choice.

* Compatibility requirements: Some legacy systems or specific software may only support FTP.

* High speed requirements: In rare cases, FTP may be slightly faster than SFTP because it does not have the overhead of encryption and decryption.

* Simple setup and usage: FTP is relatively simple to set up and use, without the need for additional configurations such as SSH keys.


<span id="9b7a815d"></span>
## 2.2 When to use SFTP?


* Encryption required: When transferring sensitive data over public networks (such as the Internet), SFTP is the preferred choice because it provides strong encryption to ensure that data is not intercepted or tampered with during transmission.

* High security requirements: SFTP transmits data through an SSH (Secure Shell) channel, offering higher security and is suitable for scenarios where secure data transmission must be ensured.

* Authentication and authorization: SFTP supports key\-based authentication, which can provide a more secure authentication mechanism than FTP usernames and passwords.

* Compliance requirements: In certain industries or under legal and regulatory requirements, data transmission must be encrypted (such as in finance or healthcare), in which case SFTP must be used.


<span id="_2-使用条件"></span>
# 3. Usage requirements

Users must have **project editing** or **Permission \- Content Management \- Module \- Data Connection \- Create Connection** permission to use this feature.

<span id="_3-操作步骤"></span>
# 4. Operation steps

First, click **Data Preparation \> Data Connection**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e538f1feabbb4340bd4d16be414d0f3b~tplv-goo7wpa0wc-image.image) </span>

Next, in the upper left corner of the data connection directory, click the **New Data Connection** button and select the "Web Connector \- FTP/SFTP" data connection.

Then, on the edit page, configure the corresponding parameters. For example:


* Data connection name: Required. Use the format connectionName_YYYYMMDDHHMMSS, for example, ftp_sftp_xxx.

* Configure server port, username, password, and other parameters.


**FTP server deployment:** 

The customer side can deploy the server independently, but it can allow CDP system connection and access.

The FTP server must be configured in passive mode, and the port range must be sufficiently large. The recommended value is: number of FTP datasets \* 2.

\*For more common issues during the configuration process, refer to this document [Appendix 2].


* Protocol type: FTP

* FTP connection mode: Default is Pasv (passive mode).

* File type: Supports csv and txt.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0418c9fb08cb494bb941d99ec69c365c~tplv-goo7wpa0wc-image.image) </span>

**FTP file content and format requirements are as follows:** 


* **File directory format**: **Required,**  for example, /data/student.

   1. Rule 1: The name of the last\-level directory must be the same as the table name, in the format /data/{tableName}, for example, /data/student.

   2. Rule 2: Multi\-level directory parsing is not supported. Do not define subdirectories under the data file directory; if present, the system will automatically skip them.

   3. Rule 3: It is not recommended to change the file directory. Before making changes, update the [DataWind \- Data Connection] configuration item to avoid data query errors.

   4. Rule 4: One file directory represents one table. Multiple tables sharing one file directory are not supported, nor is one table having multiple directories.

* **File directory content:** 

   1. **Data file: Required,**  only CSV and TXT are supported. Multiple files are allowed, and there are no restrictions on file names.

      1. Rule: The column (field) order in the data file must be consistent with the metadata file, and the data file must not contain a header row (field name row).

      2. Rule: For each query, all data is retrieved based on the file directory path (excluding files in subdirectories).

      3. Rule: The total size of files in a single file directory is recommended to be less than 500 GB.

   2. **Metadata file: Required,**  {tableName}.yml (if there are structural changes, this file needs to be modified).

      1. Rule 1: Used to parse data files and map them to structured tables.

      2. Rule 2: {tableName} is the table name. Table name changes are not supported. {tableName} must be consistent with the directory name.

      3. For the file content format, refer to Appendix 1 below

   3. **Synchronization success flag file: Required,**  {date}.verf, for example, 20230801.verf

      1. Logic: Used to indicate whether the data has been fully pushed. This task is used to build dependency logic for FTP tasks.

      2. Rule 1: The file must exist. When the task is executed, it reads the file named 20230801 to determine whether the data for the corresponding business date is ready.

      3. Rule 2: Synchronization success files from historical updates can be retained or deleted. This does not affect the determination for the latest day.

      4. Rule 3: In backfill scenarios, retaining historical data is not logically supported. Each time data is pulled from FTP, it is a full pull based on the file directory. During backfill, if the synchronization success flag for a historical date still exists, all data will be pulled according to the latest files. If it does not exist, the backfill task will remain pending and cannot be executed successfully.


Click **Parse table structure** to parse the file directory. The data table preview displays table names and field names. If there are too many table names, scrolling is supported. By default, the field information under the first table name is displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82524ad3f1fa4259a5bb759e664634c9~tplv-goo7wpa0wc-image.image) </span>

Click **Test connection** to test the connectivity of the data source.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a7f1ebefc544c398ccbac652e4b6c86~tplv-goo7wpa0wc-image.image) </span>

After the test is successful, click **Save** to proceed.

<span id="附录1：文件内容格式"></span>
# Appendix 1: File content format

```yaml
# Please fill in according to the following parameters:
### name: Field name (required)
########## Field naming rules: The field name must be unique; only letters, numbers, and underscores are supported, and it must start with a letter, with a maximum of 100 characters
### alias: Field alias (optional)
########## Field alias rules: No restriction on character type, maximum 100 characters
### type: Field type (required)
########## Type rules: No need to specify length, the following types can be specified:
    # string
    # boolean
    # long
    # double
    # date
    # datetime
    # Only basic types such as int are supported for %s in the following two types
    # Multi-level nesting is not supported, for example array<array<int>>
    # array<%s>
    # map<%s，%s>
#--------------------------------------------------------------------------------

columns:
  - name: brand_id
    alias: brand id
    typ: int
  - name: brand_name
    alias: brand name
    type: string
  - name: brand_desc
    alias: brand description
    type: string
  - name: create_time
    alias: create time
    type: date
  - name: update_time
    alias: update time
    type: date
```


<span id="附录2：ftp配置常见问题"></span>
# Appendix 2: Common FTP configuration issues

**Q1: How to resolve the 530 login incorrect error when connecting to the FTP server?** 


1. Incorrect password.

2. Check the /etc/vsftpd/vsftpd.conf configuration

   vim /etc/vsftpd/vsftpd.conf

   **Refer to the following configuration**

   anonymous_enable=YES

   userlist_deny=NO //See the explanation below

   userlist_enable=YES

   userlist_file=/etc/userlist

   seccomp_sandbox=NOlocal_enable=YES

   pam_service_name=vsftpd //This is important. Some say that on Ubuntu it is pam_service_name=ftp, you can try it.

   Explanation about the userlist file


<span id="vsftpd-userlist"></span>
# vsftpd userlist

<span id="if-userlist-deny-no，-only-allow-users-in-this-file"></span>
# If userlist_deny=NO， only allow users in this file

<span id="if-userlist-deny-yes-default-，-never-allow-users-in-this-file，-and"></span>
# If userlist_deny=YES (default)， never allow users in this file， and

<span id="do-not-even-prompt-for-a-password"></span>
# do not even prompt for a password.

<span id="note-that-the-default-vsftpd-pam-config-also-checks-etc-vsftpd-ftpusers"></span>
# Note that the default vsftpd pam config also checks /etc/vsftpd/ftpusers

<span id="for-users-that-are-denied"></span>
# for users that are denied.


3. Check /etc/pam.d/vsftpd

   vim /etc/pam.d/vsftpd

   Comment out

   #auth required pam_shells.so

   **Q2: How to resolve the "425 Security: Bad IP connection" error when uploading files from a Linux instance to an FTP site?** 

   **1) Possible causes:** 

   FTP service has two types of connections: one is the control connection, and the other is the data connection. By default, when transferring data, the FTP server checks whether the source IP addresses of the two connections are the same. If not, the "425 Security: Bad IP connection" error will be reported. This issue is often caused by clients in a NAT network with multiple public IP addresses associated with the NAT, resulting in two connections with inconsistent source IP addresses.

   **2) Solution:** 

   Disable IP address security check in passive mode as follows:

* Run the following command to edit the FTP configuration file:

* vi /etc/vsftpd/vsftpd.conf

* Add the following content to the configuration file:

   pasv_promisculous=yes

* After saving and exiting, run the following command to restart the FTP service.

* service vsftpd restart


**References:** 


* 530 error solution: https://blog.csdn.net/Adonis_D_Gogh/article/details/101023367

* 425 Security: Bad IP connection solution:

   425 Security：[Bad IP connection" error is reported when I upload a file to an FTP site on a Linux instance](https://www.alibabacloud.com/help/en/ecs/425-security-bad-ip-connection-error-is-reported-when-i-upload-a-file-to-an-ftp-site-on-a-linux-instance#:~:text=Cause,IP%20connection%22%20error%20is%20reported.)


<span id="042f62aa"></span>
# Appendix 3: SFTP configuration experience


1. Port modification (addition): https://blog.csdn.net/dandan201212/article/details/124772566
