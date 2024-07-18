```shell
sudo apt install sshuttle
```

```shell
sudo sshuttle --dns -x <server_ip> -r <username>@<server_ip>:<port> 0/0
```

verify your proxy settings are applied :

```shell
curl ip-api.com
```
