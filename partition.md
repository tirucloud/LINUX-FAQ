```bash
lsblk
fdisk -l
sudo fdisk /dev/xvdbb

n

p

1

first sector :enter
last sectro: +3G
t
L

8e

wq

sudo mkfs -t ext4 /dev/xvdbb1
sudo mkdir /data
sudo mount /dev/xvdbb1 /data

sudo blkid

nano /etc/fstab

sudo mount -a
```



