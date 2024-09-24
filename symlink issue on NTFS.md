# symlink issue on NTFS

when you have a partition which is NTFS filesystem type you may encounter errors when trying to create symlinks . to avoid this problem and fix the issue you may want to do these steps .
by default , the linux kernel mounts partitions using ntfs3 driver . but you can use ntfs-3g driver which is a more mature driver to mount these type of file systems .

find the partition UUID :

```shell
sudo blkid
```

it is sth like this :

```shell
/dev/nvme0n1p5 UUID="XXXX-YYYY" TYPE="ntfs"
```

make a note of UUID .

## edit the /etc/fstab

```shell
sudo cp /etc/fstab /etc/fstab.backup
sudo nano /etc/fstab
```

add the following to the `/etc/fstab` file :

change the E_DRIVE path with your path , and uuid with your uuid .
```shell
UUID=XXXX-YYYY  /media/mahdi/E_DRIVE  ntfs-3g  uid=1000,gid=1000,umask=022,permissions  0  0
```

then mount the partition with your gui in this case gnome .















