### 首先用 `df -h` 命令查看磁盘情况
```bash
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           198M   21M  177M  11% /run
/dev/vda2        40G   40G     0 100% /
tmpfs           988M     0  988M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           198M  4.0K  198M   1% /run/user/0
```
可以看出当前系统中有两个文件系统：/dev/vda2 和 tmpfs。

- /dev/vda2：该文件系统使用磁盘设备 /dev/vda2，容量为 40G，已使用 40G，可用空间为 0，使用比例为 100%。这表明 /dev/vda2 已经满了，需要进行磁盘清理或扩容操作。
tmpfs：该文件系统是基于内存的临时文件系统，用于存储临时文件和目录。/run、/dev/shm、/run/lock 和 /run/user/0 目录都是挂载在 tmpfs 上的，它们的容量和使用情况分别为 198M/21M、988M/0、5.0M/0、198M/4.0K。其中，/run 目录主要用于存储运行时的数据，/dev/shm 目录用于共享内存，/run/lock 目录用于存储锁文件，/run/user/0 目录用于存储用户临时文件。由于 tmpfs 是基于内存的文件系统，它的容量会随着内存的变化而变化，一般来说，它的容量不会受到磁盘容量限制。

### 然后通过find全局搜索 大于1G 的文件
```bash
sudo find / -xdev -type f -size +100M -print 2>/dev/null | head -n 10
sudo find / -xdev -type d -size +100M -print 2>/dev/null | head -n 10
```
sudo find / -xdev -type f -size +100M -print 2>/dev/null
该命令使用 find 命令查找大小超过 100 MB 的文件，其参数含义如下：
- /：表示从根目录开始搜索。
- -xdev：表示不跨越文件系统边界，只在当前文件系统中查找文件。
- -type f：表示查找文件类型为普通文件（file）的文件。
- -type d：表示查找文件类型为目录（directory）的目录。
- -size +100M：表示查找大小超过 100 MB 的文件。
- -print：表示将查找结果输出到标准输出。
- 2>/dev/null：表示将标准错误输出重定向到 /dev/null，以避免输出错误信息。

### 定位文件创建时间
```bash
ls -lh data1.doi
-rw-r----- 1 root root 36G Feb  3 19:40 data1.doi

ls -lu data1.doi
-rw-r----- 1 root root 38092357632 Jan 30 00:02 data1.doi
```

- lh : 创建时间
- lu : 访问时间 其中，第六列是文件的访问时间，第七列是文件的访问日期

> 以上三种时间戳的含义有所不同。文件的创建时间是指文件在文件系统中被创建的时间；文件的修改时间是指文件内容被修改的时间；文件的访问时间是指文件最近一次被读取或写入的时间。
