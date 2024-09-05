I was trying to compile my Rust application in linux ubuntu , and I encountered an error :
```
library fontconfig for development not found !
```

and I searched a bit through the web , it seems that linux systems have some libraries for themselves which are important and essential for development , and I didn't have one of them called `fontconfig` and the full name is `libfontconfig-dev` . I searched how to install it and a page came up which was for ubuntu distribution . it was listed in [this page](https://launchpad.net/ubuntu/+source/fontconfig) .

then I simply installed it via :

```shell
sudo apt install libfontconfig-dev
```

you can simply verify installation via `pkg-config --modversion fontconfig`





