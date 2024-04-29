# CREACIÓN DE CLUSTER K8S CON KUBEADM

## Prerequisites
1. Provisionado un nodo master "control plane" en una distro Ubuntu 20.04
2. Provisionado uno o mas  nodos workers "worker node" en una distro Ubuntu 20.04 

## Configurar el nombre del host en el control plane y worker nodes
### Configurar el hostname como "k8s-control" para el master y "k8s-worker01" para el nodo
`sudo  hostnamectl set-hostname k8s-control`
`sudo  hostnamectl set-hostname k8s-worker01`
## Agregar las ips y hostnames en el archivo /etc/hosts tanto en el nodo master como del nodo o nodos workers 
`<private_ip>   <hostname>`

## CONFIG NODE MASTER
## 1. En el nodo master ejecutar el comando
` cat <<EOF | sudo tee /etc/modules-load.d/containerd.conf`
agregar en la prompt
`overlay`
`br_netfilter`
`EOF`
## 2. Ejecutar los comandos
```
sudo modprobe overlay
sudo modprobe br_netfilter
```
## 3.  Ejecutar los siguientes comandos
`cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf`
agregar en la prompt
`net.bridge.bridge-nf-call-iptables = 1`
`net.ipv4.ip_forward = 1`
`net.bridge.bridge-nf-call-ip6tables = 1`
`EOF`

## 4. Ejecutar el comando
`sudo sysctl --system`

## 5. Instalar container.d
```
sudo apt-get update && sudo apt-get install -y containerd
sudo mkdir -p /etc/containerd
sudo containerd config default | sudo tee /etc/containerd/config.toml
sudo systemctl restart containerd
sudo swapoff -a
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

## 6. Agregar el paquete al reposiorio de k8s
`cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list`
agregar en la prompt
```
deb https://apt.kubernetes.io/ kubernetes-xenial main
```
`EOF`

## 7. Ejecutar los siguientes comandos para instala Kubeadm
```
sudo apt-get update
sudo apt-get install -y kubelet=1.27.0-00 kubeadm=1.27.0-00 kubectl=1.27.0-00
sudo apt-mark hold kubelet kubeadm kubectl 
```
## CONFIG WORKER NODES
## En todos los worker nodes realizar los pasos del 1 al 7

## EN EL NODO MASTER INICIALIZAR EL CLUSTER "solo realizarlo en el master node"
`sudo kubeadm init --pod-network-cidr 192.168.0.0/16 --kubernetes-version 1.27.0`

## EN EL NODO MASTER EJECUTAR LOS SIGUIENTES COMANDOS
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## VALIDAR CONFIG EN EL NODO MASTER
`kubectl get nodes`
si da un mensaje en status NOT READY proceder a instalar el siguiente manifiesto que es Calico network addon:
```
wget https://docs.projectcalico.org/manifests/calico.yaml
kubectl apply -f calico.yaml`
```
## Validar que se encuentre el STATUS en READY
`kubectl get nodes`

## Si el status del nodo es READY  Proceder a Generar en el nodo master el comando que contiene el token
`kubeadm token create --print-join-command`

## PEGAR EL COMANDO EN EL WORKER NODE CON PERMISOS SUDO
ejemplo sudo kubeadm join 10.158.0.4:6443 --token hxxxx --discovery-token-ca-cert-hash sha256:xxxx

## Verificar desde el nodo master que ya aparezca el worker node con el comando
`kubectl get nodes`
El workernode debe aparecer con status READY
