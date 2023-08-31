# Instalación de istio con istioctl

## Requisitos:
1. Tener un cluster k8s provisionado.
2. Tener instalado az cli. `choco install azure-cli`
3. Tener instalado istioctl "En windows descargar el ejecutable y agregar el path donde se ublica el ejecutable a la variable del sistema PATH"

### Extraer template basado en el profile default para poder customizar
`istioctl profile dump default > tuned_settings.yaml`

### Editar el archivo tuned_settings.yaml y cambiar de false a true la opción de egressGateway
egressGateway:
- enabled: true

### Instalar istio basado en el archivo custom
`istioctl install -f tuned_settings.yaml`

### Validar que los componentes istio-ingressgateway, istio-egressGateway y istiod esten instalados.
`kubectl get po -n istio-system`