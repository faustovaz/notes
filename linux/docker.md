# Docker

- To share data between running containers:

  To share data between running container we must define a named volume `$ docker volume create my-volume` and then link the volume with our container `$ docker run -d -v my-volume:/path/to/folder/inside/container image-name`

  