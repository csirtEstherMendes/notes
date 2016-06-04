## List all repositories and PPAs 
```
egrep -v '^#|^ *$' /etc/apt/sources.list /etc/apt/sources.list.d/*
```

## Strace
Single process
```
sudo strace -p `pidof apache2 | tr ' ' ','`
```
Multiple processes
```
sudo strace -f -tt -o /tmp/php.trace -s1024 -p `pidof php5-fpm | tr ' ' ','`
```
Alternative:
```
strace -tt -s2048 $(pidof httpd |sed 's/\([0-9]*\)/\-p \1/g')
```

## Single boot in Centos 7
Step 1: On the boot, press any key to enter in grub2 menu

Step 2: Press “e” key to edit arguments of kernel.

Step 3: Go to second last line (Starts with linux 16 or linuxefi) using up and down arrow then modify the ""ro"" argument.

Step 4: Modify it to “rw init=/sysroot/bin/sh”. Once done, press “Ctrl+x”

Step 5: Boot and enter the operative system

Step 5: Boot and enter the operative system
```
chroot /sysroot
```

## Cron.daily doesn’t run in Centos 7
```
yum -y install cronie-noanacron
```

## Kill processes orphaned
```
kill -9 `pidof -x 'ansible-playbook'`
```

## Verify permissions file with stat

```
[root@Niflheim tmp]# ls -alF .
total 1632
drwxrwxrwt 15 root root    4096 Apr  7 04:24 ./
drwxr-xr-x 28 root root    4096 Apr  2 21:02 ../
[root@Niflheim tmp]# stat -c '%A %a %n' .
drwxrwxrwt 1777 .

```

## Runnig Redis Monitor

```
redis-cli monitor
```
or 
```
telnet localhost 6379
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
MONITOR
+OK
```
Alternative way, via ngrep
```
ngrep -d any -pqt -W single '' port 6379
```