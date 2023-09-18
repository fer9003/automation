# Definicion
Kubernetes is an open source system for automating deployment, scaling and management of containerized applications.
# Beneficios
1. It uses multiples nodes for resilency and scalability.
2. It allows development team to move faster.
3. Kubernetes is cloud agnostic you can use it on AWS, Azure, GCP, etc

# Comandos para Kubernetes
## NAMESPACES
### Ver todos los pods del cluster
`kubectl get pods --all-namespaces`
## Ver los pods de un namespace especifico
`kubectl get pods -n <namespace_name>`
### Crear un namespace
`kubectl create namespace <namespace_name>`

### Port Forwarding
 `kubectl port-forward <pod_name> <localhost_port>:<container_port>`
