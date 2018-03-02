# Lab 3 : Create a Name Based Virtual Host

In this lab, you will be asking to add a new domain name and its corresponding ip address to `/etc/hosts`. 
The ip address will still be original IP address. 

You have to: 
* Ensure the original web server host still serves traffic as the default vhost.
* Serve this html file below on only the newly defined name vhost.


## 1. Create a new name based virtual host definition.
Create a new config file with the following contents, replacing the string **DOCUMENTROOT** with the proper DocumentRoot for your system.

### 1.1 create a homepage: index.html
* On CentOS, Ubuntu:
/var/www/html/
* On OpenSUSE:
/srv/www/htdocs/

```
<html>
<head>
<title>This is the namevhost</title>
</head>
<body>
<h1>This is namevhost</h1>
</body>
</html>
```

### 1.2 update configuration file: namevhost.conf 
* On CentOS use the file:
/etc/httpd/conf.d/namevhost.conf
* On OpenSUSE use the file:
/etc/apache2/vhosts.d/namevhost.conf
* On Ubuntu use the file:
/etc/apache2/sites-enabled/namevhost.conf

```
<VirtualHost *:80>
DocumentRoot <DOCUMENTROOT>
ServerName _default_
</VirtualHost>
<VirtualHost *:80>
DocumentRoot /namevhost/
ServerName namevhost.example.com
<Directory /namevhost/>
Options Indexes FollowSymLinks
AllowOverride None
Require all granted
</Directory>
</VirtualHost>
```


## 2. Create the new document root folder, and create the index.html file:
```
# mkdir /namevhost/
# vi /namevhost/index.html
```

## 3. Verify that SELinux permissions (if enabled) are correct.
```
# chcon -R --reference=<YOUR-DOCUMENT-ROOT> /namevhost
```

## 4. Restart apache
```
// CentOS
# systemctl restart httpd
//Ubuntu and OpenSUSE
# systemctl restart apache2
```

## 5. Test
Test your new vhost as well as the original vhost as what we have done in previous labs.




