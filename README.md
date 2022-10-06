# docker-compose

_commands to setup local docker env for development_

Feel free to clone and make any changes if you need a quick dev env locally with Docker with a set of tools this is an easy way to get started..

# Tools within docker-compose

## 📖 Table of Contents
- mysql
  - localhost:3306
  - user|user123
- postgres
  - localhost:5432
  - dbuser|Passw0rd2
- pgadmin
  - http://localhost:5050/
  - admin@email.com|Passw0rd1
  - Add Server
    - host.docker.internal
    - dbuser|Passw0rd2
- mongodb
  - mongodb://localhost:27017
- influxdb
- eventstoredb
  - https://github.com/EventStore/EventStore-Client-Dotnet
- rabbitmq
  - docker exec -it rabbitmq bin/bash
  - rabbitmqctl add_user admin admin123
  - rabbitmqctl set_user_tags admin administrator
  - rabbitmqctl set_permissions -p / admin ".*" ".*" ".*"
  - http://localhost:15672/
- redis
  - datagrip : https://plugins.jetbrains.com/plugin/12820-redis/versions
  - eYVX7EwVmmxKPCDmwMtyKVge8oLd2t81
  - or https://github.com/qishibo/AnotherRedisDesktopManager
- zipkin
  - http://localhost:9411/zipkin/
- prometheus
  - http://localhost:9090/
- grafana
  - http://localhost:3000/login
  - admin|grafana
- ElasticSearch 3 nodes
  - https://localhost:9200/
  - elastic|elastic
- Kabana
  - http://localhost:9092/
  - elastic|elastic
- Logstash
- couchdb
  - http://localhost:5984/
  - admin|couchdb
  - UI http://localhost:5984/_utils/
- kafka 3 nodes
  - 127.0.0.1:9092,127.0.0.1:9093,127.0.0.1:9094
- kafdrop
  - http://localhost:9000
- kafka-ui
  - http://localhost:8180


# Configure Docker

## Setup

Create docker-compose

```powershell
docker-compose -f .\docker-compose.yml up
```

If using Linux:
```sh
docker-compose -f ./docker-compose.yml up
```

Taredown works on both OS:
```sh
docker-compose down -v
```

extra commands:

```sh
docker --version
```
OR
```sh
docker-compose --version
```
OR
```sh
docker ps -a
```

# Configurations

### Windows

_note: for ES you will have to do a few steps_

[wsl](https://github.com/microsoft/wslg)

Gets the list of run apps
```sh
wsl -l -v
```
To Update wsl
```sh
wsl --update
```
shutdown wsl
```sh
wsl --shutdown
```
_Restart docker desktop_ to take affect

To Install GUI tool for linux on windows

[help](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#_windows_with_docker_desktop_wsl_2_backend)

_developers linux of choice_
```sh
wsl --install -d Debian
```
Change the sysctl variable
```sh
wsl -d docker-desktop
```
To set a variable this is needed for ES as it will give an error
```sh
 ysctl -w vm.max_map_count=262144
```
To verify
```sh
sysctl vm.max_map_count
```

# Notes

_I did not add MS SQL to docker-compose as I like to use that locally installed better performance._

If someone else needs it, you can add below to docker-compose.yml:
```yml
  sqlserver:
    container_name: sqlserver
    image: mcr.microsoft.com/mssql/server:2019-latest
    environment:
      - SA_PASSWORD=${MSSQL_PASSWORD}
      - ACCEPT_EULA=Y
    ports:
      - 1433:1433
```