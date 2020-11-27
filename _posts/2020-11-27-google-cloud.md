

list available extra disk
```
sudo lsblk
```

```
sudo mkfs.ext4 -m 0 -F -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb
```

```
sudo mkdir -p /data
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
echo UUID=`sudo blkid -s UUID -o value /dev/sdb` /data ext4 discard,defaults,nofail 0 2 | sudo tee -a /etc/fstab
```

Check the UUID of the extra disk
```
sudo blkid -s UUID -o value /dev/sdb
```

Open fstab file and check for the new entry for the UUID of the extra disk

```
sudo cat /etc/fstab
```


```
sudo umount /data
```
