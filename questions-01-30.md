### Linux Admin Interview Questions and Answers

**1. How do you find which users have sudo privileges?**
✅ `getent group sudo`
👉 This lists members of the sudo group. On CentOS, use: `getent group wheel`

**2. System uptime?**
✅ `uptime`
✔️ Also: `cat /proc/uptime`

**3. How do you check the number of open file descriptors for a process?**
✅ `ls /proc/<pid>/fd | wc -l`
✔️ Replace `<pid>` with the actual process ID.

**4. How do you list all environment variables?**
✅ `printenv`
✔️ Also: `env`

**5. How do you check the default gateway of a Linux system?**
✅ `ip route show | grep default`
✔️ Alternatively: `ip r`

**6. How do you clear swap memory without rebooting?**
✅ `sudo swapoff -a && sudo swapon -a`

**7. How do you find the number of CPUs in Linux?**
✅ `nproc`
✔️ Also: `lscpu | grep "^CPU(s):"`

**8. How do you see system load averages?**
✅ `uptime`
✅ `cat /proc/loadavg`

**9. How do you find Linux distro name?**
✅ `cat /etc/os-release`
✔️ Or: `lsb_release -a` (if available)

**10. How do you block all incoming connections except SSH?**
✅

```bash
sudo ufw default deny incoming  
sudo ufw allow ssh  
sudo ufw enable
```

**11. How do you check disk I/O usage?**
✅ `iostat -x 1`
✔️ `iostat` comes from `sysstat` package. Also try `iotop`.

**12. Which process is consuming the most memory?**
✅ `ps aux --sort=-%mem | head -5`

**13. How to copy files from one server to another using SSH?**
✅ `scp file.txt user@remote_host:/path/`
✔️ Or: `rsync -avz file.txt user@remote_host:/path/`

**14. How do you forcefully unmount an NFS mount?**
✅ `sudo umount -f /mnt/nfs`
✔️ Replace `/mnt/nfs` with your actual mount point.

**15. How do you see inode usage of the filesystem?**
✅ `df -i`

**16. How do you create a symlink?**
✅ `ln -s /path/to/target /path/to/symlink`

**17. How do you schedule a shutdown for a specific time?**
✅ `sudo shutdown -h 2:00`
✔️ To cancel: `sudo shutdown -c`

**18. How do you check disk space usage?**
✅ `df -h`
✔️ Shows usage in human-readable format.

**19. How do you view memory usage?**
✅ `free -h`
✔️ Or: `top`, `htop` for live view

**20. How do you list all active network connections?**
✅ `ss -tuln`
✔️ Also: `netstat -tuln` (older systems)

**21. How do you restart a service in systemd?**
✅ `sudo systemctl restart <service-name>`
✔️ Replace `<service-name>` with e.g. `nginx`

**22. How do you find which port a process is using?**
✅ `sudo lsof -i -P -n | grep LISTEN`
✔️ Or: `ss -ltnp`

**23. How do you find the size of a directory?**
✅ `du -sh /path/to/directory`

**24. How do you find the last 100 lines of a log file?**
✅ `tail -n 100 /var/log/syslog`
✔️ Or: `tail -f` to follow in real-time

**25. How do you add a user to a group?**
✅ `sudo usermod -aG groupname username`

**26. How do you kill a process by name?**
✅ `pkill <process-name>`
✔️ Or: `kill $(pidof <process-name>)`

**27. How do you find failed login attempts?**
✅ `sudo grep "Failed password" /var/log/auth.log`

**28. How do you find the current runlevel?**
✅ `runlevel`
✔️ Or: `who -r`

**29. How do you set a static IP address permanently?**
✅ **Ubuntu (Netplan):**
Edit:

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```

Example:

```yaml
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: no
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

Apply changes:

```bash
sudo netplan apply
```

✅ **CentOS/RHEL:**
Edit:

```bash
sudo nano /etc/sysconfig/network-scripts/ifcfg-eth0
```

Example:

```
DEVICE=eth0
BOOTPROTO=none
ONBOOT=yes
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
```

Then:

```bash
sudo systemctl restart network
```

**30. How do you check SELinux status?**
✅ `sestatus`
✔️ Or: `getenforce`
