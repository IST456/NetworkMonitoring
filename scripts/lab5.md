# Lab 5: SSL Certificate

In this lab, we will create and test a self-signed SSL certificate.

* Private-key pass phrase: **password**
* Country Name: **US**
* State Name: **PA**
* Locality Name: **StateCollege**
* Organization Name: **PSU**
* Organizational Unit Name: **IT**
* Common Name: **ipvhost.example.com** 
* Email Address: **admin@example.com** 

## 1. Backup the original private key, if one exists.

```
$ sudo -i
```
### 1.1 On CentOS
```
# mv /etc/pki/tls/private/localhost.key /etc/pki/tls/private/localhost.key.orig
```

### 1.2 On Ubuntu:
```
# mv /etc/ssl/private/ssl-cert-snakeoil.key  /etc/ssl/private/ssl-cert-snakeoil.key.orig
```


### 1.3 On OpenSUSE: 
There is no key by default so nothing needs to be backed up.



## 2. Create a new private key

### 2.1 On CentOS:
```
# /usr/bin/openssl genrsa -aes128 2048 > /etc/pki/tls/private/localhost.key
```
### 2.2 On OpenSUSE:
```
# /usr/bin/openssl genrsa -aes128 2048 > /etc/apache2/ssl.key/server.key
```
### 2.3 On Ubuntu:
```
# /usr/bin/openssl genrsa -aes128 2048 > /etc/ssl/private/server.key
```


## 3. Create a new self-signed SSL certificate

### 3.1 On CentOS:
```
# /usr/bin/openssl req -utf8 -new -key /etc/pki/tls/private/localhost.key -x509\
-days 365 -out /etc/pki/tls/certs/localhost.crt -set_serial 0
```
### 3.2 On OpenSUSE:
```
# /usr/bin/openssl req -utf8 -new -key /etc/apache2/ssl.key/server.key -x509 \
-days 365 -out /etc/apache2/ssl.crt/server.crt -set_serial 0
```
### 3.3 On Ubuntu:
```
# /usr/bin/openssl req -utf8 -new -key /etc/ssl/private/server.key -x509 \
-days 365 -out /etc/ssl/certs/server.crt -set_serial 0
```


## 4. Update the Apache configuration (if needed)

### 4.1 On Ubuntu: Enable SSL vhost
```
// On Ubuntu: Enable SSL vhost
# ln -s /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-enabled/
//Enable SSL module and configuration
# ln -s /etc/apache2/mods-available/ssl.conf /etc/apache2/mods-enabled/
# ln -s /etc/apache2/mods-available/ssl.load /etc/apache2/mods-enabled/
```

Edit the file `/etc/apache2/sites-enabled/default-ssl.conf` and modify the
paths for the key and crt files so they look like this:
```
SSLCertificateFile /etc/ssl/certs/server.crt
SSLCertificateKeyFile /etc/ssl/private/server.key
```

Note: You may have to comment out the directives **SSLSessionCache** and
**SSLSessionCacheTimeout** from the `/etc/apache2/mods-enabled/ssl.conf` file.

### 4.2 On OpenSUSE: Enable SSL vhost
```
# cp /etc/apache2/vhosts.d/vhost-ssl.template /etc/apache2/vhosts.d/vhost-ssl.conf
```
Enable the SSL server module, edit the file `/etc/sysconfig/apache2` and add
the string **”SSL”** to the variable **APACHE SERVER FLAGS** so it looks like this:
```
APACHE_SERVER_FLAGS="SSL"
```

### 4.3 On CentOS:

There are no configuration changes needed.

## 5. Restart Apache and test your new certificate. 
You may have to add **ipvhost.example.com**  to your `/etc/hosts` file.

### 5.1 On CentOS:
```
# systemctl restart httpd
```

### 5.2 On Ubuntu or OpenSUSE:
```
# systemctl restart apache2
```








