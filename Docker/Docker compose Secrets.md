[[Docker compose]]

>[!note] Note
>The secrets are in  /run/secrets/name_of_the_secrets

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
    environment:
       MYSQL_ROOT_PASSWORD_FILE: /run/secrets/db-pwd
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
    secrets:
      - db-pwd
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

secrets:
  db-pwd:
    file: ./db-pwd
```

## Sources
[[Docker - Sources]]

#Docker #compose #secrets
