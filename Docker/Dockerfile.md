> [!warning] It is recommended to use the default name "Dockerfile" for the primary Dockerfile 

## Goal
The dockerfile is used with `docker build` to build an [[Docker Images|image]] with a certain configuration.

## Instructions
These are the most used instruction in a Dockerfile.

| Command    | Effect                                                                                                                         |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------ |
| FROM       | set a base image                                                                                                               |
| RUN        | Executes any commands in a new layer on top of the current image and commits the result.                                       |
| WORKDIR    | Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow it in the Dockerfile |
| COPY       | Copy new files from the src to dest where src is a file in the cwd of the Dockerfile and dest a file in the image.             |
| CMD        | Instruction sets the command to be executed when running a container from an image.                                            |
| ENTRYPOINT | Allows you to configure a container that will run as an executable.                                                            |

### Examples
> [!example] FROM
> Will build an image base on the version 3.22 of alpine
> ```Dockerfile
> FROM alpine:3.22
> ```

> [!example ] RUN
Add the gcc package using the package manger of alpine
> ```Dockerfile
> FROM alpine:3.22
> RUN  apk add gcc

> [!example ] WORKDIR
> The result of pwd will be a/b/c
> ```Dockerfile
> WORKDIR /a
> WORKDIR b
> WORKDIR c
> RUN pwd
> ```

> [!example ] COPY
> >[!note]  Note
> >You can copy mutiple files at once. The last path is always the one in the image.
> 
> Copies file1.txt and file2.txt to /usr/src/things.
> ```Dockerfile
> COPY file1.txt file2.txt /usr/src/things/
> ```

> [!example ] CMD
> > [!note] Note
> > CMD is overwrite by the docker run command argument.
> 
> Run the nvim command when the container start
> ```Dockerfile
> FROM alpine:3.22
> RUN  apk add gcc
> RUN  apk add stress-ng
> RUN  apk add neovim
> CMD ["nvim"]
> ```

The CMD can also take argument for entrypoint. 
## References
[Dockerfile References](https://docs.docker.com/reference/dockerfile/)
## Best Practices
[Building Best practices - lue le 01.08.2025](https://docs.docker.com/build/building/best-practices/)
## Source
[[Docker - Sources]]



#Docker #Dockerfile



