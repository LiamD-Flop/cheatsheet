# Linux - Network

Network related files
```bash
/etc/resolv.conf
/etc/network/interfaces
/etc/hosts
```

Show your network devices with some info
```bash
ip address show
```

Show default gateway
```bash
ip route
```

Show nameservers
```bash
cat /etc/resolv.conf
```

Take down a network adapter
```bash
ifconfig <network adapter> down
# or
ifdown <network adapter>
```

Bring network adapter back up
```bash
ifconfig <network adapter> up
# or
ifup <network adapter>
```