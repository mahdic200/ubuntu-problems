# adding or removing users

```shell
sudo adduser <username>
```

## making it a sudoer

```shell
usermod -aG sudo <username>
```

verifying operation :

```shell
groups <username>
```

# removing a user

if you wanna completely remove that poor user :

```shell
sudo deluser --remove-home <username>
```

if you wanna keep files :

```shell
sudo deluser <username>
```
