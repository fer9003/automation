# Comandos Powershell
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
