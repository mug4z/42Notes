[[Docker compose]]

Volumes are persistent data stores implemented by the container engine.

>[!note] Note
Creates a volume named db-data that is shared between the Linux and Linux2 services
 
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
    volumes:
      - db-data:/etc/data
    stdin_open: true
    tty: true

  Linux2:
    image: testcompose:latest
    depends_on:
      - Linux
    networks:
      - Linux2
    volumes:
      - db-data:/home/yheaa
    stdin_open: true
    tty: true

networks:
  Linux:
    driver: bridge
  Linux2:
    driver: bridge

volumes:
  db-data:
```
## Sources
[[Docker - Sources]]

#Docker #compose #volumes