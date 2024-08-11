when you run `sudo apt update` and you see a package repository name which is for an uninstalled application or package in your ubuntu machine you have options .

# /etc/apt/sources.list.d/ directory

navigate to this directory :
```shell
cd /etc/apt/sources.list.d
```

then find the package name with find :
```shell
sudo find ./ -name '*package_name*'
```

and after this :
```shell
sudo grep -r 'package_name'
```

and just BECAREFUL ! and CAREFULLY remove those files .