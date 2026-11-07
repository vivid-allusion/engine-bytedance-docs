---
title: "HPC - Setting up Slurm compute cluster"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/HPC_-_Building_Slurm_computing_clusters"
---

This topic describes how to set up a Slurm compute cluster on HPC\-optimized instances.

## Overview

### What is Slurm?

Simple Linux Utility for Resource Management (Slurm) is an open\-source, fault\-tolerant, and highly scalable cluster management and job scheduling system, suitable for both large and small Linux clusters. It operates without requiring kernel modifications and is relatively self\-contained. As a cluster workload manager, Slurm offers three core features:

* Allocates exclusive or non\-exclusive access to resources (compute nodes) for users over a specified period, enabling the resources to execute workloads.

* Provides a framework for initiating, executing, and monitoring workloads (typically parallel workloads) on the allocated set of nodes.

* Arbitrates resource contention by managing a queue of pending workloads.

### Architecture diagram

> Architecture diagram source: [Slurm official website](https://slurm.schedmd.com/).

![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e62cb73bcf8fc4d1b2a133f7996a0902)

* Controller daemon (slurmctld): The central service of the resource management system, responsible for resource status maintenance, resource allocation, job scheduling, and job management/control.

* Node monitoring process (slurmd): Runs on each compute node. It collects resource status on the node and reports it to the controller daemon, while also receiving requests from the controller daemon and user commands to perform operations such as job step loading and job cancellation.

* slurmdbd: The middleware for command\-line tools and the control process to access the database. It provides a unified interface for accessing data and associated information, while enabling user authentication and security isolation.

* The client commands include:

   * sbatch: Submits single\-node and multi\-node Slurm jobs.

   * srun: Run jobs.

   * scancel: Terminates pending or running jobs.

   * sinfo: Views system status.

   * squeue: Views job status.

   * sacct: Views information about running or completed jobs and job steps.

   * scontrol: A management tool for monitoring and modifying cluster configurations and status information.

   * sacctmgr: Used for database management, enabling authentication and administration of clusters, valid users, and valid billing accounts.

### Preparations

Prepare three HPC\-optimized instances to serve as the management node and compute nodes, and perform the following operations on each node. Assume the configuration information for each node is as follows:

* Operating system: CentOS 7.8

* Instance specifications: 4 vCPU, 16 GB memory, 300 GB data disk

* Database specifications: MySQL, 2 vCPU, 4 GB memory, 100 GB data disk

* Compute node 1: C1, 192.168.0.32

* Compute node 2: C2, 192.168.0.159

* Management node: M1, 192.168.0.65

1. Execute the following commands on each of the three nodes to specify the hostname:

   ```Plain Text
   hostnamectl set-hostname m1
   hostnamectl set-hostname c1
   hostnamectl set-hostname c2
   ```

2. Delete the installed Slurm. If Slurm was not previously installed, skip this step.

   * Delete the database.

      ```Plain Text
      yum remove mariadb-server mariadb-devel -y
      ```

   * Remove Slurm and Munge.

      ```Plain Text
      yum remove slurm munge munge-libs munge-devel -y
      ```

   * Delete the user and corresponding folders.

      ```Plain Text
      userdel -r slurm
      suerdel -r munge
      ```

3. Disable firewall.

   ```Plain Text
   systemctl stop firewalld
   systemctl disable firewalld
   systemctl stop iptables
   systemctl disable iptables
   ```

4. Modify resource limits.

   1. Execute the following command to open the file.

      ```Plain Text
      vim /etc/security/limits.conf
      ```

   2. Add the following content below "End of file", as shown in the figure below.

      ```Plain Text
      - nofile 655360
      - nproc 655350
      ```

      ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b9f5425e63f478e0a9a68016623a7c3d)

5. Configure the time zone and synchronize the cluster clock.

   ```Plain Text
   ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
   ```

6. Install and configure the NTP server.

   1. Install the NTP server.

      ```Plain Text
      yum install ntp -y
      systemctl enable ntpd.service
      ntpdate pool.ntp.org
      systemctl start ntpd
      ```

   2. Synchronize the NTP server.

      ```Plain Text
      yum install ntp -y
      systemctl start ntpd
      systemctl enable ntpd
      ```

   3. Install the EPEL repository.

      ```Plain Text
      yum install http://mirrors.sohu.com/fedora-epel/epel-release-latest-7.noarch.rpm
      ```

7. Install and configure NFS on the control node M1.

   1. Install NFS.

      ```Plain Text
      yum -y install nfs-utils rpcbind
      ```

   2. Create the exports file.

      1. Execute the following command to create and open the file.

         ```Plain Text
         vim /etc/exports
         ```

      2. Add the following content.

         ```Plain Text
         /software/ *(rw,async,insecure,no_root_squash)
         ```

   3. Start NFS.

      ```Plain Text
      systemctl start nfs
      systemctl start rpcbind
      systemctl enable nfs
      systemctl enable rpcbind
      ```

   4. View the NFS status.

      ```java
      systemctl status nfs
      ```

      If the following output is displayed, the installation is successful.

      ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_08bb041255340478e05bf416e278d9b4)

8. Edit local static resolution.

   1. Execute the following command to open the local hosts file.

      ```Plain Text
      vi /etc/hosts
      ```

   2. Write the following content into the file, and replace the IP addresses and hostnames with the actual ones in your environment:

      ```Plain Text
      192.168.0.253  m1
      192.168.0.65   c1
      192.168.0.191  c2
      ```

9. Perform passwordless authentication.

   1. Generate a key.

      ```Plain Text
      ssh-keygen
      ```

      After you press the Enter key repeatedly as prompted, the following output is displayed:

      ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_0aeaa7b89836d26732d8a7be1db1b02b)

   2. Copy the key to compute nodes C1 and C2.

      ```Plain Text
      ssh-copy-id -i .ssh/id_rsa.pub c1
      ssh-copy-id -i .ssh/id_rsa.pub c2
      ```

      During the process, enter the login passwords for the compute nodes.

      ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c42c2a0262aea458ad7aaf01d254ee0c)

   3. Log in to the compute nodes again to confirm that no passwords are required, indicating successful passwordless authentication.

      ```Plain Text
      ssh root@c1
      ssh root@c2
      ```

## Step 1: Install Munge

Both Slurm and Munge require that the UIDs and GIDs are consistent across all nodes in the cluster. Log in to each node and install Munge.

1. Create a global user.

   ```Plain Text
   export MUNGEUSER=991
   groupadd -g $MUNGEUSER munge
   useradd  -m -c "MUNGE Uid 'N' Gid Emporium" -d /var/lib/munge -u $MUNGEUSER -g munge  -s /sbin/nologin munge
   ```

2. Install Munge.

   1. Install the EPEL repository.

      ```Plain Text
      yum install epel-release
      ```

   2. Install Munge.

      ```Plain Text
      yum install munge munge-libs munge-devel -y
      ```

   3. Install the rng tool.

      ```Plain Text
      yum install rng-tools -y 
      ```

   4. Create a new key and configure permissions on the control node M1.

      ```Plain Text
      /usr/sbin/create-munge-key -r
      dd if=/dev/urandom bs=1 count=1024 > /etc/munge/munge.key 
      chown munge: /etc/munge/munge.key 
      chmod 400 /etc/munge/munge.key
      ```

   5. Send the generated key to compute nodes C1 and C2.

      ```Plain Text
      scp /etc/munge/munge.key root@c1:/etc/munge
      scp /etc/munge/munge.key root@c2:/etc/munge
      ```

      After you enter "yes" and the compute node password, a message indicating that the key has been sent successfully appears, as shown in the figure below.

      ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a446701936de4c81c83976cd155acf0e)

   6. Modify permissions on management node M1 and compute nodes C1 and C2.

      ```Plain Text
      chown -R munge: /etc/munge/ /var/log/munge/ 
      chmod 0700 /etc/munge/ /var/log/munge/
      systemctl enable munge 
      systemctl restart munge
      ```

3. Check the Munge status.

   ```Plain Text
   systemctl restart munge
   systemctl status munge
   ```

4. Execute the following commands on the management node M1 to verify whether Munge has been installed successfully and to check connectivity between the management node and each compute node.

   ```Plain Text
   munge -n 
   munge -n | unmunge 
   munge -n | ssh c1 unmunge
   munge -n | ssh c2 unmunge
   ```

   If the following output is displayed, the installation is successful.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_8768ddf21c18a85ad5a53312d73ae568)

## Step 2: Install Slurm

Log in to each node to install Slurm.

1. Create the Slurm user.

   ```Plain Text
   groupadd -g 1109 slurm
   useradd -m -c "Slurm manager" -d /var/lib/slurm -u 1109 -g slurm -s /bin/bash slurm
   ```

2. Install dependencies.

   ```Bash
   yum install  openssl openssl-devel pam-devel numactl numactl-devel hwloc hwloc-devel lua lua-devel readline-devel rrdtool-devel ncurses-devel man2html libibmad libibumad -y
   yum install  gcc gcc-c++ readline-devel perl-ExtUtils-MakeMaker pam-devel rpm-build mysql-devel -y
   ```

3. Download and install Slurm.

   1. Install Slurm.

      ```Bash
      wget https://download.schedmd.com/slurm/slurm-20.02.7.tar.bz2
      ```

   2. Install rpmbuild to compile Slurm and create an rpm package.

      ```Plain Text
      yum install rpm-build
      rpmbuild -ta slurm-20.02.7.tar.bz2
      ```

   3. Go to the rpm package directory and install Slurm.

      ```Plain Text
      cd /root/rpmbuild/RPMS/x86_64
      yum localinstall slurm-*
      ```

## Step 3: Configure the management node

1. Log in to the management node M1 and create the relevant files.

   ```Bash
   mkdir /var/spool/slurmctld
   chown slurm: /var/spool/slurmctld
   chmod 755 /var/spool/slurmctld
   touch /var/log/slurmctld.log
   chown slurm: /var/log/slurmctld.log
   touch /var/log/slurm_jobacct.log /var/log/slurm_jobcomp.log
   chown slurm: /var/log/slurm_jobacct.log /var/log/slurm_jobcomp.log
   mkdir /var/spool/slurm
   chown slurm:slurm /var/spool/slurm
   chmod 755 /var/spool/slurm
   mkdir -p /var/spool/slurm/cluster_state
   chown slurm:slurm /var/spool/slurm/cluster_state
   ```

2. Edit the management node configuration file.

   1. Open the file.

      ```Bash
      vi /etc/slurm/slurm.conf
      ```

      Enter the following content.

      ```Bash
      #
      # Example slurm.conf file. Please run configurator.html
      # (in doc/html) to build a configuration file customized
      # for your environment.
      #
      #
      # slurm.conf file generated by configurator.html.
      #
      # See the slurm.conf man page for more information.
      #
      ClusterName=test
      ControlMachine=m1
      ControlAddr=192.168.0.65 #Management node IP
      #BackupController=
      #BackupAddr=
      #
      SlurmUser=slurm
      #SlurmdUser=root
      SlurmctldPort=6817
      SlurmdPort=6818
      AuthType=auth/munge
      #JobCredentialPrivateKey=
      #JobCredentialPublicCertificate=
      StateSaveLocation=/var/spool/slurmctld
      SlurmdSpoolDir=/var/spool/slurm/d
      SwitchType=switch/none
      MpiDefault=none
      SlurmctldPidFile=/var/run/slurmctld.pid
      SlurmdPidFile=/var/run/slurmd.pid
      ProctrackType=proctrack/pgid
      #PluginDir=
      #FirstJobId=
      ReturnToService=0
      #MaxJobCount=
      #PlugStackConfig=
      #PropagatePrioProcess=
      #PropagateResourceLimits=
      #PropagateResourceLimitsExcept=
      #Prolog=
      #Epilog=
      #SrunProlog=
      #SrunEpilog=
      #TaskProlog=
      #TaskEpilog=
      #TaskPlugin=
      #TrackWCKey=no
      #TreeWidth=50
      #TmpFS=
      #UsePAM=
      #
      # TIMERS
      SlurmctldTimeout=300
      SlurmdTimeout=300
      InactiveLimit=0
      MinJobAge=300
      KillWait=30
      Waittime=0
      #
      # SCHEDULING
      SchedulerType=sched/backfill
      #SchedulerAuth=
      SelectType=select/cons_tres
      SelectTypeParameters=CR_Core
      #PriorityType=priority/multifactor
      #PriorityDecayHalfLife=14-0
      #PriorityUsageResetPeriod=14-0
      #PriorityWeightFairshare=100000
      #PriorityWeightAge=1000
      #PriorityWeightPartition=10000
      #PriorityWeightJobSize=1000
      #PriorityMaxAge=1-0
      #
      # LOGGING
      SlurmctldDebug=info
      SlurmctldLogFile=/var/log/slurmctld.log
      SlurmdDebug=info
      SlurmdLogFile=/var/log/slurmd.log
      JobCompType=jobcomp/none
      #JobCompLoc=
      #
      # ACCOUNTING
      JobAcctGatherType=jobacct_gather/linux
      #JobAcctGatherFrequency=30
      #
      AccountingStorageType=accounting_storage/slurmdbd
      #AccountingStorageHost=
      #AccountingStorageLoc=
      #AccountingStoragePass=
      #AccountingStorageUser=
      #
      # COMPUTE NODES
      NodeName=c[1-2] Procs=1 State=UNKNOWN
      PartitionName=debug Nodes=ALL Default=YES MaxTime=INFINITE State=UP
      ```

3. Send the edited configuration file to compute nodes C1 and C2.

   ```Bash
   scp /etc/slurm/slurm.conf root@c1:/etc/slurm/
   scp /etc/slurm/slurm.conf root@c2:/etc/slurm/
   ```

4. Log in to the BytePlus console to configure the RDS service.

   1. Create an instance and select version 5.7. Take note that the RDS instance must be in the same region, availability zone, and VPC as the HPC\-optimized instance.

   2. Add the IP address of management node M1 to the allowlist of the RDS instance. As shown in the figure below, select the "Security" tab, click the "Modify" button, add the IP address of M1, and then click the "OK" button.

   3. Create a database named slurm_acct_db, which is used by Slurmctld to access data via Slurmdbd. As shown in the figure below, select the "Databases" tab, click the "Create database" button, enter the database name, select the character set, and then click the "OK" button.

5. Configure the slurmdbd.conf file.

   1. Create the systemd file.

      ```Plain Text
      cp /usr/lib/systemd/system/slurmctld.service /usr/lib/systemd/system/slurmd.service /usr/lib/systemd/system/slurmdbd.service /etc/systemd/system/
      cat /etc/systemd/system/slurmctld.service
      ```

   2. Configure the slurmdbd.conf file.

      ```Plain Text
      cp /etc/slurm/slurmdbd.conf.example /etc/slurm/slurmdbd.conf
      chown slurm: /etc/slurm/slurmdbd.conf
      chmod 600 /etc/slurm/slurmdbd.conf
      mkdir /var/log/slurm/
      touch /var/log/slurm/slurmdbd.log
      chown slurm: /var/log/slurm/slurmdbd.log
      vi /etc/slurm/slurmdbd.conf
      ```

      Enter the following content in the slurmdbd.conf configuration file.

      ```Bash
      #
      # Example slurmdbd.conf file.
      #
      # See the slurmdbd.conf man page for more information.
      #
      # Archive info
      #ArchiveJobs=yes
      #ArchiveDir="/tmp"
      #ArchiveSteps=yes
      #ArchiveScript=
      #JobPurge=12
      #StepPurge=1
      #
      # Authentication info
      AuthType=auth/munge
      #AuthInfo=/var/run/munge/munge.socket.2
      #
      # slurmDBD info
      DbdAddr=localhost
      DbdHost=localhost
      DbdPort=6819
      SlurmUser=slurm
      #MessageTimeout=300
      DebugLevel=verbose
      #DefaultQOS=normal,standby
      LogFile=/var/log/slurm/slurmdbd.log
      PidFile=/var/run/slurmdbd.pid
      #PluginDir=/usr/lib/slurm
      #PrivateData=accounts,users,usage,jobs
      #TrackWCKey=yes
      #
      # Database info
      StorageType=accounting_storage/mysql
      StorageHost=mysql3dd7de4bfd19.rds.ivolces.com # Database instance intranet address
      StoragePort=3306 # Intranet port
      StoragePass=AihymTs4X*7z*QGp # Database instance Password
      StorageUser=zxd-slurm # Account name
      StorageLoc=slurm_acct_db # Database name
      ```

6. Start the SlurmDBD service.

   ```Plain Text
   systemctl enable slurmdbd
   systemctl start slurmdbd
   systemctl status slurmdbd
   ```

7. Start the slurmctl service.

   ```Plain Text
   systemctl enable slurmctld.service
   systemctl start slurmctld.service
   systemctl status slurmctld.service
   ```

## Step 4: Configure Slurm compute nodes

1. Create the /etc/slurm/ directory on compute nodes C1 and C2, respectively.

   ```Plain Text
   mkdir /var/spool/slurmd
   chown slurm: /var/spool/slurmd
   chmod 755 /var/spool/slurmd
   touch /var/log/slurmd.log
   chown slurm: /var/log/slurmd.log
   ```

2. Start the Slurm service on compute nodes C1 and C2, respectively.

   ```Plain Text
   mkdir /var/spool/slurm
   mkdir /var/spool/slurm/d
   systemctl start slurmd.service
   systemctl status slurmd.service
   systemctl enable slurmd.service
   ```

## Step 5: Execute commands to test the Slurm cluster

1. Display all compute nodes.

   ```Plain Text
   scontrol show nodes
   ```

   If `State=DOWN` is displayed for the compute nodes, execute the following command to change their status to `IDLE`:

   ```Plain Text
   scontrol update nodename=cas01 state=resume
   ```

2. Edit the test script.

   ```Plain Text
   vim "day 1".sh
   ```

   Paste the following content into the file, and then save and exit the file.

   ```Plain Text
   #!/bin/bash
   sleep 30
   echo "always day 1 $(hostname)"
   ```

3. Execute the following command on compute nodes C1 and C2.

   ```Plain Text
   cat slurm-X.out
   ```

4. Execute the test script on the management node M1.

   ```Plain Text
   sbatch "day 1".sh
   squeue
   ```

5. If the output from the management node and test nodes is as follows, the cluster has been deployed successfully.![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_105d584ef1e104b800ecc83b3b1aec1b)If the following output is displayed, the cluster is deployed successfully.

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_c1be5c11fb3b3622266cda18915bf22d)

   ![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9f54bdf0c8859072bc53237602f0dd79)

## Appendix: Basic Slurm operation commands

You can visit the [Slurm official website](https://slurm.schedmd.com/) to view basic operation commands.
