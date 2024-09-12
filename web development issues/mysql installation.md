digital ocean is the best : [https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04) 

```shell
sudo apt update
```

```shell
sudo apt install mysql-server
```

```shell
sudo systemctl start mysql.service
```

```shell
sudo mysql
```

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

exit mysql :

```sql
exit
```

```shell
mysql -u root -p
```

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```

```shell
sudo mysql_secure_installation
```

```sql
CREATE USER 'username'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

to grant a **single** privilege to a user for a database's table :

```sql
GRANT PRIVILEGE ON database.table TO 'username'@'localhost';
```

to grant all privileges for all databases to a user :

```sql
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;
```

```sql
FLUSH PRIVILEGES;
```


