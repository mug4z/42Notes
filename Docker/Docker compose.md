!! ATENTION AU VOLUME PERSISTANT
## Goal
Define and manage multi-container apps in one YAML file, streamlining orchestration and replication.
## Use cases example
- Automated test environments : you can build environement and destroy it with a few commands.

## How it works
Needs an [[YAML]] compose file. (e.g. compose.yaml)
### The compose file
By default it's `compose.yaml` or `compose.yml`
The `docker-compose.yaml` and `docker-compose.yaml` is also supported.
If both files exist, Compose prefers the `compose.yaml`
## CLI
- Start 
```console
 $ docker compose up
```
- Stop
```console
 $ docker compose down
```

 - Start with a specific yaml file
```console
 $ docker compose -f file.yaml up
```
- Stop with a specific file
```console
$ docker compose -f file.yaml down
```

## Services
[[Docker Compose Services]]

## Networks
[[Docker Compose Networks]]

## Volumes
[[Docker compose Volumes]]

## Secrets
[[Docker compose Secrets]]


https://docs.docker.com/reference/compose-file/secrets/
## to Be define

https://docs.docker.com/reference/compose-file/configs/


https://docs.docker.com/reference/cli/docker/compose/

## Sources
[[Docker - Sources]]

#Docker #compose