# ETCD & Monk
This repository contains Monk.io template to deploy Minio Cluster either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running.
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository
```bash
git clone https://github.com/Burakhan/monk-etcd
```

## Load Template
```bash
cd monk-etcd
monk load MANIFEST
```


#### Let's take a look at the themes I have installed.
```bash
foo@bar:~$ monk list monk-etcd
✔ Got the list
Type      Template         Repository  Version  Tags
runnable  monk-etcd/etcd1  local       -        -
runnable  monk-etcd/etcd2  local       -        -
runnable  monk-etcd/etcd3  local       -        -
group     monk-etcd/stack  local       -        -

```

## Deploy Stack
```bash
foo@bar:~$ monk run monk-etcd/stack
✔ Starting the job: local/monk-etcd/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% gcr.io/etcd-development/etcd:v3.2.10 mnk-3
✔ [================================================] 100% gcr.io/etcd-development/etcd:v3.2.10 mnk-2
✔ [================================================] 100% gcr.io/etcd-development/etcd:v3.2.10 mnk-1
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Starting containers DONE
✔ Started local/monk-etcd/stack

🔩 templates/local/monk-etcd/stack
 ├─🧊 Peer mnk-2
 │  └─🔩 templates/local/monk-etcd/etcd2
 │     └─📦 0b32d7b8369e6998c37e4d3da98e54c0-cal-monk-etcd-etcd2-monk-etcd2
 │        ├─🧩 gcr.io/etcd-development/etcd:v3.2.10
 │        └─🔌 open 13.49.125.125:2392 (0.0.0.0:2392) -> 2379
 ├─🧊 Peer mnk-1
 │  └─🔩 templates/local/monk-etcd/etcd1
 │     └─📦 aadf6524344b80f2d49b7d8d3bb9bf04-cal-monk-etcd-etcd1-monk-etcd1
 │        ├─🧩 gcr.io/etcd-development/etcd:v3.2.10
 │        └─🔌 open 13.53.139.95:2391 (0.0.0.0:2391) -> 2379
 └─🧊 Peer mnk-3
    └─🔩 templates/local/monk-etcd/etcd3
       └─📦 448d86067ccec2768e8839add8a443a9-cal-monk-etcd-etcd3-monk-etcd3
          ├─🧩 gcr.io/etcd-development/etcd:v3.2.10
          └─🔌 open 13.50.109.173:2393 (0.0.0.0:2393) -> 2379

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) local/monk-etcd/stack - Inspect logs
	monk shell     local/monk-etcd/stack - Connect to the container's shell
	monk do        local/monk-etcd/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```


## Variables
The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable                     	| Description                               	|
|------------------------------	|-------------------------------------------	|
| monk_etcd1_port               | etcd node 1 public port, Default: 2391 	    |
| monk_etcd2_port               | etcd node 1 public port, Default 2392        	|
| monk_etcd3_port               | etcd node 1 public port, Default: 2393        	|


## Stop, remove and clean up workloads and templates

```bash
monk purge -x -a
```