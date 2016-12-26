# Docker
List names of running docker container:
```
docker inspect --format='{{.Name}}' $(sudo docker ps -q --no-trunc)
```

List names of all docker container:
```
docker inspect --format='{{.Name}}' $(sudo docker ps -aq --no-trunc)
```

One liner to stop / remove all docker containers:
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```
