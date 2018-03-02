# Lab 4: Create password protected sub directory

Goal of this lab includes:
* Create the directory secure in the default document root.
* Require the user **bob** enter the password **heyman!** to access this directory.

## 1. Create the new secure folder
* On CentOS and Ubuntu and later:
/var/www/html/secure/
* On OpenSUSE:
/srv/www/htdocs/secure/

```
// CentOS and Ubuntu and later
$ cd /var/www/html/
$ mkdir secure

// On OpenSUSE
$ cd /srv/www/htdocs
$ mkdir secure
```

## 2. Create the following stanza to password protect the directory

* On CentOS use the file:
/etc/httpd/conf.d/secure-dir.conf
* On OpenSUSE use the file:
/etc/apache2/vhosts.d/secure-dir.conf
* On Ubuntu use the file:
/etc/apache2/sites-enabled/secure-dir.conf

```
<Location /secure/>
AuthType Basic
AuthName "Restricted Area"
AuthUserFile secure.users
Require valid-user
</Location>
```

## 3. Create a password file and an entry for the user bob in the appropriate directory

* On CentOS use the file:
/etc/httpd/secure.users
* On OpenSUSE use the file:
/srv/www/secure.users
* On Ubuntu use the file:
/etc/apache2/secure.users

Please use below command: 
```
// Ubuntu
$ sudo htpasswd -c $FILENAME bob
// OpenSUSE
$ sudo htpasswd2 -c $FILENAME bob
```

You may have to install **apache2-utils** if `htpasswd` does not exist.


## 4. Restart apache
```
//CentOS
$ sudo systemctl restart httpd
// Ubuntu and OpenSUSE
$ sudo systemctl restart apache2
```

## 5. Verify that the directory is password protected and that bob is allowed to log in.
