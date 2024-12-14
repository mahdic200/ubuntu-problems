# XDM configurations

# XDM javashared resources folder

The `javasharedresources` folder is typically created by the Java Runtime Environment (JRE) or Java Virtual Machine (JVM). It's used to store class data sharing (CDS) caches, which improve the performance of Java applications by reducing startup time and memory usage. This folder is not specific to Xtreme Download Manager (XDMan) but is likely created because XDMan uses Java.
The JVM can be instructed to avoid creating the `javasharedresources` folder by overriding its default behavior:
## 2. Modify JVM Options

**Find XDMan's Executable Script**: Locate the script or command that launches XDMan. It might be in `/usr/bin/xdman` or similar locations.

**Edit the Launch Script**: Add the following JVM option to disable the use of `javasharedresources`:

```bash
-Xshare:off
```


this is the bash script located in `/usr/bin/xdman` which I changed it due to above explanations :

```shell
#!/bin/bash

2 if [ $EUID -eq 0 ];then

3 echo "It's not recomended to run XDM as root, as it can cause proble

ms"

4 fi

5 /opt/xdman/jre/bin/java -Dsun.java2d.xrender=false -Xmx1024m -Xshare:off -jar /opt/xdman/

xdman.jar

```

I changed it and `-Xshare:off` before `-jar /opt/xdman` . also I changed the `/usr/share/applications/xdman.desktop` to use the `/usr/bin/xdman` script file as executable .

and it seems it did the trick for me .

# XDM tray Icon

go to XDM settings and scroll down to Advanced Settings and then check the `Show the Tray icon (needs restart)` .

go to system monitoring and then search for `xdman` and then kill the processes and open the XDM again .