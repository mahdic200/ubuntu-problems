
digital ocean : [https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)


## inspection

```shell
sudo ufw status
```

## enable

```shell
sudo ufw enable
```

# disable

```shell
sudo ufw disable
```

## Block an IP Address

```shell
sudo ufw deny from 203.0.113.100
```

# Delete a rule

```shell
sudo ufw delete allow from 203.0.113.101
```

## list available application profiles

```shell
sudo ufw app list
```

## enable application profile

```shell
sudo ufw allow "OpenSSH"
```

## disable application profile

example :

```shell
sudo ufw delete allow 22/tcp
```






















