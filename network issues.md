clear DNS cache:

```shell
sudo resolvectl flush-caches
```

problem to installing packages:

```shell
sudo apt update
``` 

```shell
sudo apt-get update
```

if net not working for getting apt packages : 

```shell
sudo nano /etc/resolv.conf
```


and add these lines before nameserver ... :

```conf
nameserver 8.8.8.8
nameserver 8.8.4.4
```



solve apt update network issue:

```shell
echo "nameserver 8.8.8.8" | sudo tee /etc/resolv.conf > /dev/null
```