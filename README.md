# fluent-docker
Fluent 6.3 docker image based on CentOS 7 with VNC

```
docker pull centos:centos7
docker run -d -it -p 5959:5901 --name fluent centos:centos7
docker start -i fluent
```

```
cd ~
echo "
[base]
name=CentOS-7 - Base
baseurl=http://vault.centos.org/7.9.2009/os/x86_64/
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[updates]
name=CentOS-7 - Updates
baseurl=http://vault.centos.org/7.9.2009/updates/x86_64/
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[extras]
name=CentOS-7 - Extras
baseurl=http://vault.centos.org/7.9.2009/extras/x86_64/
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[centosplus]
name=CentOS-7 - Plus
baseurl=http://vault.centos.org/7.9.2009/centosplus/x86_64/
# mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
" > /etc/yum.repos.d/CentOS-Base.repo
```

```
yum clean all
yum makecache
```

```
yum install libjpeg-turbo -y
yum install libXt -y
yum install compat-libstdc++-33.x86_64 -y
yum install tigervnc-server -y
yum install xterm -y
yum install epel-release -y
yum install icewm -y
```

```
vncserver
```

```
echo "
#!/bin/sh

unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
/etc/X11/xinit/xinitrc

xterm &
icewm &

" > /root/.vnc/xstartup
```


