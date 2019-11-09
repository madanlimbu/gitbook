# VPS setup

#### Create a sudo user

```text
#login as root user
adduser <username> #create new user
usermod -aG sudo <username> #add user to sudo group

su - <username> #switch to new user
sudo ls -la #test user have sudo access
```

#### Install apache

```text
sudo apt-get update #update package db
sudo apt-get install apache2 #install apache

curl http://localhost #test server is working
```



