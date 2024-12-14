# mysql installation for xampp

to install xampp on ubuntu and debian 12 you need to install this package first :

`sudo apt install net-tools`

and mysql-server this is a full reference [digital ocean](https://docs.vultr.com/how-to-install-mysql-on-debian-12) :

```shell
wget https://dev.mysql.com/get/mysql-apt-config_0.8.30-1_all.deb
```

```shell
sudo dpkg -i mysql-apt-config_0.8.30-1_all.deb
```

```shell
sudo apt update
sudo apt install mysql-server
```
