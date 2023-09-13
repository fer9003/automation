# Comandos Basicos de Powershell
1. Ejecutar un proceso por ejemplo Notepad
`Start-Process notepad`
2.  Cerrar un proceso por ejemplo Notepad
`Stop-Process -Name notepad`
3. Mostrar todos los directorios y archivos
`Get-Item *`
4. Mostrar el contenido de un archivo "demo.txt" y solo muestre las primeras 8 lineas
`Get-Content -Path .\demo.txt -TotalCount 8`
5. Mostrar todos los servicios
`Get-Service`
`Get-Service -Name "win*" -Exclude "WinRM"`
6. Iniciar un servicio "eventlog"
`Start-Service -Name "eventlog"`
7. Verificar el estado de un servicio "eventlog"
`Get-Service -Name "eventlog"`
8. Parar un servicio "ejemplo AudioSrv"
`Stop-Service -Name AudioSrv`
9. Ver el Scope de Execution Policy
`Get-ExecutionPolicy -list`
10. Cambiar a RemoteSigned la ExecutionPolicy que tiene como scope LocalMachine
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine`
11. Copiar un archivo a otro directorio
`Copy-Item "C:\users\fernando\demo.txt" -Destination "C:\Demo\"`
12. ELiminar un archivo
`Remove-Item "C:\Users\fernando\demo.txt"`

# Comandos Powershell Modules
1. Muestra los modulos dispoibles
`Get-Module -ListAvailable`
2. Muestra los modulos instalados
`Get-Module`
3. Muestra todos los comandos disponibles en un modulo "Az.Compute"
`Get-Command -Module "Az.Compute"`
4. Mostrar info de ayuda acerca de un comando que pertenece a un modulo "Start-AzVM"
`Get-Help Start-AzVM`
5. Obtener un ejemplo de como usar un comando
`Get-Help Start-AzVM -examples`

# Variables
```
$location = Get-Location
$location
$x = 98
3 +$x
```
## Pipelines Ideal for filtering Objects
`Get-Service | Format-List `
`Get-Service -Name WinRM |Format-List -Property *`
## Listar los servicios que estan en ejecución
`Get-Service | Where-Object {$_.Status eq "Running}`
## Listar los servicios que estan en stopped
`Get-Service | Where-Object {$_.Status eq "Stopped"}`
## Listar únicamente los 5 primeros servicios que estan en ejecución 
`Get-Service | Where-Object {$_.Status eq "Running"} | Select-Object -First 5`

# Instalar AZ Modulo para Azure
1. Instalar el modulo Az
`Install-Module -Name Az -AllowClobber -Scope AllUsers`
2. Verificar la instalacion
`Get-Module`

# Conectarse a cuenta Azure desde Powershell
1. Comando para conectarse a Azure por Powershell
`Connect-AzAccount`

# Comandos para Azure Powershell 
1. Informacion de la suscripción
`Get-AzSubscription | fl`
2. Información acerca de una VM
`get-azvm`
3. Parar una vm "TestVM"
`stop-azvm -Name TestVM `
4. Start una vm "TestVM"
`start-azvm -Name TestVM`
5. Mostrar los ResourceGroups
`Get-AzResourceGroup`
6. Crear un Resource Group
`New-AzResourceGroup`
7. Login y Logout
`Login-AzAccount`
`Logout-AzAccount`

