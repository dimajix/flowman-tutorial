# Flowman Tutorial

Welcome to this tutorial for developing data transformation applications with Flowman. In a sequence of multiple
lessons, you will start learning the basic concepts of Flowman and later get known to more advanced features of
Flowman. All lessons will use a subset of a publicly available data set about weather data.

## Running Flowman in Docker

The easiest way to follow the tutorial is to use the provided `docker-compose.yml` which will start a Docker container
containing Flowman with all lessons mounted as a volume.


### Start MS SQL Server
```shell
docker-compose up -d sqlserver
```

### Start Flowman Container
```shell
docker-compose run --rm flowman bash

cd /opt/flowman
```


## 3. Running the Example

## Running the whole project

```shell
flowexec -f flow project run
```

## Interactive Shell

```shell
flowshell -f flow
```
