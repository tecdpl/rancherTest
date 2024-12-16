# rancherTest

Instale o Docker

mkdir -p $HOME/rancher

docker network create rancher-network

docker run --name rancher-server -d -v $HOME/rancher:/var/lib/rancher \
--restart=unless-stopped \
-p 80:80 -p 443:443 \
--network=rancher-network \
--privileged \
rancher/rancher:v2.9.2

docker run -d --name worker1 --privileged --network=rancher-network \
--restart=unless-stopped ubuntu:20.04 sleep infinity

docker run -d --name worker2 --privileged --network=rancher-network \
--restart=unless-stopped ubuntu:20.04 sleep infinity