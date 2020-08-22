Transmission installer centos7
===============================
```
#yum install -y epel-release

#yum update -y

#yum install -y transmission-daemon
```
===============================


设置启动
===============================
```
#systemctl start transmission-daemon
#systemctl stop transmission-daemon


```
===============================

设置transmission 参数
===============================
```
# vi /var/lib/transmission/.config/transmission-daemon/settings.json
dht-enabled : false
rpc-whitelist: 192.168.1.*
dht-enabled: false
```
===============================

挂载NFS 兴建下载目录
===============================
```
# yum install -y nfs-utils
# mkdir /mnt/download
# cd /mnt/download

# mkdir movie tvshow action seeds

# vi /etc/fstab
192.168.1.XX:/Home30T/30TZFS/Video/Movie /mnt/download/movie nfs4 rw,hard,intr,proto=tcp     0 0
192.168.1.XX:/Home30T/30TZFS/Video/TV_Series /mnt/download/tvshow nfs4 rw,hard,intr,proto=tcp     0 0
192.168.1.XX:/Home30T/30TZFS/Download/Action /mnt/download/action nfs4 rw,hard,intr,proto=tcp     0 0
192.168.1.XX:/Home30T/30TZFS/Download/seeds /mnt/download/seeds nfs4 rw,hard,intr,proto=tcp     0 0

```
===============================

安装flexget
===============================
```
# yum install python-pip
# pip install --upgrade pip
# pip install --upgrade setuptools
# pip install flexget
```
===============================

设置flexget
===============================
```
# mkdir /etc/flexget
# cd /etc/flexget/
# vi config.yml
tasks:
  movie:
    rss: https://.....
    accept_all: yes
    download: /mnt/download/seeds
    transmission:
      host: localhost
      port: 9091
      path: /mnt/download/movie

  action:
    rss: https://.....
    accept_all: yes
    download: /mnt/download/seeds
    transmission:
      host: localhost
      port: 9091
      path: /mnt/download/action
  tvshow:
    rss: https://.......
    accept_all: yes
    download: /mnt/download/seeds
    transmission:
      host: localhost
      port: 9091
      path: /mnt/download/tvshow

schedules:
  # Run every task once an hour
  - tasks: '*'
    interval:
      minutes: 2

```
===============================

打开防火墙
==================
```
#firewall-cmd --zone=public --add-port=9091/tcp --permanent

#firewall-cmd --reload
```
===============================

启动transmission, flexget
==================
```
# systemctl start transmission-daemon
# systemctl enable transmission-daemon
# cd /etc/flexget
# flexget daemon start -d

```
===============================

每次机器重启, 重新加载flexget
==================
```
# cd /etc/flexget
# flexget daemon start -d

```
===============================
