# Definicion
Openshift is a managed kubernetes experience for on-premise and cloud-based deployments, built on RHEL and kubernetes, provides a secure and scalable solution for enterprise class applications.
# Beneficios
1. Increased security
2. Entreprise support
3. Self-managing platform
4. Command line and web based management tools.
# Componentes
## Infra Node
A node server containing infrastructure services like monitoring, logging or external routing
## Console
The web UI for the Openshift cluster, It allows for users and administrators to interact with cluster resources
### Project
An extension of kubernetes namespaces. It is an isolations mechanism allowing users to create resources and keep them separate from other Openshift users.
# OpenShift Resources
1. Deployment Config "dc": This is a template for running applications
2. Build Config "bc": This is used by Openshift S"I to build a container image from source code stored in a Git repository, works with a deployment config to provide CICD workflows.
3. Routes: This is a way to expose a service to an external reachable hostname, It is use to allow external clients to reach your applications.
# Comandos OpenShift
## Login before interact with Openshift cluster
`oc login <clusterUrl>`
## This commands is used to get help on oc commands
`oc <command> --help`
## Get the url for the web console , the url can be inputted into a web browser
`oc whoami --show-console`
## List the project
`oc project`
## Status 
`oc status`
## List all objects
`oc get all`
## Describe an object
`oc describe service <service_name>`
## List routes
`oc get routes`
`oc edit route <route_name>`
## List Pods
`oc get pods`
## Execute command inside Pod
`oc exec <pod_name> -- <command>`
