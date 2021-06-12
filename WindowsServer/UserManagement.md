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

#### Add all users from OU to a secure group
```powershell
 Get-ADUser -SearchBase '<DistinguishedName (without the CN part)>' -Filter * | ForEach-Object {Add-ADGroupMember -Identity '<secure group name>' -Members $_ }
 ```

 function prompt {"`n$(get-date) | PS [$Env:userdomain\\$Env:username@$Env:computername] `n$($PWD.ProviderPath) > "}