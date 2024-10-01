# compression in linux

## compression

```shell
tar -czvf archive_name.tar.gz /path/to/directory
```

## decompression

```shell
tar -xzvf archive_name.tar.gz
```

# Handy Linux Commands

## 1. Compressing and Decompressing in Linux

### Compressing a Directory

#### Using Gzip

```shell
tar -czvf archive_name.tar.gz /path/to/directory
```

Using Bzip2

```shell
tar -cjvf archive_name.tar.bz2 /path/to/directory
```

Using XZ

```shell
tar -cJvf archive_name.tar.xz /path/to/directory
```

# decompressing

Decompressing Gzip Archive (.tar.gz)

```shell
tar -xzvf archive_name.tar.gz
```

Decompressing Bzip2 Archive (.tar.bz2)

```shell
tar -xjvf archive_name.tar.bz2
```


Decompressing XZ Archive (.tar.xz)

```shell
tar -xJvf archive_name.tar.xz
```

## 2. Changing Permissions

Change the Permissions of All Folders Inside a Directory

```shell
find /path/to/parent_directory -type d -exec chmod 755 {} \;
```

Change the Permissions of All Files Inside a Directory

```shell
find /path/to/parent_directory -type f -exec chmod 644 {} \;
```

# Compressing and Decompressing with 7z

### Installing 7zip

```shell
sudo apt install p7zip-full
```

### Compressing
usage example :

```shell
7z a archive_name.7z /path/to/directory
```

### Decompressing

```shell
7z x archive_name.7z
```








