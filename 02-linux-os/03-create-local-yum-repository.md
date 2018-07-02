# Create Local Yum Repository
## Mount CentOS Everything DVD ISO image to Virtual Machine
```bash
mount -t auto /dev/cdrom /media/

result:
mount: /dev/sr0 is write-protected, mounting read-only
```
## Configure Yum repository source to current path
```bash
# Prohibit access to public network installation sources
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak

# Set access local installation sources
vi /etc/yum.repos.d/CentOS-Media.repo

####### from:
# [c7-media]
# name=CentOS-$releasever - Media
# baseurl=file:///media/CentOS/
#         file:///media/cdrom/
#         file:///media/cdrecorder/
# gpgcheck=1
# enabled=0
# gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
####### to:
# [c7-media]
# name=CentOS-$releasever - Media
# baseurl=file:///media/
# gpgcheck=1
# enabled=1
# gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

# Clear yum cache
yum clean all

result:
Loaded plugins: fastestmirror
Cleaning repos: c7-media
Cleaning up everything
Maybe you want: rm -rf /var/cache/yum, to also free up space taken by orphaned data from disabled or removed repos

# Remake yum cache
yum makecache
result:
Loaded plugins: fastestmirror
Determining fastest mirrors
c7-media                                                                                                                                      | 3.6 kB  00:00:00
(1/4): c7-media/group_gz                                                                                                                      | 166 kB  00:00:00
(2/4): c7-media/primary_db                                                                                                                    | 5.9 MB  00:00:00
(3/4): c7-media/filelists_db                                                                                                                  | 6.9 MB  00:00:00
(4/4): c7-media/other_db                                                                                                                      | 2.5 MB  00:00:00
Metadata Cache Created
```
## Setup Apache Web Server
```bash
yum install httpd -y

result:
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
Resolving Dependencies
--> Running transaction check
---> Package httpd.x86_64 0:2.4.6-80.el7.centos will be installed
--> Processing Dependency: httpd-tools = 2.4.6-80.el7.centos for package: httpd-2.4.6-80.el7.centos.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.4.6-80.el7.centos.x86_64
--> Processing Dependency: libaprutil-1.so.0()(64bit) for package: httpd-2.4.6-80.el7.centos.x86_64
--> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.4.6-80.el7.centos.x86_64
--> Running transaction check
---> Package apr.x86_64 0:1.4.8-3.el7_4.1 will be installed
---> Package apr-util.x86_64 0:1.5.2-6.el7 will be installed
---> Package httpd-tools.x86_64 0:2.4.6-80.el7.centos will be installed
---> Package mailcap.noarch 0:2.1.41-2.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=====================================================================================================================================================================
 Package                                Arch                              Version                                          Repository                           Size
=====================================================================================================================================================================
Installing:
 httpd                                  x86_64                            2.4.6-80.el7.centos                              c7-media                            2.7 M
Installing for dependencies:
 apr                                    x86_64                            1.4.8-3.el7_4.1                                  c7-media                            103 k
 apr-util                               x86_64                            1.5.2-6.el7                                      c7-media                             92 k
 httpd-tools                            x86_64                            2.4.6-80.el7.centos                              c7-media                             89 k
 mailcap                                noarch                            2.1.41-2.el7                                     c7-media                             31 k

Transaction Summary
=====================================================================================================================================================================
Install  1 Package (+4 Dependent packages)

Total download size: 3.0 M
Installed size: 10 M
Downloading packages:
warning: /media/Packages/apr-1.4.8-3.el7_4.1.x86_64.rpm: Header V3 RSA/SHA256 Signature, key ID f4a80eb5: NOKEY
Public key for apr-1.4.8-3.el7_4.1.x86_64.rpm is not installed
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                5.2 MB/s | 3.0 MB  00:00:00
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Importing GPG key 0xF4A80EB5:
 Userid     : "CentOS-7 Key (CentOS 7 Official Signing Key) <security@centos.org>"
 Fingerprint: 6341 ab27 53d7 8a78 a7c2 7bb1 24c6 a8a7 f4a8 0eb5
 Package    : centos-release-7-5.1804.el7.centos.x86_64 (@anaconda)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : apr-1.4.8-3.el7_4.1.x86_64                                                                                                                        1/5
  Installing : apr-util-1.5.2-6.el7.x86_64                                                                                                                       2/5
  Installing : httpd-tools-2.4.6-80.el7.centos.x86_64                                                                                                            3/5
  Installing : mailcap-2.1.41-2.el7.noarch                                                                                                                       4/5
  Installing : httpd-2.4.6-80.el7.centos.x86_64                                                                                                                  5/5
  Verifying  : httpd-tools-2.4.6-80.el7.centos.x86_64                                                                                                            1/5
  Verifying  : apr-1.4.8-3.el7_4.1.x86_64                                                                                                                        2/5
  Verifying  : mailcap-2.1.41-2.el7.noarch                                                                                                                       3/5
  Verifying  : httpd-2.4.6-80.el7.centos.x86_64                                                                                                                  4/5
  Verifying  : apr-util-1.5.2-6.el7.x86_64                                                                                                                       5/5

Installed:
  httpd.x86_64 0:2.4.6-80.el7.centos

Dependency Installed:
  apr.x86_64 0:1.4.8-3.el7_4.1         apr-util.x86_64 0:1.5.2-6.el7         httpd-tools.x86_64 0:2.4.6-80.el7.centos         mailcap.noarch 0:2.1.41-2.el7

Complete!

```
## Startup Apache Web Server
```bash
# Start Apache Web Server
systemctl start httpd
# Enable Apache Web Server automatic startup with OS boot
systemctl enable httpd

result:
Created symlink from /etc/systemd/system/multi-user.target.wants/httpd.service to /usr/lib/systemd/system/httpd.service.
```
> P.S. Other command
```bash
# Check Apache Web Service Status
systemctl status httpd

# Stop Apache Web Service
systemctl stop httpd

# Disable Apache web service automatic startup with OS boot
systemctl disable httpd
```
## Copy RPM Packages to Target Floder
```bash
cp -a /media/Packages/* /var/www/html/
```
## Set Apache Web Service Configure Files
```bash
vi /etc/httpd/conf/httpd.conf

# from:
# Options Indexes FollowSymLinks
# to:
# Options All Indexes FollowSymLinks

# remove default welcome page
rm -rf /etc/httpd/conf.d/welcome.conf

# restrat apache web service
systemctl restart httpd

# Verify
text command: curl IP/localhost
browser: http://IP
```
## Set firewall configure
```bash
# Stop and Disable Firewall Service
systemctl stop firewalld
systemctl disable firewalld

result:
Removed symlink /etc/systemd/system/multi-user.target.wants/firewalld.service.
Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.

# Disable SELinux
vi /etc/selinux/config

# from:
# SELINUX=enforcing
# to:
# SELINUX=disabled

# Reboot OS
reboot
```
## Installation createrepo Tools
```bash
yum install createrepo -y

result:
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
Resolving Dependencies
--> Running transaction check
---> Package createrepo.noarch 0:0.9.9-28.el7 will be installed
--> Processing Dependency: python-deltarpm for package: createrepo-0.9.9-28.el7.noarch
--> Processing Dependency: libxml2-python for package: createrepo-0.9.9-28.el7.noarch
--> Processing Dependency: deltarpm for package: createrepo-0.9.9-28.el7.noarch
--> Running transaction check
---> Package deltarpm.x86_64 0:3.6-3.el7 will be installed
---> Package libxml2-python.x86_64 0:2.9.1-6.el7_2.3 will be installed
---> Package python-deltarpm.x86_64 0:3.6-3.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=====================================================================================================================================================================
 Package                                    Arch                              Version                                      Repository                           Size
=====================================================================================================================================================================
Installing:
 createrepo                                 noarch                            0.9.9-28.el7                                 c7-media                             94 k
Installing for dependencies:
 deltarpm                                   x86_64                            3.6-3.el7                                    c7-media                             82 k
 libxml2-python                             x86_64                            2.9.1-6.el7_2.3                              c7-media                            247 k
 python-deltarpm                            x86_64                            3.6-3.el7                                    c7-media                             31 k

Transaction Summary
=====================================================================================================================================================================
Install  1 Package (+3 Dependent packages)

Total download size: 454 k
Installed size: 2.0 M
Downloading packages:
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                651 kB/s | 454 kB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : deltarpm-3.6-3.el7.x86_64                                                                                                                         1/4
  Installing : python-deltarpm-3.6-3.el7.x86_64                                                                                                                  2/4
  Installing : libxml2-python-2.9.1-6.el7_2.3.x86_64                                                                                                             3/4
  Installing : createrepo-0.9.9-28.el7.noarch                                                                                                                    4/4
  Verifying  : createrepo-0.9.9-28.el7.noarch                                                                                                                    1/4
  Verifying  : libxml2-python-2.9.1-6.el7_2.3.x86_64                                                                                                             2/4
  Verifying  : deltarpm-3.6-3.el7.x86_64                                                                                                                         3/4
  Verifying  : python-deltarpm-3.6-3.el7.x86_64                                                                                                                  4/4

Installed:
  createrepo.noarch 0:0.9.9-28.el7

Dependency Installed:
  deltarpm.x86_64 0:3.6-3.el7                     libxml2-python.x86_64 0:2.9.1-6.el7_2.3                     python-deltarpm.x86_64 0:3.6-3.el7

Complete!
```
## Initializing repository
```bash
createrepo /var/www/html

result:
Spawning worker 0 with 1239 pkgs
Spawning worker 1 with 1239 pkgs
Spawning worker 2 with 1239 pkgs
Spawning worker 3 with 1239 pkgs
Spawning worker 4 with 1239 pkgs
Spawning worker 5 with 1239 pkgs
Spawning worker 6 with 1239 pkgs
Spawning worker 7 with 1238 pkgs
Workers Finished
Saving Primary metadata
Saving file lists metadata
Saving other metadata
Generating sqlite DBs
Sqlite DBs complete
```
## Configure Client Yum repository
```bash
vi /etc/yum.repos.d/CentOS-Media.repo

[c7-media]
name=CentOS-$releasever - Media
baseurl=file:///media/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

[c7-remote]
name=CentOS-$releasever - Media
baseurl=http://192.168.0.31
gpgcheck=0
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

yum clean all
yum makecache

result:
Loaded plugins: fastestmirror
Determining fastest mirrors
c7-remote                                                                                                                                     | 2.9 kB  00:00:00
(1/3): c7-remote/filelists_db                                                                                                                 | 6.9 MB  00:00:00
(2/3): c7-remote/primary_db                                                                                                                   | 5.9 MB  00:00:00
(3/3): c7-remote/other_db                                                                                                                     | 2.5 MB  00:00:00
Metadata Cache Created
```
> P.S. Must be remove CentOS-Base.repo file
```bash
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak
or
rm -rf /etc/yum.repos.d/CentOS-Base.repo
```

## Done
Now we can use yum install centos packages by local yum repository

```bash
# Verify local yum repository
yum install net-tools -y

result:
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
Resolving Dependencies
--> Running transaction check
---> Package net-tools.x86_64 0:2.0-0.22.20131004git.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=====================================================================================================================================================================
 Package                             Arch                             Version                                              Repository                           Size
=====================================================================================================================================================================
Installing:
 net-tools                           x86_64                           2.0-0.22.20131004git.el7                             c7-remote                           305 k

Transaction Summary
=====================================================================================================================================================================
Install  1 Package

Total download size: 305 k
Installed size: 917 k
Downloading packages:
net-tools-2.0-0.22.20131004git.el7.x86_64.rpm                                                                                                 | 305 kB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : net-tools-2.0-0.22.20131004git.el7.x86_64                                                                                                         1/1
  Verifying  : net-tools-2.0-0.22.20131004git.el7.x86_64                                                                                                         1/1

Installed:
  net-tools.x86_64 0:2.0-0.22.20131004git.el7

Complete!
```