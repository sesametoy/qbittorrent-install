qbittorrent installer centos7
===============================
```
#yum install -y epel-release

#yum update -y

#yum install -y qbittorrent-nox
```
===============================

qbittorrent installer centos7
===============================
```
#yum install -y epel-release

#yum update -y

#yum install -y qbittorrent-nox
```
===============================

首先执行qbittorrent程序
===============================
```
#qbittorrent-nox 

Press 'y' key to accept and continue...
```
按 y
===============================

设置开机启动
===============================
```
#vi /usr/lib/systemd/system/qbittorrent.service

[Unit]

Description=qbittorrent torrent server

[Service]

User=root

ExecStart=/usr/bin/qbittorrent-nox

Restart=on-abort

[Install]

WantedBy=multi-user.target

systemctl daemon-reload

systemctl restart qbittorrent

systemctl enable qbittorrent
```
===============================

设置qbittorrent 参数
===============================
```
# .config/qBittorrent/qBittorent.conf
```
===============================



打开防火墙
==================
```
#firewall-cmd --zone=public --add-port=8080/tcp --permanent

#firewall-cmd --zone=public --add-port=8080/udp --permanent

#firewall-cmd --reload

#sudo firewall-cmd --reload

===============================
