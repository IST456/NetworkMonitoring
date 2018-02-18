# Lab 1. Install Apache Server 
This lab is using Ubuntu.

## 1. install apache 
```
$ sudo apt-get install apache2
```

## 2. create default page

### 2.1. go to defualt Document Root 
```
$ cd /var/www/html/
```

### 2.2. create index.html 
```
$ vim index.html
```
put the content as:
```
<html><head><title>This is lab 1</title></head><body><h1>This is my default lab 1</h1></body></html>
```
## 3. Double check Apache is enabled and started
```
$ sudo systemctl enable apache2
$ sudo systemctl start apache2
```
## 4. Verify page you created
`
$ w3m -dump http://<YOUR_IP_ADDRESS>/index.html 
`
or 
`
$ firefox http://<YOUR_IP_ADDRESS>/index.html
`

