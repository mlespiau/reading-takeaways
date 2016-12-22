# Docker
List running docker container names:
```
docker inspect --format='{{.Name}}' $(sudo docker ps -aq --no-trunc)
```
