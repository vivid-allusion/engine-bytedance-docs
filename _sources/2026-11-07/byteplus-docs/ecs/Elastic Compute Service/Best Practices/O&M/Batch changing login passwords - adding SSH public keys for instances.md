---
title: "Batch changing login passwords/adding SSH public keys for instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Batch-modify-instance-login-password-and-add-SSH-public-key"
---

This topic describes how to use the cloud assistant feature to change a login password or add an SSH public key in a batch for Linux ECS instances.

> To change the login password or add an SSH public key on a Linux ECS instance, you do not need to install the password plugin.


<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

If you need to change the login password for an existing Linux instance, or log in to a Linux instance with another key pair, you can use the cloud assistant feature. Specifically, this allows you to quickly complete the operations through preset public commands "Change Linux instance password" and "Add SSH public key to Linux instance" respectively.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

For the Linux instances for which you need to change the login password or add a key pair, [cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client) is installed and is in **Running** status.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the left\-side navigation pane, select "Monitoring \> Cloud assistant," then select the "Job Management" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Click the "Create a job" button to enter the Create a job page.

   > This practice only describes special configurations. For parameter details, refer to [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).   
   

   * Create a job for changing the login password

      1. For the "Execute command" section, select "Public commands" and "Change Linux instance password" in sequence.

      2. Enter the username and the new login password in the arguments `username` and `password`.

         > In the example provided in this section, the login password for the `root` account is to be changed.         
         

   * Create a job to add an SSH public key

      1. For the "Execute command" section, select "Public commands" and "Add SSH public key for Linux instance" in sequence.

      2. Enter the SSH public key to be added.

5. After the jobs are created, they are automatically executed by cloud assistant.

6. You can manually check the execution progress and results of the jobs. For detailed execution results, see [Viewing job execution results](https://docs.byteplus.com/en/docs/ecs/View-job-execution-results).

7. When the job status is **Execution successful**, you can use the new password or the private key to log in to the target instance.
