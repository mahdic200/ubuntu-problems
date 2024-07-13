unable to mount PATH to /media/USER/PATH

# mount manually

find your drive name

```shell
sudo fdisk -l
```

```shell
sudo mkdir /media/USER/pick_a_name
```

then mount the drive

```shell
sudo mount FULL_PATH_OF_DRIVE /media/USER/picked_name
```

# unmount with umount

```shell
sudo umount /media/USER/picked_name
```

done :)