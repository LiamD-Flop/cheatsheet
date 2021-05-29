# Windows Server - Setup

#### Enabling numpad by default
```powershell
Set-ItemProperty -Path "Registry::HKU\.DEFAULT\Control Panel\Keyboard" -Name "InitialKeyboardIndicators" -Value "2"
```

#### Setting a static ip
```powershell
## First get the index of the adapter you want to set a static ip on.
Get-NetAdapter

## Now set the static ip
New-NetIPAddress -IPAddress <ip> -PrefixLength <subnetmask> -InterfaceIndex <Index of inderface from previous command> -DefaultGateway <gateway>
```

#### Changing the DNS Server
```powershell
Set-DnsClientServerAddress -InterfaceIndex <ifindex> -ServerAddresses <dns ip>
```

#### Allowing ICMP in firewall
```powershell
New-NetFirewallRule -DisplayName "ICMP IPv4" -Protocol ICMPv4 -IcmpType 8 -Enabled True -Action Allow
New-NetFirewallRule -DisplayName "ICMP IPv6" -Protocol ICMPv6 -IcmpType 8 -Enabled True -Action Allow
```