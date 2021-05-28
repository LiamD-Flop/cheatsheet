# NSP - Scanning

## Useful commands
**ARP Ping**
Arp ping will send a arp request for the set ip address
```bash
arping <ip-address>
```

## nmap

**Ping sweep**
```bash
nmap -sn <ip-address>-<last host to scan>
```

**Port scan**
```bash
nmap <ip-address>
```

**Detect service on port**
```bash
nmap -sV <ip-address>
```