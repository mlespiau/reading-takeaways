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

Fix wrong time in docker containers after Macbook sleep and wake up
```
docker run -it --rm --privileged --pid=host debian nsenter -t 1 -m -u -n -i date -u $(date -u +%m%d%H%M%Y)
```

Run $COMMAND in all containers
``` 
export COMMAND="ls -la"
for c in $(docker ps | grep web | awk '{print $1}'); do docker exec -ti $c $COMMAND; done
```

# Apache / HTTPD
Count URLs accessed on a given hour
``` 
cat access_log | grep 30/Dec/2016:10 | awk '{ print $9}' | sort | uniq -c | sort -gr | head
```

Count request by IP for a given hour
``` 
cat access_log | grep 30/Dec/2016:10 | awk '{ print $4}' | sort | uniq -c | sort -gr | head
```

# Curl
Curl format to troubleshoot latency
```
echo "\n
            time_namelookup:  %{time_namelookup}\n
               time_connect:  %{time_connect}\n
            time_appconnect:  %{time_appconnect}\n
           time_pretransfer:  %{time_pretransfer}\n
              time_redirect:  %{time_redirect}\n
         time_starttransfer:  %{time_starttransfer}\n
                            ----------\n
                 time_total:  %{time_total}\n
              size_download:  %{size_download}\n
\n" > curl-format.txt
