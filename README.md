# Docker
## Note
### Dockerfile
In Dockerfile:
```bash
FROM $img:$tag
COPY . $container_dir # copy all the files/dirs to $container_dir, if not exsit in the container, it will create
WORKDIR $container_dir # set the work/login dir as $container_dir
RUN ... # command when building the image, usually install sth., try using && connect several commands
EXPOSE $port # set up port open inside the docker
CMD ["bash","-c","..."] # use bash env. to run some command once the container is created, usually service.
```
### Build image, create container
```bash
sudo docker build -t $image . # build image based on ./Dockerfile
sudo docker run -itd -d 40001:40000 --name "$container" $image # create container, add -rm can directly delete after running test commands
sudo docker exec -it $container /bin/bash
```

### Other commands
```bash
sudo docker cp . $container:/ # copy files
sudo docker ps # show all running containers
sudo docker stop $containerID # stop container
sudo docker rm $containerID # remove container
sudo docker images # list all images
sudo docker rmi $imageID # remove image
```

