# Lab 6 : Create a Certificate Signing Request

This lab is asking us to use the same settings in the last exercise to generate a Certificate Signing Request.

## 1. Create a new private key

### 1.1 On CentOS:
```
# /usr/bin/openssl genrsa -aes128 2048 > /etc/pki/tls/private/ipvhost.example.com.key
```
### 1.2  On OpenSUSE:
```
# /usr/bin/openssl genrsa -aes128 2048 > /etc/apache2/ssl.key/server.key
```
### 1.3 On Ubuntu:
```
# /usr/bin/openssl genrsa -aes128 2048 > /etc/ssl/private/server.key
```

## 2. Create a new Certificate Signing Request.

### 2.1 On CentOS:
```
# /usr/bin/openssl req -utf8 -new -key \
-key /etc/pki/tls/private/ipvhost.example.com.key \
-out /etc/pki/tls/certs/ipvhost.example.com.csr
```
### 2.2 On OpenSUSE:
```
# /usr/bin/openssl req -utf8 -new \
-key /etc/apache2/ssl.key/server.key \
-out /etc/apache2/ssl.csr/server.csr
```
### 2.3 On Ubuntu:
```
# /usr/bin/openssl req -utf8 -new \
-key /etc/ssl/private/server.key \
-out /etc/ssl/server.csr
```
You’ll be asked for a challenge password. Make sure you remember it.

## 3. Test
You must then send off this Certificate Signing Request to be signed by a Certificate Authority.
