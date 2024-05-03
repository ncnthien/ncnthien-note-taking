- pull an image
```
docker pull <image_name>
```
- current running containers
```
docker ps
```
- trigger a command via a container (can use this way to access bash of container if needed)
```
docker exec -it <container_id> <command>
```
- current image list
```
docker image ls
```
- copy a file from container to local
```
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH
```
- copy a file from local to container
```
docker cp [OPTIONS] SRC_PATH CONTAINER:DEST_PATH
```
- stop a running container
```
docker stop [OPTIONS] CONTAINER
```
- remove a container
```
docker rm [OPTIONS] CONTAINER
```