# Windows Server - DNS
*DNS server should be installed after installing the AD*

#### Adding a forwarder
```powershell
Add-DnsServerForwarder -IPAddress <ip> -PassThru
```