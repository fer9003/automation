# Install istio using docker

## Pre requisites
1. Install docker, docker compose
2. Install kubectl

## Execute the following commands:
´´´
kubectl config set-context istio --cluster=istio
kubectl config set-cluster istio --server=http://localhost:8080
kubectl config use-context istio
export DOCKER_GATEWAY=172.28.0.1:
wget  https://github.com/istio/istio/releases/download/1.0.6/istio-1.0.6-linux.tar.gz
tar -xvf istio-1.0.6-linux.tar.gz
cd istio-1.0.6/
docker compose -f install/consul/istio.yaml up -d

´´´
## Notes:
Execute again the command:
´docker compose -f install/consul/istio.yaml up -d´

