# pwsh-mremoteng-confCons
Simple PowerShell cmdlet to call Consul API and generate confCons.xml file for mRemoteNG

## Params
* `consulUri` - Consul address
* `connectionFile` - path where confCons.xml should be saved
* `sshUsername` - username for ssh connection

## How to use it?
You can execute this cmdlet every time you start mRemoteNG. Just edit / create the shortcut and add this or run it in command line or powershell console:
```shell
powershell -NoProfile -Command "Stop-Process -Name mRemoteNG -Force" ; Create-mRemoteNGConnectionFile -consulUri {{ Consul Address }} -connectionFile {{ path for confCons.xml file }} -sshUsername {{ ssh username }} ; {{ path for mRemoteNG.exe file }} /c:"{{ path for confCons.xml file }}"
```
for example:
```shell
powershell -NoProfile -Command "Stop-Process -Name mRemoteNG -Force" ; Create-mRemoteNGConnectionFile -consulUri http://consul.mydomain:8500/v1/catalog/nodes -connectionFile C:\Program Files\mRemoteNG\confCons.xml -sshUsername my-ssh-user ; C:\Program Files\mRemoteNG\mRemoteNG.exe /c:"C:\Program Files\mRemoteNG\confCons.xml"
```
