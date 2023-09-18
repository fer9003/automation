# Instalación de K3S
## Instalación Nodo Master
`curl -sfL https://get.k3s.io | sh - `
### Probar que se haya instalado el nodo master
`sudo kubectl get nodes`
### Obtener token para pasarlo en la variable K3S_URL en la config de los worker nodes.
`sudo cat /var/lib/rancher/k3s/server/node-token`

## Instalación Node Worker
`curl -sfL https://get.k3s.io | K3S_URL=https://<ip_master_node>:6443 K3S_TOKEN=<token> sh - `

### Probar que el nodo se haya agregado ejecutando el siguiente comando desde el nodo master
`sudo kubectl get nodes`


# Dar permiso para que su usuario pueda leer el kubeconfig file esta config se realiza en el master node
```
sudo groupadd k3s
sudo usermod -aG k3s <su_usuario>
sudo chown root:k3s /etc/rancher/k3s/k3s.yaml
sudo chmod 740 /etc/rancher/k3s/k3s.yaml
exit
```
## Iniciar sesión nuevamente en el master node y ejecutar el comando sin sudo
`kubectl get nodes`

# Ejecutar un pod y service de prueba
```
kubectl run my-first-pod --image nginx
kubectl expose pod my-first-pod --type NodePort --port=80 --name=nginx-np-service
kubectl get svc
```
## Visualizar desde el navegador con la ip del nodo master y puerto NodePort
`<ip_nodo_master>:<nodePort>`