# rabbitmq-dcos-framework 
## Building the package

In order to build a stub-universe hosted on an S3 bucket run:
```bash
export HTTP_HOST=<172.16.24.16> # please make sure the IP is accessable from dc/os master
./framework/rabbitmq/build.sh local
```

```bash
export S3_BUCKET=mbi-dcos
./framework/rabbitmq/build.sh aws
```

```bash
export S3_BUCKET=mbi-dcos
./framework/rabbitmq/build.sh .dcos
```
