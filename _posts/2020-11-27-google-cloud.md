---
layout: post
title: "GCP"
---

list available extra disk

```
$ sudo lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda       8:0    0   10G  0 disk 
├─sda1    8:1    0  9.9G  0 part /
├─sda14   8:14   0    3M  0 part 
└─sda15   8:15   0  124M  0 part /boot/efi
sdb       8:16   0  200G  0 disk 
```


format /dev/sdb
```
$ sudo mkfs.ext4 -m 0 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb
mke2fs 1.44.5 (15-Dec-2018)
Discarding device blocks: done                            
Creating filesystem with 52428800 4k blocks and 13107200 inodes
Filesystem UUID: f32bdbb2-f937-44c0-a45f-64007374db66
Superblock backups stored on blocks: 
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
        4096000, 7962624, 11239424, 20480000, 23887872
Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (262144 blocks): done
Writing superblocks and filesystem accounting information: done
```

```
sudo mkdir -p /data
```

```
sudo mount -o discard,defaults /dev/sdb /data
```
```
sudo chmod a+w /data
```



```
df -h
```

```
sudo cp /etc/fstab /etc/fstab.backup
```



Execute the following command to make a fstab entry with the UUID of the disk.

```
$ echo UUID=`sudo blkid -s UUID -o value /dev/sdb` /data ext4 discard,defaults,nofail 0 2 | sudo tee -a /etc/fstab
UUID=f32bdbb2-f937-44c0-a45f-64007374db66 /data ext4 discard,defaults,nofail 0 2
```

Check the UUID of the extra disk
```
sudo blkid -s UUID -o value /dev/sdb
f32bdbb2-f937-44c0-a45f-64007374db66
```

Open fstab file and check for the new entry for the UUID of the extra disk

```
$ sudo cat /etc/fstab
# /etc/fstab: static file system information
UUID=59af2a10-b9ae-4d14-94db-29555eafcabc / ext4 rw,discard,errors=remount-ro,x-systemd.growfs 0 0
UUID=ED6A-504D /boot/efi vfat defaults 0 0
UUID=f32bdbb2-f937-44c0-a45f-64007374db66 /data ext4 discard,defaults,nofail 0 2
```


```
sudo umount /data
```
