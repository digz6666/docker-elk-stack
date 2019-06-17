### create elastic data dir and set permission
mkdir .es_data
chmod g+rwx .es_data
chgrp 1000 .es_data

### build images
docker build -t ast-elasticsearch -f elasticsearch/Dockerfile .
docker build -t ast-logstash -f logstash/Dockerfile .
docker build -t ast-kibana -f kibana/Dockerfile .

### run
docker-compose up

### run in background (detached mode)
docker-compose up -d

### stop
docker-compose down

### bash into container
docker exec -it ast-elasticsearch bash

### get container logs
docker logs ast-elasticsearch

### info
docker info

### get size of image
docker images

### list containers, images, volumes and networks
docker container ls
docker image ls
docker volume ls
docker network ls

### cleanup
docker system prune

### get ip address of container
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ast-elasticsearch

### backup container
docker run --rm --volumes-from dbstore -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
