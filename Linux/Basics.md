# Linux - Basics

Make sure packages are up to date
```bash
apt update && apt upgrade
```

### Installing sudo
```bash
apt install sudo
```

Giving user sudo rights
```bash
usermod -aG sudo <username>
```

Giving an entire group sudo rights
```bash
visudo
# Add following line
%<groupname>    ALL=(ALL:ALL) ALL
```

### Man powermove
```bash
man -k <some search term>
```
This will show the you man pages where the search term can be found