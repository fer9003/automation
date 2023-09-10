# Instalación de istio con istioctl

## Requisitos:
1. Tener un cluster k8s provisionado.
2. Tener conexión al cluster ".kube/config" `az aks get-credentials --resource-group <rg_name> --name <aks_cluster_name>`
3. Tener instalado az cli. `choco install azure-cli`
### Instalar istioctl
```
wget https://github.com/istio/istio/releases/download/1.18.2/istio-1.18.2-linux-amd64.tar.gz
tar xvf istio 1.18
cd istio
export PATH=$PWD/bin:$PATH
```

### Instalar istio
`istioctl install`

### Validar que los componentes istio-ingressgateway, istio-egressGateway y istiod esten instalados.
`kubectl get po -n istio-system`

### Configurar istio injection para un namespace especifico
`kubectl label namespace <namespace_name> istio-injection=enabled`
