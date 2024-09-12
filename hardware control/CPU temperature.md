# CPU temperature

```shell
sudo apt install lm-sensors
```

```shell
sudo sensors-detect
```

answer yes to all .
```shell
sudo service kmod start
```

then :
```shell
sensors
```