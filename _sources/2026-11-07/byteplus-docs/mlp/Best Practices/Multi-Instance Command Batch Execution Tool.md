---
title: "Multi-Instance Command Batch Execution Tool"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Multi-instance_command_batch_execution_tool"
---

Allrun is an alias tool provided by the machine learning platform, helping users quickly perform the same actions on all workers.


* This command is mainly used to quickly and flexibly configure the task runtime environment, e.g., software package compilation and installation.

* Do not use this command to start training tasks. When using deepspeed / horovodrun / mpirun to start training tasks, the start command should not be executed using allrun.

* Each allrun command is executed in a separate process, so allrun export will not have the expected effect. If the command to be executed needs to temporarily specify environment variables, use the `-x` parameter; for details, view [Scenario Seven](https://docs.byteplus.com/en/docs/186/53995#%E5%9C%BA%E6%99%AF%E4%B8%83-%E6%8C%87%E5%AE%9A%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F).


Since allrun is an alias of mpirun, usage can refer to the [mpirun Official Help Documentation](https://www.open-mpi.org/doc/v4.0/man1/mpirun.1.php); this article provides best practices for some common scenarios. In examples, unless otherwise specified, the default operating system is Ubuntu / Debian, the command is executed by worker0, and takes effect on all workers.

<span id="场景一-执行脚本"></span>
# Scenario 1 Execute Script

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is recommended to separate the initialization script and training script, then run the initialization script using this method, which eliminates the need to consider Shell syntax issues involved in the remaining scenarios.</div>


<div data-tips="true" data-tips-type="tip">Because Shell syntax is relatively complex, and in some scenarios it is necessary to execute multiple commands within the same session, it is recommended to write all commands to be executed into a script, e.g.: init.sh</div>


```Plain
allrun bash init.sh
```


<span id="场景二-为所有-worker-安装相同的软件包"></span>
# Scenario 2 Install the same packages for all workers

```Plain
allrun apt-get install -y pdsh
# or
allrun pip install touch
```


<span id="场景三-同时执行多条语句"></span>
# Scenario 3 Execute multiple commands simultaneously

Separate with `&&` or `||`.

```Plain
allrun bash -c "cd /workspace && touch testfile"
```


Separate with `;`.

```Plain
allrun bash -c "cd /workspace; touch testfile"
```


<span id="场景四-重定向多个-worker-的运行结果到本地文件"></span>
# Scenario 4 Redirect run results of multiple workers to a local file

```Plain
allrun hostname > all_hostname
```


Use `cat all_hostname` to view the file content.

```Plain
t-20220414214615-9rkhj-worker-0
t-20220414214615-9rkhj-worker-1
```


<span id="场景五-各-worker-通过重定向生成文件"></span>
# Scenario 5 Each worker generates files through redirection

<span id="使用各-worker-自身的环境变量"></span>
## Use each worker's own environment variables

```Plain
allrun bash -c 'echo "$MLP_HOST" > host'
```


Execute `cat host` on worker0 to view the file content.

```Plain
172.16.64.131
```


Execute `cat host` on worker1 to view the file content.

```Plain
172.16.66.155
```


<span id="使用执行命令所在-worker-的环境变量"></span>
## Use the environment variables of the worker where the command is executed

```Plain
allrun bash -c "echo $MLP_HOST > host"
```


Execute `cat host` on worker0 to view the file content.

```Plain
172.16.64.131
```


Execute `cat host` on worker1 to view the file content, whose content is also the IP of worker0.

```Plain
172.16.64.131
```


<span id="场景六-重定向生成文件包含双引号"></span>
# Scenario 6 Redirect to generate a file containing double quotes

```Plain
allrun bash -c "echo '{\"key\": \"value\"}' > test"
```


Execute `cat test` on worker0 and worker1 to view the file content; both are:

```Plain
{"key": "value"}
```


<span id="场景七-指定环境变量"></span>
# Scenario 7 Specify environment variables

```Plain
allrun -x TEST_ENV=test_env bash -c 'echo "$TEST_ENV"'
```


Because echo is executed once on worker0 and worker1 respectively, it will print:

```Plain
test_env
test_env
```
