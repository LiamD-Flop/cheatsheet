# Linux - Webserver

### Give the server a fixed IP
```bash
sudo nano /etc/network/interfaces

# Then set the desired nic to a static address
# Example
iface ens37 inet static
    address 10.1.1.2/24
    broadcast 10.1.1.255
```

You could also bind a feature (like a web server) to a specific nic using dnsmasq

### Install the desired webserver
In this example Apache
```bash
sudo apt install apache2
```

After installing you could check if the service is installed correctly by looking at `/var/log/messages`

### Setting up the webserver

Best thing to do is create a user for you all things related to the webserver
```
sudo useradd web
sudo usermod -g www-data
```

Now we make the `web` user the owner of the folder `/var/www/`
```bash
sudo chown web:www-data /var/www
```

Setup the file permissions
```bash
# Make the folders 755
sudo find /var/www/ -type d -exec chmod 755 {} +
# Make the files 644
sudo find /var/www/ -type f -exec chmod 644 {} +
```

Set an alias to you domainname in your hosts file
```bash
sudo nano /etc/hosts

# add a line with the static ip and the domainname

10.1.1.2    hostname.be
```
