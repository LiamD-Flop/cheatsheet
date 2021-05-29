# Windows Server - User Management

#### Getting a list of users in the domain
```powershell
Get-ADUser -Filter * -Properties *
```

#### Enabling AD User
```powershell
Enable-ADUser -Identity <Name>
```

#### Disabling AD User
```powershell
Disable-ADUser -Identity <Name>
```

#### Creating AD User
```powershell
New-ADUser -Name <name> -AccountPassword(Read-Host -AsSecureString "Type password")
```
