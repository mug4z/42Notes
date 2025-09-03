---
id: Docker Compose Networks
aliases: []
tags:
  - Docker
  - compose
  - network
---

[[Docker compose]]

Network make sure that a container can communicate with other container.

>[!info]
Lists of drivers
[Docker network drivers](https://docs.docker.com/engine/network/drivers/)

> [!note] Note
> The example below make us of two networks Linux and Linux2, which separate the two containers

```yaml
# Liste of services
services:
  # A services name ?
  Linux:
    # Image name 
    image: testcompose:latest
    build: ./
    networks:
      - Linux
    stdin_open: true
    tty: true

  Linux2:
    image: testcompose:latest
    depends_on:
      - Linux
    networks:
      - Linux2
    stdin_open: true
    tty: true

networks:
  Linux:
    driver: bridge
  Linux2:
    driver: bridge
```

## Sources
[[Docker - Sources]]

