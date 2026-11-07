---
title: "Ray integration with log service TLS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_integration_with_log_service_TLS"
---

<span id="9ec0ceeb"></span>
## Preparatory work


1. Enable [TLS](https://console.volcengine.com/tls/region:tls+cn-beijing/project?projectName=default) and create projects and topics

2. Configure indexes under the corresponding topic, adding jobId, submitId, and workerId

3. Install the log\-collector component and upgrade to the latest version on the [VKE component management](https://console.volcengine.com/vke/region:vke+cn-beijing/cluster/ccnfhgu0ocuoaj0l5iqmg/addon) page


<span id="e86bd0a0"></span>
## Introduction to log information in Ray

When starting a ray job submit task, the task generates the following logs:


|File name |Log content |Example |
|---|---|---|
|job\-driver\-raysubmit_\*.log<br><br>Example: job\-driver\-raysubmit_JWQCshmQFcQcpN3i.log |Client submission log |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef0c5cea3ed24c2ba3d9f1003bc5c4c9~tplv-goo7wpa0wc-image.image) </span> |
|runtime_env_setup\-xxx.log<br><br>Example: runtime_env_setup\-02000000.log |Runtime environment storage information |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8530d873d2da4b71acaf943223313309~tplv-goo7wpa0wc-image.image) </span> |
|python\-core\-driver\-\*.log<br><br>Example: python\-core\-driver\-02000000ffffffffffffffffffffffffffffffffffffffffffffffff_261.log |Driver\-side log |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91448770266c46e293b69953004c5a94~tplv-goo7wpa0wc-image.image) </span> |
|worker\-xxx\-$(id)\-xx.err<br><br>worker\-xxx\-$(id)\-xx.out<br><br>Example: worker\-0c408bdf249f9b2fde1abf5d34a80c88cb2f97ad159caf145964a67a\-02000000\-3352.out<br><br>worker\-0c408bdf249f9b2fde1abf5d34a80c88cb2f97ad159caf145964a67a\-02000000\-3352.err |Worker log |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20ac0c80d45f495ebf8e8c1443bd25cd~tplv-goo7wpa0wc-image.image) </span> |
|python\-core\-worker\-\*.log<br><br>Example: python\-core\-worker\-0c408bdf249f9b2fde1abf5d34a80c88cb2f97ad159caf145964a67a_3352.log |Worker logs |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12c13220f0b94b54ab87452860f8bd86~tplv-goo7wpa0wc-image.image) </span> |
|gcs_server.\* |GCS logs | |


<span id="fbb1265a"></span>
## Log integration configuration

Create a new collection rule on the VKE cluster \- Log Center \- Log Collection Rules page

Since there are multiple log formats and different collection rules, multiple rules need to be configured here

When creating a new rule, select the newly created TLS project and log

Each set of rules requires configuration of K8s collection rules

app.kubernetes.io/instance ray\-cluster

<span id="480f12f1"></span>
### Dashboard log

Collection path:

```Shell
/tmp/ray/session_*/logs/dashboard*
```


Log sample

```Shell
2024-03-16 16:22:03,644 INFO metrics_agent.py:286 -- Metrics from a worker (8b330b47e5e538cb97c8f55092cec27bfceee0cf089da84bc7a5d1f3) is cleaned up due to timeout. Time since last report 120.52756787417457s
2024-03-16 16:23:04,414 ERROR optional_utils.py:293 -- Unexpected error in handler: Cannot write to closing transport
Traceback (most recent call last):
  File "/home/ray/.conda/envs/ray/lib/python3.10/site-packages/ray/dashboard/optional_utils.py", line 291, in decorator
    return await f(self, *args, **kwargs)
  File "/home/ray/.conda/envs/ray/lib/python3.10/site-packages/ray/dashboard/modules/job/job_agent.py", line 193, in tail_job_logs
    await ws.send_str(lines)
  File "/home/ray/.conda/envs/ray/lib/python3.10/site-packages/aiohttp/web_ws.py", line 335, in send_str
    await self._writer.send(data, binary=False, compress=compress)
  File "/home/ray/.conda/envs/ray/lib/python3.10/site-packages/aiohttp/http_websocket.py", line 729, in send
    await self._send_frame(message, WSMsgType.TEXT, compress)
  File "/home/ray/.conda/envs/ray/lib/python3.10/site-packages/aiohttp/http_websocket.py", line 682, in _send_frame
    self._write(header + message)
  File "/home/ray/.conda/envs/ray/lib/python3.10/site-packages/aiohttp/http_websocket.py", line 702, in _write
    raise ConnectionResetError("Cannot write to closing transport")
ConnectionResetError: Cannot write to closing transport
2024-03-16 16:23:04,415 INFO web_log.py:211 -- 192.168.0.26 [16/Mar/2024:16:20:25 +0800] "GET /api/job_agent/jobs/raysubmit_bAzBtNgnRMgkSuEG/logs/tail HTTP/1.1" 500 0 "-" "Python/3.10 aiohttp/3.9.3"
```


First line regular expression

```Shell
\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


<span id="9d3d9f55"></span>
### GCS log

Collection path

```Shell
/tmp/ray/session_*/logs/gcs_server*
```


Log sample

```Shell
[2024-03-14 19:21:59,582 I 24 24] (gcs_server) gcs_server.cc:846: Event stats:


Global stats: 32 total (18 active)
Queueing time: mean = 6.000 ms, max = 64.021 ms, min = 1.671 us, total = 191.992 ms
Execution time:  mean = 2.004 ms, total = 64.122 ms
Event stats:
        GcsInMemoryStore.Put - 6 total (3 active), Execution time: mean = 10.672 ms, total = 64.033 ms, Queueing time: mean = 10.617 ms, max = 63.697 ms, min = 1.671 us, total = 63.702 ms
        InternalKVGcsService.grpc_client.InternalKVPut - 6 total (6 active), Execution time: mean = 0.000 s, total = 0.000 s, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        GcsInMemoryStore.GetAll - 5 total (0 active), Execution time: mean = 5.677 us, total = 28.383 us, Queueing time: mean = 24.712 us, max = 28.782 us, min = 21.689 us, total = 123.559 us
        InternalKVGcsService.grpc_server.InternalKVPut - 4 total (4 active), Execution time: mean = 0.000 s, total = 0.000 s, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        InternalKVGcsService.grpc_server.InternalKVPut.HandleRequestImpl - 4 total (1 active), Execution time: mean = 8.098 us, total = 32.392 us, Queueing time: mean = 44.057 us, max = 60.544 us, min = 55.316 us, total = 176.230 us
        PeriodicalRunner.RunFnPeriodically - 4 total (2 active, 1 running), Execution time: mean = 4.667 us, total = 18.669 us, Queueing time: mean = 31.997 ms, max = 64.021 ms, min = 63.966 ms, total = 127.988 ms
        GcsInMemoryStore.Get - 1 total (0 active), Execution time: mean = 8.677 us, total = 8.677 us, Queueing time: mean = 2.324 us, max = 2.324 us, min = 2.324 us, total = 2.324 us
        ClusterResourceManager.ResetRemoteNodeView - 1 total (1 active), Execution time: mean = 0.000 s, total = 0.000 s, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        RayletLoadPulled - 1 total (1 active), Execution time: mean = 0.000 s, total = 0.000 s, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s


[2024-03-14 19:21:59,583 I 24 24] (gcs_server) gcs_server.cc:847: GcsTaskManager Event stats:
```


First line regular expression:

```Shell
\[\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


<span id="7439f6ab"></span>
### raysubmit

Collection path

```Shell
/tmp/ray/session_*/logs/job-driver-raysubmit*
```


File sample

```Shell
2024-03-16 16:17:48,360 INFO worker.py:1540 -- Connecting to existing Ray cluster at address: 192.168.0.26:6379...
2024-03-16 16:17:48,366 INFO worker.py:1715 -- Connected to Ray cluster. View the dashboard at ^[[1m^[[32m192.168.0.26:8265 ^[[39m^[[22m
DeprecationWarning: `route_prefix` in `@serve.deployment` has been deprecated. To specify a route prefix for an application, pass it into `serve.run` instead.
^[[36m(ProxyActor pid=22282)^[[0m INFO 2024-03-16 16:17:52,005 proxy 192.168.0.26 proxy.py:1143 - Proxy actor 3ea43c4b93176981b6c12a1e17000000 starting on node ce22d6b42fd3df5ce0ecd2799287a87da1dfbda85ca591bc30428d00.
^[[36m(ProxyActor pid=22282)^[[0m INFO 2024-03-16 16:17:52,009 proxy 192.168.0.26 proxy.py:1357 - Starting HTTP server on node: ce22d6b42fd3df5ce0ecd2799287a87da1dfbda85ca591bc30428d00 listening on port 8000
^[[36m(ProxyActor pid=22282)^[[0m INFO:     Started server process [22282]
^[[36m(ServeController pid=22226)^[[0m INFO 2024-03-16 16:17:52,200 controller 22226 deployment_state.py:1547 - Deploying new version of deployment BoostingModel in application 'default'. Setting initial target number of replicas to 1.
^[[36m(ServeController pid=22226)^[[0m INFO 2024-03-16 16:17:52,302 controller 22226 deployment_state.py:1831 - Adding 1 replica to deployment BoostingModel in application 'default'.
{"result":"versicolor"}
^[[36m(ServeReplica:default:BoostingModel pid=22335)^[[0m Received http request with data [1.2, 1.0, 1.1, 0.9]
^[[36m(ServeReplica:default:BoostingModel pid=22335)^[[0m INFO 2024-03-16 16:17:55,188 default_BoostingModel xQuXbM 9809fe8a-5c91-448f-be90-35fe3dab8a15 /iris replica.py:772 - __CALL__ OK 5.2ms
```


First line regular expression

```Shell
\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


Parse collection path:

Collection path sample

```Shell
/tmp/ray/session_2024-03-14_19-21-59_498571_8/logs/job-driver-raysubmit_1388WhQ575piY84f.log
```


Extraction regular expression

```Shell
/tmp/ray/session_.*/logs/job-driver-(raysubmit_[A-Za-z0-9]*)\.log
```


Extraction result: submitId

<span id="8fe3ba6b"></span>
### monitor

Collection path

```Shell
/tmp/ray/session_*/logs/monitor*
```


File sample

```Shell
2024-03-14 19:22:06,072 INFO autoscaler.py:426 --
======== Autoscaler status: 2024-03-14 19:22:06.072033 ========
Node status
---------------------------------------------------------------
Active:
 1 node_ce22d6b42fd3df5ce0ecd2799287a87da1dfbda85ca591bc30428d00
Pending:
 (no pending nodes)
Recent failures:
 (no failures)

Resources
---------------------------------------------------------------
Usage:
 0.0/2.0 CPU
 0.0/1.0 GPU
 0B/9.31GiB memory
 0B/2.70GiB object_store_memory

Demands:
 (no resource demands)
2024-03-14 19:22:06,072 INFO autoscaler.py:469 -- The autoscaler took 0.001 seconds to complete the update iteration.
```


First line regular expression

```Shell
\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


<span id="89687438"></span>
### Core driver log

Collection path

```Shell
/tmp/ray/session_*/logs/python-core-driver-*
```


File format

```Shell
[2024-03-14 19:23:38,356 I 788 788] core_worker.cc:2737: Creating actor: 548cb9bd733042def4f87ccf03000000
[2024-03-14 19:23:41,264 I 788 788] direct_actor_transport.cc:188: Actor creation task finished, task_id: ffffffffffffffff548cb9bd733042def4f87ccf03000000, actor_id: 548cb9bd733042def4f87ccf03000000, actor_repr_name:
[2024-03-14 19:24:38,355 I 788 817] core_worker.cc:588: Event stats:


Global stats: 946 total (8 active)
Queueing time: mean = 62.903 us, max = 38.679 ms, min = 8.188 us, total = 59.506 ms
Execution time:  mean = 32.356 ms, total = 30.609 s
Event stats:
        CoreWorker.RecoverObjects - 600 total (1 active), Execution time: mean = 3.418 us, total = 2.051 ms, Queueing time: mean = 88.084 us, max = 38.679 ms, min = 9.317 us, total = 52.850 ms
        CoreWorker.ExitIfParentRayletDies - 61 total (1 active), Execution time: mean = 7.183 us, total = 438.167 us, Queueing time: mean = 24.236 us, max = 41.793 us, min = 11.091 us, total = 1.478 ms
        NodeManagerService.grpc_client.ReportWorkerBacklog - 60 total (0 active), Execution time: mean = 394.125 us, total = 23.648 ms, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        CoreWorker.InternalHeartbeat - 60 total (1 active), Execution time: mean = 86.542 us, total = 5.193 ms, Queueing time: mean = 27.382 us, max = 398.484 us, min = 9.719 us, total = 1.643 ms
        NodeManagerService.grpc_client.ReportWorkerBacklog.OnReplyReceived - 60 total (0 active), Execution time: mean = 13.998 us, total = 839.895 us, Queueing time: mean = 20.086 us, max = 29.476 us, min = 10.978 us, total = 1.205 ms
        CoreWorkerService.grpc_server.PushTask - 18 total (1 active), Execution time: mean = 1.698 s, total = 30.566 s, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        CoreWorkerService.grpc_server.PushTask.HandleRequestImpl - 18 total (0 active), Execution time: mean = 42.514 us, total = 765.250 us, Queueing time: mean = 23.470 us, max = 34.842 us, min = 12.368 us, total = 422.467 us
        CoreWorkerService.grpc_server.GetCoreWorkerStats - 12 total (0 active), Execution time: mean = 195.349 us, total = 2.344 ms, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        CoreWorkerService.grpc_server.GetCoreWorkerStats.HandleRequestImpl - 12 total (0 active), Execution time: mean = 42.440 us, total = 509.284 us, Queueing time: mean = 29.899 us, max = 74.633 us, min = 19.090 us, total = 358.783 us
        CoreWorker.RecordMetrics - 12 total (1 active), Execution time: mean = 103.716 us, total = 1.245 ms, Queueing time: mean = 13.754 us, max = 21.320 us, min = 11.162 us, total = 165.050 us
[2024-03-14 19:23:41,264 I 788 788] direct_actor_transport.cc:188: Actor creation task finished, task_id: ffffffffffffffff548cb9bd733042def4f87ccf03000000, actor_id: 548cb9bd733042def4f87ccf03000000, actor_repr_name:
```


First line regular expression

```Shell
\[\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


Collection path sample

```Shell
/tmp/ray/session_2024-03-14_19-21-59_498571_8/logs/python-core-driver-02000000ffffffffffffffffffffffffffffffffffffffffffffffff_261.log
```


Extraction regular expression

```Shell
/tmp/ray/session_.*/logs/python-core-driver-([0-9]*)fffffffffffffffffffffff.*.log
```


Extraction result: jobId

<span id="90dfe5b6"></span>
### Core worker log

File path

```Shell
/tmp/ray/session_*/logs/python-core-worker-*
```


Log sample

```Shell
[2024-03-14 19:23:38,356 I 788 788] core_worker.cc:2737: Creating actor: 548cb9bd733042def4f87ccf03000000
[2024-03-14 19:23:41,264 I 788 788] direct_actor_transport.cc:188: Actor creation task finished, task_id: ffffffffffffffff548cb9bd733042def4f87ccf03000000, actor_id: 548cb9bd733042def4f87ccf03000000, actor_repr_name:
[2024-03-14 19:24:38,355 I 788 817] core_worker.cc:588: Event stats:


Global stats: 946 total (8 active)
Queueing time: mean = 62.903 us, max = 38.679 ms, min = 8.188 us, total = 59.506 ms
Execution time:  mean = 32.356 ms, total = 30.609 s
Event stats:
        CoreWorker.RecoverObjects - 600 total (1 active), Execution time: mean = 3.418 us, total = 2.051 ms, Queueing time: mean = 88.084 us, max = 38.679 ms, min = 9.317 us, total = 52.850 ms
        CoreWorker.ExitIfParentRayletDies - 61 total (1 active), Execution time: mean = 7.183 us, total = 438.167 us, Queueing time: mean = 24.236 us, max = 41.793 us, min = 11.091 us, total = 1.478 ms
        NodeManagerService.grpc_client.ReportWorkerBacklog - 60 total (0 active), Execution time: mean = 394.125 us, total = 23.648 ms, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        CoreWorker.InternalHeartbeat - 60 total (1 active), Execution time: mean = 86.542 us, total = 5.193 ms, Queueing time: mean = 27.382 us, max = 398.484 us, min = 9.719 us, total = 1.643 ms
        NodeManagerService.grpc_client.ReportWorkerBacklog.OnReplyReceived - 60 total (0 active), Execution time: mean = 13.998 us, total = 839.895 us, Queueing time: mean = 20.086 us, max = 29.476 us, min = 10.978 us, total = 1.205 ms
        CoreWorkerService.grpc_server.PushTask - 18 total (1 active), Execution time: mean = 1.698 s, total = 30.566 s, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        CoreWorkerService.grpc_server.PushTask.HandleRequestImpl - 18 total (0 active), Execution time: mean = 42.514 us, total = 765.250 us, Queueing time: mean = 23.470 us, max = 34.842 us, min = 12.368 us, total = 422.467 us
        CoreWorkerService.grpc_server.GetCoreWorkerStats - 12 total (0 active), Execution time: mean = 195.349 us, total = 2.344 ms, Queueing time: mean = 0.000 s, max = -0.000 s, min = 9223372036.855 s, total = 0.000 s
        CoreWorkerService.grpc_server.GetCoreWorkerStats.HandleRequestImpl - 12 total (0 active), Execution time: mean = 42.440 us, total = 509.284 us, Queueing time: mean = 29.899 us, max = 74.633 us, min = 19.090 us, total = 358.783 us
        CoreWorker.RecordMetrics - 12 total (1 active), Execution time: mean = 103.716 us, total = 1.245 ms, Queueing time: mean = 13.754 us, max = 21.320 us, min = 11.162 us, total = 165.050 us
[2024-03-14 19:23:41,264 I 788 788] direct_actor_transport.cc:188: Actor creation task finished, task_id: ffffffffffffffff548cb9bd733042def4f87ccf03000000, actor_id: 548cb9bd733042def4f87ccf03000000, actor_repr_name:
```


First line regular expression

```Shell
\[\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


Collection path sample

```Shell
/tmp/ray/session_2024-03-14_19-21-59_498571_8/logs/python-core-worker-009a17774013feebeec40ff17429f237265ef3ca550a9cfe1c280074_7754.log
```


Extraction regular expression

```Shell
/tmp/ray/session_.*/logs/python-core-worker-([A-Za-z0-9]*)_.*.log
```


Extraction result: workerId

<span id="bcd4c01b"></span>
### Ray\-client log

Collection path

```Shell
/tmp/ray/session_*/logs/ray_client_server*
```


Log format

```Shell
2024-03-14 19:22:01,378 INFO server.py:885 -- Starting Ray Client server on 0.0.0.0:10001, args Namespace(host='0.0.0.0', port=10001, mode='proxy', address='192.168.0.26:6379', redis_password=None, runtime_env_agent_address='http://192.168.0.26:50711')
```


First line regular expression:

```Shell
\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


<span id="c8cd0ef0"></span>
### Raylet log

Collection path

```Shell
/tmp/ray/session_*/logs/raylet*
```


Log format

```Shell
[2024-03-14 19:22:01,572 I 211 211] (raylet) main.cc:174: Setting cluster ID to: ccbe1b0b8b55be54fbb0a0487aa1741d4ed4bad8e4c63f014f60063b
[2024-03-14 19:22:01,575 I 211 211] (raylet) io_service_pool.cc:35: IOServicePool is running with 1 io_service.
[2024-03-14 19:22:01,576 I 211 211] (raylet) store_runner.cc:32: Allowing the Plasma store to use up to 2.9011GB of memory.
[2024-03-14 19:22:01,576 I 211 211] (raylet) store_runner.cc:48: Starting object store with directory /dev/shm, fallback /tmp/ray, and huge page support disabled
[2024-03-14 19:22:01,576 I 211 242] (raylet) dlmalloc.cc:154: create_and_mmap_buffer(2901147656, /dev/shm/plasmaXXXXXX)
[2024-03-14 19:22:01,576 I 211 242] (raylet) store.cc:561: ========== Plasma store: =================
Current usage: 0 / 2.9011 GB
- num bytes created total: 0
0 pending objects of total size 0MB
- objects spillable: 0
- bytes spillable: 0
- objects unsealed: 0
- bytes unsealed: 0
- objects in use: 0
- bytes in use: 0
- objects evictable: 0
- bytes evictable: 0

- objects created by worker: 0
- bytes created by worker: 0
- objects restored: 0
- bytes restored: 0
- objects received: 0
- bytes received: 0
- objects errored: 0
- bytes errored: 0

[2024-03-14 19:22:01,578 I 211 211] (raylet) grpc_server.cc:129: ObjectManager server started, listening on port 34401.
```


First line regular expression:

```Shell
\[\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


<span id="4ce7262b"></span>
### Runtime log

Collection path

```Shell
/tmp/ray/session_*/logs/runtime_env*
```


Log collection

```Shell
2024-03-16 16:26:36,640 INFO runtime_env_agent.py:509 -- Got request from raylet to decrease reference for runtime env: {"working_dir": "gcs://_ray_pkg_7e51b6d3d9a2e7cd.zip"}.
2024-03-16 16:26:36,641 INFO runtime_env_agent.py:129 -- Unused runtime env {"working_dir": "gcs://_ray_pkg_7e51b6d3d9a2e7cd.zip"}.
2024-03-16 16:26:36,641 INFO runtime_env_agent.py:263 -- Runtime env {"working_dir": "gcs://_ray_pkg_7e51b6d3d9a2e7cd.zip"} removed from env-level cache.
```


First line regular expression

```Shell
\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


Collection path sample /tmp/ray/session_2024\-03\-14_19\-21\-59_498571_8/logs/runtime_env_setup\-01000000.log

Extraction regular expression

```Shell
/tmp/ray/session_.*/logs/runtime_env_setup-([A-Za-z0-9]*).log
```


Extraction result jobId

<div style="text-align: center">
Worker log</div>


Collection path

```Shell
/tmp/ray/session_*/logs/worker-*
```


Log sample

```Shell
[2024-03-16 10:39:15,071 E 17806 17806] logging.cc:361: *** SIGABRT received at time=1710556755 on cpu 13 ***
ray::JobSupervisor(PyEval_EvalCode+0x87) [0x591cd7] PyEval_EvalCode
ray::JobSupervisor() [0x5c2967] run_eval_code_obj
ray::JobSupervisor() [0x5bdad0] run_mod
ray::JobSupervisor() [0x45956b] pyrun_file.cold
ray::JobSupervisor(_PyRun_SimpleFileObject+0x19f) [0x5b805f] _PyRun_SimpleFileObject
ray::JobSupervisor(_PyRun_AnyFileObject+0x43) [0x5b7dc3] _PyRun_AnyFileObject
ray::JobSupervisor(Py_RunMain+0x38d) [0x5b4b7d] Py_RunMain
ray::JobSupervisor(Py_BytesMain+0x39) [0x584e49] Py_BytesMain
/lib/x86_64-linux-gnu/libc.so.6(__libc_start_main+0xf3) [0x7faf7df45083] __libc_start_main
ray::JobSupervisor() [0x584cfe]

*** SIGABRT received at time=1710556755 on cpu 13 ***
PC: @     0x7faf7df6400b  (unknown)  raise
    @     0x7faf7e281420  1491767840  (unknown)
    @     0x7faf7c13135a         80  __cxxabiv1::__terminate()
    @     0x7faf7c8d3a4a         32  std::_Sp_counted_base<>::_M_release()
    @     0x7faf7ca58bd2         96  std::_Sp_counted_ptr_inplace<>::_M_dispose()
    @     0x7faf7c8d3a4a         32  std::_Sp_counted_base<>::_M_release()
    @     0x7faf7c990032        144  std::default_delete<>::operator()()
    @     0x7faf7ca01fdb        128  ray::core::CoreWorker::~CoreWorker()
    @     0x7faf7c8d3a4a         32  std::_Sp_counted_base<>::_M_release()
    @     0x7faf7ca40154        112  ray::core::CoreWorkerProcessImpl::RunWorkerTaskExecutionLoop()
    @     0x7faf7ca4025d         32  ray::core::CoreWorkerProcess::RunTaskExecutionLoop()
    @     0x7faf7c852667         32  __pyx_pw_3ray_7_raylet_10CoreWorker_7run_task_loop()
    @           0x4ff2f4  (unknown)  method_vectorcall_NOARGS
    @ ... and at least 1 more frames
[2024-03-16 10:39:15,071 E 17806 17806] logging.cc:361: *** SIGABRT received at time=1710556755 on cpu 13 ***
```


First line regular expression

```Shell
\[?\d+-\d+-\d+\s\d+:\d+:\d+,\d+\s.*
```


Collection path sample /tmp/ray/session_2024\-03\-14_19\-21\-59_498571_8/logs/worker\-02db26fc7946af0a8de4aa4cfe923e2141a6078677d17180dda261e2\-10000000\-14731.out

Extraction regular expression

```Shell
/tmp/ray/session_.*/logs/worker-([A-Za-z0-9]*)-([A-Za-z0-9]*)-.*
```


Extraction result workerId jobId

<span id="ff2c324a"></span>
## Log query case

<span id="0792e49b"></span>
### Query all submitId

Query condition \* | SELECT DISTINCT(submitId)

<span id="5d8ffcd3"></span>
### Query logs by known submitId

Query condition submitId: "raysubmit_kE8xm63Wi36UBHaK"

<span id="98baf098"></span>
### Retrieve all workerId by known jobId

Query condition: jobId: "1b000000" | select DISTINCT(workerId)

<span id="25f15242"></span>
### Logs of a specific worker in a job

Query condition: jobId: "1b000000" AND workerId: "0ae97b84873e69ea83836a5f49b40ba55330d2875e8300820a8d2e16"

<span id="9cce2099"></span>
### Keyword search in logs of a specific job

Query condition: jobId: "1b000000" AND **content**: "GPU"
