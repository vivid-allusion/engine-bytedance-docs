---
title: "Remote connection to the development machine"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Remote_connection_to_the_development_machine"
---

When using a terminal or an IDE such as VSCode on a local or other device to remotely connect to the development machine, you can use direct SSH connection to quickly start writing, debugging, and running data processing tasks.

<span id="9bb7d0ce"></span>
## Prerequisites


1. A key pair has been generated locally.

   1. To generate a public key and private key on the local machine, use the `ssh-keygen` command to create new public and private key files.

   2. Use the `cat ~/.ssh/id_rsa.pub` command to obtain the public key of the local machine.

2. The SSH public key configured when creating the development machine must match the local private key.

3. The development machine status is Running.

4. When creating the development machine, ensure the selected security group allows the SSH client network segment. Also ensure that port 2222 is allowed.


<span id="d3c76b4f"></span>
## Procedure

<span id="bdcaaece"></span>
### Obtain the login command


1. After the development machine enters the running state, you can obtain the SSH login command using the following methods.

   1. Development machine list page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7e94d4a9ab44c3387f9fdfee8cff232~tplv-goo7wpa0wc-image.image) </span>

   2. Development machine details page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a9f14eeb1c147459b17c25b5bd16104~tplv-goo7wpa0wc-image.image) </span>


<span id="c384d489"></span>
### Connect to the development machine locally

<span id="d9c05f95"></span>
#### Connect to the development machine locally using Trae


1. Go to [Trae's official website](https://www.trae.ai/), install Trae on your computer, and refer to [Trae installation guide](https://docs.trae.ai/ide/set-up-trae?_lang=zh) for detailed instructions.

2. Open the remote resource manager, then click the  **+**  button.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bdf677189a04fb2b27ee08315708105~tplv-goo7wpa0wc-image.image" width="2072px" />   </div>
   

3. Enter the SSH login command in the input box. For the command, refer to [Caution](https://docs.byteplus.com/docs/Byteplus_LAS/92509#c23424e4).

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/181e494126584d208add3063a048d582~tplv-goo7wpa0wc-image.image" width="2072px" />   </div>
   

4. After clicking **Confirm**, the remote host name appears in the SSH connection target.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b91b56b69ec4b3785bfc739034f0902~tplv-goo7wpa0wc-image.image" width="2072px" />   </div>
   

5. Open the resource manager, select to connect to the host in the current window, and wait for Trae to download and install the remote server.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6c2fbf3febc4373afa24726fdd85bc3~tplv-goo7wpa0wc-image.image" width="2072px" />   </div>
   

* For detailed steps, refer to: [Develop with SSH (Remote SSH) - Documentation - Trae CN](https://docs.trae.cn/ide/ssh-remote).


<span id="a0875373"></span>
#### Connect to the development machine locally using VSCode


1. Install the Remote Explorer extension in the local VSCode application.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d81d22b3bc746cca79d68aba922cf4b~tplv-goo7wpa0wc-image.image" width="1058px" />   </div>
   

2. On the Welcome page, select the `Connect to...` button. If this is your first time, click the `SSH` option and wait for VSCode to automatically install `Remote - SSH` and `Remote - SSH: Editing Configuration Files`. The dropdown list will then show the `Connect to Host...` option; click this option.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fab1149f88394edaa2851423f25aa37e~tplv-goo7wpa0wc-image.image" width="1274px" />   </div>
   

3. Then click `Configure SSH Hosts...`, which will display the SSH configuration file path.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0d1f4fa6f32495b8fa77aa15da8e40e~tplv-goo7wpa0wc-image.image" width="2400px" />   </div>
   

4. Click the SSH path shown in the list (the default path is usually `~/.ssh/config`), open the config file, and configure it.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de7a4cb86dfa44ff8f98cd52211987c7~tplv-goo7wpa0wc-image.image" width="1260px" />   </div>
   


Change the port to the one you specified when creating the development machine, then paste the following configuration at the end of the file and save it:

```YAML
HOST 101.126.65.0
    HostName 101.126.65.242 
    IdentityFile <your_rsa_path>
    Port <Access port, which is the SSH call port set when creating the developer computer, such as: Port 1024>
    User root
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0550870edab6469ba1a04494bb83a603~tplv-goo7wpa0wc-image.image" width="2042px" /></div>



5. Click the `Connect to...` button again, then select `Connect to Host...` from the dropdown list, and choose the path you just configured.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfe3bebafa5a48daa071f83e6baa66a5~tplv-goo7wpa0wc-image.image" width="2400px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed steps, refer to: <a href="https://vscode.js.cn/docs/remote/ssh">Using SSH for remote development \- VSCode editor</a>.</div>



6. After a successful connection, open a terminal to use the development machine.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70c9c14442e64f1fba52950c5992ca97~tplv-goo7wpa0wc-image.image" width="2042px" /></div>


<span id="641a13a4"></span>
#### Connect to the development machine using your local PyCharm


1. Install the Remote Develop Gateway plugin in your local PyCharm application.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d7e04a1b5194412a41bda5c36739c42~tplv-goo7wpa0wc-image.image" width="1948px" /></div>



2. On the PyCharm welcome page, create a new connection. Enter root for Username, the IP from the SSH login command for Host, and add the port number from the SSH login command for Port. If the private key address is ~/.ssh/id_rsa, you can also set a custom private key address.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e81e65229c1b45afa1dc8c36cf433d43~tplv-goo7wpa0wc-image.image" width="1992px" /></div>



3. On the next page of the wizard, set the remote IDE version and the remote code directory.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b05d7efc94314f8298cd60ac6fa57a76~tplv-goo7wpa0wc-image.image" width="2000px" /></div>



4. Connect to the remote code repository.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0df3c92ba954c078fe23a31046e95fb~tplv-goo7wpa0wc-image.image" width="1956px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed steps, refer to: <a href="https://www.jetbrains.com/zh-cn/help/pycharm/remote-development-starting-page.html#start_from_IDE">Connect to a remote server from PyCharm | PyCharm</a>.</div>


<span id="c23424e4"></span>
## Caution

If the local private key is stored in the default path and the path is specified in the environment, you can directly use the login command provided by LAS. If it is not saved to the default path, use the following command to log in:

```Bash
ssh -i ~/xxx/${ssh private key name} -p ${Developer computer port} root@${CLB public network IP}
# "~/xxx/${ssh private key name}" is the path where you store your SSH private key
ssh -i ~/.ssh/las_rsa/new -p 1111 root@101.126.64.0
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the local private key is not stored in the <code>~/.ssh/</code> default path, use</div>


<div data-tips="true" data-tips-type="warning"><code>ssh -i ~/xxx/private key file -p port number username@server address</code> command to log in to the development machine.</div>
