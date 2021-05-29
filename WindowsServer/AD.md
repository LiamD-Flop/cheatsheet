# Windows Server - Active Directory

#### Installing AD
```powershell
Install-windowsfeature -name AD-Domain-Services -IncludeManagementTools
```

#### Creating forest
```powershell
Import-Module ADDSDeployment
Install-ADDSForest -DomainName <domain name> -InstallDns -SafeModeAdministratorPassword <password>
```
Wait for the restart and Active Directory  should be installed

#### Making sure the NTP to sync time
```powershell
net stop w32time
w32tm /config /syncfromflags:manual /manualpeerlist:"0.pool.ntp.org, 1.pool.ntp.org, 2.pool.ntp.org"
w32tm /config /reliable:yes
net start w32time
```

#### Adding machine to AD
On the machine execute
```powershell
Add-Computer -DomainName <domainName> -Restart
```