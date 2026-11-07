---
title: "Setting up a Python environment"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Setting_up_Python_environment"
---

You can install or upgrade the Python 3 environment on an ECS instance. This way, you can leverage the powerful features of the [Python](https://www.python.org/) language and manage the development environment in a flexible manner.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have [purchased an ECS instance](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances) and [associated an EIP](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP) with the instance.

<span id=".5ZyoTGludXjkuK3mkK3lu7o="></span>
## Set up a Python environment in Linux

<span id=".5q2l6aqk5LiA77ya5a6J6KOFUHl0aG9u"></span>
### Install/Upgrade Python

You can use the Advanced Packaging Tools (APT) or manually download and compile the source code to install the required Python version.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you use the APT, you can quickly install Python. However, the Python version provided in the software repository may not be the latest version or the specific version you need. For example, you might require Python 3.9.22. Under such circumstances, we recommend that you manually compile the source code and install the required Python version.</div>


* <div data-tips="true" data-tips-type="tip">Many system tools, such as yum, apt, cloud\-init, systemd, and netplan depend on the default Python version of the operating system. Therefore, when you upgrade the Python version, we recommend that you manually compile the code and install the new version of Python. <strong>We recommend that you do not uninstall the old Python version or replace the</strong> <strong><code>/usr/bin/python</code></strong><strong>or</strong> <strong><code>/usr/bin/python3</code></strong><strong> symbolic link</strong>. Otherwise, system exceptions may occur or the instance may fail to start. After the upgrade, you can use the new version of Python by referring to the <a href="https://docs.byteplus.com/en/docs/ecs/Setting_up_Python_environment#nza6Nb1R">instructions in this topic</a>.</div>




<Tabs>
<Tab zoneid="lXikWX4BtI" title="Use the APT tool">
<TabTitle>Use the APT tool</TabTitle>

In the examples in this section, Python 3 is installed on Ubuntu 20.04 and CentOS Stream 8 operating systems by using the package manager. For other image versions, install the Python version based on your business requirements.


<Tabs>
<Tab zoneid="dieaRE7Suf" title="veLinux/Ubuntu/Debian">
<TabTitle>veLinux/Ubuntu/Debian</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance?LibVersion=markdown备份版本).

2. Execute the following command to update the local software package index. This ensures that the package information in the system is up\-to\-date.

   ```Plain Text
   sudo apt update
   ```
   

3. Execute the following command to query installable Python packages in the software repository.

   ```Plain Text
   apt-cache search python | grep -E '^python3\.[0-9]+\s'
   ```
   

   When the following output appears, Python 3.8 and 3.9 can be installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e83fbf77b7d061e54b73548d9f54c723.png) </span>

4. Execute the following command to install the Python package corresponding to the instance architecture.

   ```Plain Text
   sudo apt install -y python3.9
   ```
   

5. Execute the following command to check whether Python 3.9 has been installed successfully.

   ```Plain Text
   python3.9 --version
   ```
   

   When the following output appears, Python 3.9.5 has been successfully installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_846c57987d77608f795413486850bbac.png) </span>


</Tab>
<Tab zoneid="tD4wum3FsB" title="CentOS">
<TabTitle>CentOS</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance?LibVersion=markdown备份版本).

2. Execute the following command to update the local software package index. This ensures that the package information in the system is up\-to\-date.

   ```Plain Text
   sudo yum update -y
   ```
   

3. Execute the following command to query installable Python packages in the software repository.

   ```Plain Text
   sudo yum list available | grep -E '^python3[0-9]\.(x86_64|aarch64|noarch)'
   ```
   

   When the following output appears, Python 3.8.17 and 3.9.19 can be installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a51d2534ac6052ac723cbf488cd47cfc.png) </span>

4. Execute the following command to install the Python package corresponding to the instance architecture.

   ```Plain Text
   sudo yum install -y python39.x86_64
   ```
   

5. Execute the following command to check whether Python 3.9 has been installed successfully.

   ```Plain Text
   python3.9 --version
   ```
   

   When the following output appears, Python 3.9.19 has been successfully installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_72c40a8bd346bfa95d40a83b61e33c75.png) </span>


</Tab>
</Tabs>



</Tab>
<Tab zoneid="C4dOLpvVNp" title="Manually compile the code">
<TabTitle>Manually compile the code</TabTitle>

In the examples in this section, Python 3.9.22 is installed on Ubuntu 20.04 and CentOS Stream 8 operating systems. For other image versions, install dependency libraries based on your business requirements to ensure system compatibility.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance?LibVersion=markdown备份版本).

2. Install various dependency libraries and tools required for Python compilation, including compilers, development libraries, and other necessary packages.

   
   <Tabs>
   <Tab zoneid="uUB0bTQtz1" title="veLinux/Ubuntu/Debian">
   <TabTitle>veLinux/Ubuntu/Debian</TabTitle>
   
   1. Execute the following command to update the local software package index. This ensures that the package information in the system is up\-to\-date.
   
      ```Plain Text
      sudo apt update
      ```
      
   
   2. Execute the following command to install various dependency libraries and tools required for Python compilation, including compilers, development libraries, and other necessary packages.
   
      ```SQL
      sudo apt install-y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="t1YkAVX6rR" title="CentOS">
   <TabTitle>CentOS</TabTitle>
   
   Execute the following command to install various dependency libraries and tools required for Python compilation, including compilers, development libraries, and other necessary packages.
   
   ```Plain Text
   sudo yum groupinstall -y "Development Tools"
   sudo yum install -y gcc openssl-devel bzip2-devel libffi-devel zlib-devel \
       ncurses-devel readline-devel sqlite-devel xz-devel tk-devel gdbm-devel \
       libuuid-devel libnsl2-devel wget
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

3. Execute the following command to download the source code package of Python 3.9.22 from the official Python website.

   ```Plain Text
   wget https://www.python.org/ftp/python/3.9.22/Python-3.9.22.tgz
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example in this section, Python 3.9.22 is installed. Replace the download link with the download link of the Python version that you want to install. <a href="https://www.python.org/downloads/source/">Learn more</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Since cross\-border data downloads are involved, the download might take a long time. You can also download the source code package to your local environment and then upload the package to the ECS instance. <a href="https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview?LibVersion=markdown备份版本">Learn more</a>.   </div>
   

4. Execute the following command to decompress the downloaded Python 3.9.22 source code package.

   ```Plain Text
   tar -xf Python-3.9.22.tgz
   ```
   

5. Execute the following command to switch the current working directory to the Python 3.9.22 source code directory.

   ```Plain Text
   cd Python-3.9.22
   ```
   

6. Execute the following command to execute the Python configuration script, configure the compilation environment for the Python interpreter, and enable performance optimization options.

   ```Plain Text
   ./configure --enable-optimizations
   ```
   

7. Execute the following command to compile Python source code based on the configuration file (Makefile) by using the Make tool.

   ```Plain Text
   sudo make -j$(nproc)
   ```
   

   Compilation success example:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba4d18bdc5260cbb45fa7f83d179e228.png) </span>

8. Execute the following command to install the compiled Python interpreter in the `/usr/local/bin/` directory.

   ```SQL
   sudo make altinstall
   ```
   

   Installation complete example:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e291ef6db2b9d6c45f5f20fd81baa475.png) </span>

9. Execute the following command to view the Python version and verify whether Python 3.9.22 has been successfully installed.

   ```Plain Text
   /usr/local/bin/python3.9 --version
   ```
   

   Successful installation example:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fedca1a1bf9ad00167933697a58135f.png) </span>

10. Execute the following command to install PyPI.

   ```Plain Text
   /usr/local/bin/python3.9 -m ensurepip
   /usr/local/bin/python3.9 -m pip install --upgrade pip
   ```
   

   Successful installation example:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74e34af2e4caa1387a1f7099c85e4852.png) </span>


</Tab>
</Tabs>


<span id="nza6Nb1R"></span>
### Use the specified version of Python

If multiple versions of Python are installed on your ECS instance, you can use the specified version of Python based on your business requirements by using the following methods.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After you install the new version of Python, we recommend that you use the specified version of Python by using the <strong>Python interpreter with a version number</strong>, <strong>specifying the default Python version for the current user</strong>, or <strong>using a virtual environment</strong>.</div>


* <div data-tips="true" data-tips-type="warning">If you want to <strong>specify the default Python version for the system</strong>, make sure that this action will not affect the operating system components and business operations.</div>




<Tabs>
<Tab zoneid="jkUybOrMbF" title="Use the Python interpreter with a version number">
<TabTitle>Use the Python interpreter with a version number</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Use Python 3 interpreters with version numbers in locations, such as the command line and code. Example:

   * View the Python version

      ```Plain Text
      /usr/local/bin/python3.9 --version
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6f66d59d104a15b23b52394a45e731b5.png) </span>

   * View the PyPI version

      ```Plain Text
      /usr/local/bin/pip3.9 --version
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe166a4464e1e2bd4b2f066a6fa2b1c0.png) </span>


</Tab>
<Tab zoneid="orjtoPqi1N" title="Specify a Python version for the target user">
<TabTitle>Specify a Python version for the target user</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Switch to the target user.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can separately specify a Python version for users, such as the root user.   </div>
   

   1. Execute the following command to view existing users.

      ```Plain Text
      cat /etc/passwd | cut -d: -f1
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aad573ff6f5e9ffa2e40ef52192d7103.png) </span>

   2. Execute the following command to switch to the target user.

      ```Plain Text
      su pytest
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>pytest</code> with the name of the target user.      </div>
      

3. Edit the corresponding configuration file based on the Shell interpreter you use.

   1. Execute the following command to open the configuration file.

      * Bash

         ```Plain Text
         vim ~/.bashrc
         ```
         

      * ZSH

         ```Plain Text
         vim ~/.zshrc
         ```
         

   2. Press the `i`key to enter the edit mode, and copy the following content to the file.

      ```Plain Text
      alias python3=/usr/local/bin/python3.9
      alias pip3=/usr/local/bin/pip3.9
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>/usr/local/bin/python3.9</code> and <code>/usr/local/bin/pip3.9</code> with the actual paths of Python and PyPI versions, respectively.      </div>
      

   3. Press the `Esc` key to exit the edit mode, enter `:wq`, and then press Enter to save the changes and close the file.

   4. Execute the following command to make the configuration take effect.

      * Bash

         ```Plain Text
         source ~/.bashrc
         ```
         

      * ZSH

         ```Plain Text
         source ~/.zshrc
         ```
         

4. Execute the following command to check whether the Python version used by the current user has been successfully changed.

   * View the Python 3 version

      ```Plain Text
      python3 --version
      ```
      

      When the following output appears, Python 3.9.22 is specified for the current user.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2ef68c05aecd40dd0d8d166e5254d6b2.png) </span>

   * View the PyPI version

      ```Plain Text
      pip3 --version
      ```
      

      When the following output appears, the 25.1.1 version is specified for PyPI 3 for the current user.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68db80e187b997995adbfb6d4484d735.png) </span>


</Tab>
<Tab zoneid="sFAVDXWQCo" title="Use a virtual environment">
<TabTitle>Use a virtual environment</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to create a virtual environment.

   ```Plain Text
   /usr/local/bin/python3.9 -m venv myenv
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>/usr/local/bin/python3.9</code> with the path of the target Python version.   </div>
   

3. Execute the following command to enter the virtual environment.

   ```Plain Text
   source myenv/bin/activate
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d377e711595543feb4a36380ede845b1.png) </span>

4. Execute the following command to confirm the Python version used in the current environment.

   ```Plain Text
   python --version
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ef1951c06785fd96881b943662c72c96.png) </span>

5. You can also execute the following command to exit the virtual environment. For more Python virtual environment actions, view the [official venv documentation](https://docs.python.org/library/venv.html).

   ```Plain Text
   deactivate
   ```
   





</Tab>
<Tab zoneid="mFSCEOfsqo" title="Specify the default Python version of the system">
<TabTitle>Specify the default Python version of the system</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current default Python 3 version.

   ```Plain Text
   python3 --version
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ed0232f6056a7d05d66e2945ce3e8aa.png) </span>

3. Execute the following command to view configurable Python 3 versions.

   ```Plain Text
   sudo update-alternatives --display python3
   ```
   

   When the following output appears, you can select Python 3.8 or Python 3.9 as the default Python 3 version.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a80419483d6aceb038ae11706866f93e.png) </span>

4.  **(Optional)**  If the configurable Python 3 versions do not include the version you want to use, execute the following command to add the desired Python version as an option.

   ```Plain Text
   sudo update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.9 1
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>/usr/local/bin/python3.9</code> with the actual path to your Python version.   </div>
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56c3057ebc76b276ab2947cb9142010c.png) </span>

5. Select the default version.

   1. Execute the following command to view the Python versions that you can select.

      ```Plain Text
      sudo update-alternatives --config python3
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f898ba9a2c6318dbf6e5e37c6b1cd230.png) </span>

   2. Enter the serial number of the file that you want to use as the default Python version based on your business requirements. In the example in this topic, Python 3.9 is specified as the default version.

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f5e23420de646f7aa59b1090e298c55.png) </span>

6. Execute the following command to confirm the current default version of Python 3.

   ```Plain Text
   python3 --version
   ```
   

   When the following output appears, you have successfully switched the default version of Python 3 to 3.9.22.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cec9cbb979f576c35404b917858483a7.png) </span>


</Tab>
</Tabs>


<span id=".5ZyoV2luZG93c-S4reaQreW7ug=="></span>
## Set up a Python environment in Windows

In this example, Python 3 is installed on the English version of the 64\-bit Windows Server 2022 operating system.

<span id=".5q2l6aqk5LiA77ya5a6J6KOFUHl0aG9u"></span>
### Step 1: Install Python


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Visit the [official Python website](https://www.python.org/downloads/windows/) in your browser.

3. Select the Python version installer you want to install and download the installer.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e54b1f1e0693c93db2ed67f98bc174b6.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, 64\-bit Python 3.12.5 is installed. Download the Python version installer you want to use.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since cross\-border data downloads are involved, the download might take a long time. You can also download the Python version installer to your local environment and then upload the installer to the ECS instance. <a href="https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview">Learn more</a>.   </div>
   

4. After the download is complete, double\-click the downloaded Python executable file to start the installation process.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0f25dc95f34201e2a6bd4889f67875e6.png) </span>

5. Select "Use admin privileges when installing py.exe" and "Add python.exe to PATH" and then click the "Install Now" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2c66c4f7f3eadb55ff162f9d43820a88.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this example, all components in the Python executable file are installed. This is the best practice for developers who want to use Python for any type of project. You can also click "Customize installation" to manually select the components you want to install. <a href="https://docs.python.org/zh-cn/3/using/windows.html">Learn more</a>.   </div>
   

6. After the installation is complete, click the "Close" button to close the installation page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_73a39567decd05bc9ea1797e2bf611e2.png) </span>

7. Click the Windows icon, and click "Windows System \> Command Prompt".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b11e2132f97514bb1e2af55aba012c26.png) </span>

8. Execute the following command to check whether Python has been successfully installed and configured.

   ```Plain Text
   python
   ```
   

   Sample output:

   As shown in the figure below, you have successfully installed Python 3.12.5 on the instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_104245b93d8b3292568d580b04b807ce.png) </span>


<span id=".5q2l6aqk5LqM77ya6YWN572u57O757uf6buY6K6kUHl0aG9u54mI5pys77yI5Y-v6YCJ77yJ"></span>
### Step 2: Specify the default Python version of the system (optional)

If multiple versions of Python are installed on your ECS instance, you can modify the default Python version of the system.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Click the Windows icon and click "Windows System \> Run".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2c44dff7e90b42224bea79fdf88b330.png) </span>

3. Enter the following content in the dialog box, and click the "OK" button to open the system attribute dialog box.

   ```Plain Text
   sysdm.cpl
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7368538e9c3da7cc5f8d1d83a021284f.png) </span>

4. Select the "Advanced" tab, and click the "Environment Variables" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b3c8d79c05b2b0a846d2c715b360336.png) </span>

5. Select the "Path" parameter in the "User variables for Administrator" area, and click the "Edit..." button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d77f3366dff298aa8d584530afe3e0a.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The path information of the Python versions installed in this topic is configured in the "User variables for Administrator" area, rather than the "System variables" area. Select the "Path" parameter where the Python path information is located based on actual conditions.   </div>
   

6. Select the Python version you want to use by default, and click the "Move Up" button to move it to the top.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You need to move both paths of the target Python version to the top.   </div>
   

   * Example before adjustment:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f96d6a9d4e6373925475c29f9f5263e.png) </span>

   * Example after adjustment:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b137d20bcb253ef1e988ddfa62b513c5.png) </span>

7. Click the "OK" button in sequence to save the changes and close the "System Properties" dialog box.

8. Click the Windows icon and click "Windows System \> Command Prompt".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b11e2132f97514bb1e2af55aba012c26.png) </span>

9. Execute the following command to check whether the default Python version has been successfully changed.

   ```Plain Text
   python --version
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7342de96a941f3504f971063e161433c.png) </span>
