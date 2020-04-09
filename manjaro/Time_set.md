###解决Manjaro(archLinux)系统时间快8小时

设置时区: sudo ln -sf /usr/share/zoneinfo/Asia/Shanghai/etc/localtime
安装openNTPD: sudo pacman -S openntpd
重启openNTPD: systemctl restart openntpd
设置开机启动: systemctl enable openntpd
