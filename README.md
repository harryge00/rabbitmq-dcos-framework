# rabbitmq-dcos-framework 
## Building the package

In order to build a stub-universe hosted on an S3 bucket run:
```bash
export HTTP_HOST=<172.16.24.16> # please make sure the IP is accessable from dc/os master
./frameworks/rabbitmq/build.sh local
```

```bash
export S3_BUCKET=<BUCKET_NAME>	# Configure aws-cli first.
./frameworks/rabbitmq/build.sh aws
```

```bash
export S3_BUCKET=<BUCKET_NAME>	# Configure aws-cli first.
./frameworks/rabbitmq/build.sh .dcos
```


## Clustering Guide

`rabbit_peer_discovery_classic_config` is used. The `rabbitmq.conf` looks like:
```
loopback_users.guest = false
total_memory_available_override_value = 3279945728
listeners.tcp.default = 5672
default_pass = password
default_user = admin
management.tcp.port = 15672
cluster_formation.peer_discovery_backend = rabbit_peer_discovery_classic_config
cluster_formation.classic_config.nodes.0 = rabbit@rabbitmq-0-server.mqcluster1.autoip.dcos.thisdcos.directory
cluster_formation.classic_config.nodes.1 = rabbit@rabbitmq-1-server.mqcluster1.autoip.dcos.thisdcos.directory
cluster_formation.classic_config.nodes.2 = rabbit@rabbitmq-2-server.mqcluster1.autoip.dcos.thisdcos.directory
```
This config is generated dynamically. So when scaling, the peer node list will also be updated.

## Quickstart
1. Build the docker image before deploying the framework:
```
docker build -t hyge/rabbitmq:3.7.17-cluster -f frameworks/rabbitmq/src/main/docker/Dockerfile frameworks/rabbitmq/src/main/docker
```

## TODO
1. Add the "docker-entrypoint.sh" as template, so no need to build image.