# Host principal
brew install multipass
multipass launch --name rancher --cpus 6 --memory 6G --disk 30G
multipass launch --name work1 --cpus 2 --memory 2G --disk 10G
multipass shell rancher
multipass shell work1

# VM Rancher
sudo apt  install docker.io -y
sudo usermod -aG docker ubuntu
newgrp docker

docker run --name rancher -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged rancher/rancher:v2.9.2
docker logs rancher 2>&1 | grep "Bootstrap Password:"

# Host principal
echo "192.168.64.X nginx-app.demo.home.arpa" | sudo tee -a /etc/hosts
multipass delete rancher
multipass delete work1
multipass purge
