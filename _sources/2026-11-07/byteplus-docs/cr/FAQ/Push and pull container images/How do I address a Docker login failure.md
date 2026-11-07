---
title: "How do I address a Docker login failure"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How-do-I-address-a-Docker-login-failure"
---

Troubleshooting varies according to error messages:

<span id="报错-**docker:-command-not-found**"></span>
## Error: **docker: command not found**

Confirm whether Docker is installed. If not, refer to the [Docker official documentation](https://docs.docker.com/engine/install/centos/) to install Docker.

<span id="报错-**cannot-connect-to-the-docker-daemon-at-xxx-is-the-docker-daemon-running?**"></span>
## Error: **Cannot connect to the Docker daemon at xxx. Is the docker daemon running?** 

Start the local Docker server.

<span id="密码错误"></span>
## Password error

Ensure that the Docker logon password you entered is correct. The password for logging on to the Container Registry (CR) instance is set on the **Overview** page of the CR console, not the password for logging on to the BytePlus console.

If you forget the password for logging on to the CR instance, refer to [Changing access passwords for Enterprise Edition instances](https://docs.byteplus.com/en/docs/cr/Get-access-credentials) , change the password, then use the new password to log on again.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using <code>sudo</code> command to log on as a non\-root user, enter the password twice:</div>



* <div data-tips="true" data-tips-type="tip">The first password is the root user's password.</div>


* <div data-tips="true" data-tips-type="tip">The second password is for logging on to the CR instance.</div>
