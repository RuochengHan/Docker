# Docker
## Note
### Bugs
1. Docker log, do not give all python print: https://www.jianshu.com/p/9f1fa58d4395
```bash
# In Dockerfile:
CMD ["python", "-u", "Api.py"]
# In .py file:
print("Hello? Anyone there?", flush=True)
```

### Dockerfile
In Dockerfile:
```bash
FROM $img:$tag
COPY . $container_dir # copy all the files/dirs to $container_dir, if not exist in the container, it will create
WORKDIR $container_dir # set the work/login dir as $container_dir
RUN ... # command when building the image, usually install sth., try using && connect several commands
EXPOSE $port # set up port open inside the docker
CMD ["bash","-c","..."] # use bash env. to run some command once the container is created, usually service.
```
Need to use 0.0.0.0:$port for service, not 127.0.0.1:$port

### Build image, create container
```bash
sudo docker build -t $image . # build image based on ./Dockerfile
# create container, add -rm can directly delete after running test commands
sudo docker run -it -p 40001:40000 --name "$container" $image # 40001 is port outside and 40000 is inside
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

## Install
```bash
$ sudo apt update
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
$ apt-cache policy docker-ce
Output:
docker-ce:
  Installed: (none)
  Candidate: 5:19.03.9~3-0~ubuntu-focal
  Version table:
     5:19.03.9~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
$ sudo apt install docker-ce
$ sudo systemctl start docker
$ sudo systemctl status docker
Output:
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2020-05-19 17:00:41 UTC; 17s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 24321 (dockerd)
      Tasks: 8
     Memory: 46.4M
     CGroup: /system.slice/docker.service
             └─24321 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
```
