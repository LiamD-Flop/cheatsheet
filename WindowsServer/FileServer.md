# Windows Server - File Server

#### Installing file server
```powershell
Install-WindowsFeature -Name FS-FileServer -IncludeAllSubFeature -IncludeManagementTools
```

#### Share a folder
```powershell
New-SMBShare -Name <shared folder name> -Path <path to folder>
```