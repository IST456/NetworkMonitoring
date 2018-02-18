# Lab 2 document root in virtual network interface 
Serve two document roots at same time, original file accessible at original IP address, while new one works as well

## 1. Create IP alias
```
$ sudo ip addr add 192.168.153.#/24 dev eth0
```
make sure that `192.168.153.#/24` does not conflit with other existing interfaces

## 2. Add to `/etc/hosts`

`vim /etc/hosts`
then add in format as the third line below:
```
127.0.0.1       localhost
127.0.1.1       vagrant.vm      vagrant
192.168.153.3  ipvhost.example.com
```

## 3. Add ipvhost directory
```
$ cd /var/www/html/
$ mkdir ipvhost
```

## 4. create homepage 
```
$ vim /ipvhost/index.html
```
The content of file looks like below:
```
<html><head><title>This is the Lab 2 IP vhost</title></head><body><h1>This is my IP vhost Lab 2 </h1></body></html>
```
## 5. double check SElinux permissions
`$ sudo chcon -R --reference=<YOUR-DOCUMENT-ROOT>  /ipvhost/`

## 6. create configuration file for virtual IP host
`$ vim /etc/apache2/sites-enabled/ipvhost.conf`
Then append following:
```
<VirtualHost 192.168.153.X:80>DocumentRoot /ipvhost/ServerName ipvhost.example.com<Directory /ipvhost/>Options Indexes FollowSymLinksAllowOverride NoneRequire all granted</Directory></VirtualHost>
```
## 7. restart apache and test as lab 1
`$ sudo systemctl restart apache2`
