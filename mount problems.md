if you have problem with mounting some drive on ubuntu then enter this commands in the shell :

1 - `sudo fdisk -l`

2 - `sudo mkdir /media/windows`

3 - `sudo mount -t ntfs -o ro /dev/sdXY /media/windows`