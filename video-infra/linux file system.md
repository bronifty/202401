![](./media/linux-file-system.png)
- /bin is os binaries 
- /usr is unix system resources (/usr/local/bin is where sysadmin installs user aka non-system apps) 
- /sbin is sysadmin utils 
- /lib is library modules shared by /bin and /sbin (/usr/bin has a copy of /bin) 
- /etc is config files for networking, authentication, etc (eg ssh_config) 
- /home and /root are user folders 
- /var is for logs and caches (home of volatile os app state) 
- /run is systemd sessions and logging used by sockets (files - eg mysql.sock) 
- /proc & /sys are low level process and system logs related to system processes and the underlying systems such as firmware or lower level software that facilitates comms with hardware
cf https://www.youtube.com/watch?v=bbmWOjuFmgA
