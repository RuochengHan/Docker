# Docker
## Note
In Dockerfile:
```bash
FROM $img:$tag
COPY . $container_dir # copy all the files/dirs to $container_dir, if not exsit in the container, it will create
WORKDIR $container_dir # set the work/login dir as $container_dir
RUN ... # command when building the image, usually install sth., try using && connect several commands
EXPOSE $port # set up port open inside the docker
CMD ["bash","-c","..."] # use bash env. to run some command once the container is created, usually service.
```
