# Installation Pacemaker Cluster
## Add IP and Node Alias to each nodes hosts file
```bash
echo '192.168.0.21 sqll01' >> /etc/hosts
echo '192.168.0.22 sqll02' >> /etc/hosts
echo '192.168.0.23 sqll03' >> /etc/hosts
echo '192.168.0.24 sqll04' >> /etc/hosts
echo '192.168.0.25 sqll05' >> /etc/hosts
echo '192.168.0.26 sqll06' >> /etc/hosts
echo '192.168.0.27 sqll07' >> /etc/hosts
echo '192.168.0.28 sqll08' >> /etc/hosts
echo '192.168.0.29 sqll09' >> /etc/hosts
```
## Enable SQL Server Availability Group Feature on each nodes
```bash
/opt/mssql/bin/mssql-conf set hadr.hadrenabled  1

result:
SQL Server needs to be restarted in order to apply this setting. Please run
'systemctl restart mssql-server.service'.

systemctl restart mssql-server
```
## Synchronization date time on each nodes
```bash
ntpdate 192.168.0.30
```
## Installation Pacemaker on each nodes
```bash
yum install pacemaker pcs fence-agents-all resource-agents -y

result:
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
c7-remote                                                                                                                                     | 2.9 kB  00:00:00
Resolving Dependencies
--> Running transaction check
---> Package fence-agents-all.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: fence-agents-wti >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-vmware-soap >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-vmware-rest >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-scsi >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-sbd >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-rsb >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-rsa >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-rhevm >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-mpath >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-kdump >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-ipmilan >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-ipdu >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-intelmodular >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-ilo2 >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-ilo-ssh >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-ilo-mp >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-ilo-moonshot >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-ifmib >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-ibmblade >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-hpblade >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-heuristics-ping >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-eps >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-emerson >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-eaton-snmp >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-drac5 >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-compute >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-cisco-ucs >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-cisco-mds >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-brocade >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-bladecenter >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-apc-snmp >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-apc >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-amt-ws >= 4.0.11-86.el7 for package: fence-agents-all-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-virt for package: fence-agents-all-4.0.11-86.el7.x86_64
---> Package pacemaker.x86_64 0:1.1.18-11.el7 will be installed
--> Processing Dependency: pacemaker-libs = 1.1.18-11.el7 for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: pacemaker-cluster-libs = 1.1.18-11.el7 for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: pacemaker-cli = 1.1.18-11.el7 for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libqb > 0.17.0 for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libquorum.so.5(COROSYNC_QUORUM_1.0)(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libgnutls.so.28(GNUTLS_1_4)(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcpg.so.4(COROSYNC_CPG_1.0)(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcmap.so.4(COROSYNC_CMAP_1.0)(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcfg.so.6(COROSYNC_CFG_0.82)(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: corosync for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libxslt.so.1()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libtransitioner.so.2()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libstonithd.so.2()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libquorum.so.5()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libqb.so.0()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libpengine.so.10()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libpe_status.so.10()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libpe_rules.so.2()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: liblrmd.so.1()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libgnutls.so.28()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcrmservice.so.3()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcrmcommon.so.3()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcrmcluster.so.4()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcpg.so.4()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcorosync_common.so.4()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcmap.so.4()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcib.so.4()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
--> Processing Dependency: libcfg.so.6()(64bit) for package: pacemaker-1.1.18-11.el7.x86_64
---> Package pcs.x86_64 0:0.9.162-5.el7.centos will be installed
--> Processing Dependency: ruby >= 2.0.0 for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: python-clufter >= 0.59.0 for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: rubygem-json for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: python-setuptools for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: python-lxml for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: psmisc for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: overpass-fonts for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: liberation-sans-fonts for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: /usr/bin/ruby for package: pcs-0.9.162-5.el7.centos.x86_64
--> Processing Dependency: libruby.so.2.0()(64bit) for package: pcs-0.9.162-5.el7.centos.x86_64
---> Package resource-agents.x86_64 0:3.9.5-124.el7 will be installed
--> Processing Dependency: bc for package: resource-agents-3.9.5-124.el7.x86_64
--> Processing Dependency: /usr/sbin/rpc.nfsd for package: resource-agents-3.9.5-124.el7.x86_64
--> Processing Dependency: /usr/sbin/rpc.mountd for package: resource-agents-3.9.5-124.el7.x86_64
--> Processing Dependency: /usr/sbin/mount.cifs for package: resource-agents-3.9.5-124.el7.x86_64
--> Processing Dependency: /usr/sbin/lvm for package: resource-agents-3.9.5-124.el7.x86_64
--> Processing Dependency: /sbin/rpc.statd for package: resource-agents-3.9.5-124.el7.x86_64
--> Processing Dependency: /sbin/mount.nfs4 for package: resource-agents-3.9.5-124.el7.x86_64
--> Processing Dependency: /sbin/mount.nfs for package: resource-agents-3.9.5-124.el7.x86_64
--> Processing Dependency: /bin/netstat for package: resource-agents-3.9.5-124.el7.x86_64
--> Running transaction check
---> Package bc.x86_64 0:1.06.95-13.el7 will be installed
---> Package cifs-utils.x86_64 0:6.2-10.el7 will be installed
--> Processing Dependency: libwbclient.so.0(WBCLIENT_0.9)(64bit) for package: cifs-utils-6.2-10.el7.x86_64
--> Processing Dependency: libtalloc.so.2(TALLOC_2.0.2)(64bit) for package: cifs-utils-6.2-10.el7.x86_64
--> Processing Dependency: keyutils for package: cifs-utils-6.2-10.el7.x86_64
--> Processing Dependency: libwbclient.so.0()(64bit) for package: cifs-utils-6.2-10.el7.x86_64
--> Processing Dependency: libtalloc.so.2()(64bit) for package: cifs-utils-6.2-10.el7.x86_64
---> Package corosync.x86_64 0:2.4.3-2.el7 will be installed
--> Processing Dependency: libcgroup.so.1(CGROUP_0.32.1)(64bit) for package: corosync-2.4.3-2.el7.x86_64
--> Processing Dependency: libcgroup.so.1(CGROUP_0.32)(64bit) for package: corosync-2.4.3-2.el7.x86_64
--> Processing Dependency: libnetsnmp.so.31()(64bit) for package: corosync-2.4.3-2.el7.x86_64
--> Processing Dependency: libcgroup.so.1()(64bit) for package: corosync-2.4.3-2.el7.x86_64
---> Package corosynclib.x86_64 0:2.4.3-2.el7 will be installed
---> Package fence-agents-amt-ws.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: openwsman-python >= 2.6.3-1.git4391e5c.el7 for package: fence-agents-amt-ws-4.0.11-86.el7.x86_64
--> Processing Dependency: fence-agents-common >= 4.0.11-86.el7 for package: fence-agents-amt-ws-4.0.11-86.el7.x86_64
---> Package fence-agents-apc.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-apc-snmp.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: net-snmp-utils for package: fence-agents-apc-snmp-4.0.11-86.el7.x86_64
---> Package fence-agents-bladecenter.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-brocade.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-cisco-mds.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-cisco-ucs.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-compute.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: python-requests for package: fence-agents-compute-4.0.11-86.el7.x86_64
---> Package fence-agents-drac5.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-eaton-snmp.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-emerson.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-eps.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-heuristics-ping.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-hpblade.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-ibmblade.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-ifmib.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-ilo-moonshot.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-ilo-mp.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-ilo-ssh.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-ilo2.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: gnutls-utils for package: fence-agents-ilo2-4.0.11-86.el7.x86_64
---> Package fence-agents-intelmodular.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-ipdu.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-ipmilan.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: /usr/bin/ipmitool for package: fence-agents-ipmilan-4.0.11-86.el7.x86_64
---> Package fence-agents-kdump.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-mpath.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: device-mapper-multipath for package: fence-agents-mpath-4.0.11-86.el7.x86_64
---> Package fence-agents-rhevm.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-rsa.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-rsb.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-sbd.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-scsi.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-vmware-rest.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-agents-vmware-soap.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: python-suds for package: fence-agents-vmware-soap-4.0.11-86.el7.x86_64
---> Package fence-agents-wti.x86_64 0:4.0.11-86.el7 will be installed
---> Package fence-virt.x86_64 0:0.3.2-13.el7 will be installed
---> Package gnutls.x86_64 0:3.3.26-9.el7 will be installed
--> Processing Dependency: trousers >= 0.3.11.2 for package: gnutls-3.3.26-9.el7.x86_64
--> Processing Dependency: libnettle.so.4()(64bit) for package: gnutls-3.3.26-9.el7.x86_64
--> Processing Dependency: libhogweed.so.2()(64bit) for package: gnutls-3.3.26-9.el7.x86_64
---> Package liberation-sans-fonts.noarch 1:1.07.2-16.el7 will be installed
--> Processing Dependency: liberation-fonts-common = 1:1.07.2-16.el7 for package: 1:liberation-sans-fonts-1.07.2-16.el7.noarch
---> Package libqb.x86_64 0:1.0.1-6.el7 will be installed
---> Package libxslt.x86_64 0:1.1.28-5.el7 will be installed
---> Package lvm2.x86_64 7:2.02.177-4.el7 will be installed
--> Processing Dependency: lvm2-libs = 7:2.02.177-4.el7 for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: device-mapper-persistent-data >= 0.7.0-0.1.rc6 for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: liblvm2app.so.2.2(Base)(64bit) for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: libdevmapper-event.so.1.02(Base)(64bit) for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: liblvm2app.so.2.2()(64bit) for package: 7:lvm2-2.02.177-4.el7.x86_64
--> Processing Dependency: libdevmapper-event.so.1.02()(64bit) for package: 7:lvm2-2.02.177-4.el7.x86_64
---> Package net-tools.x86_64 0:2.0-0.22.20131004git.el7 will be installed
---> Package nfs-utils.x86_64 1:1.3.0-0.54.el7 will be installed
--> Processing Dependency: libtirpc >= 0.2.4-0.7 for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
--> Processing Dependency: gssproxy >= 0.7.0-3 for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
--> Processing Dependency: rpcbind for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
--> Processing Dependency: quota for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
--> Processing Dependency: libnfsidmap for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
--> Processing Dependency: libevent for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
--> Processing Dependency: libtirpc.so.1()(64bit) for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
--> Processing Dependency: libnfsidmap.so.0()(64bit) for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
--> Processing Dependency: libevent-2.0.so.5()(64bit) for package: 1:nfs-utils-1.3.0-0.54.el7.x86_64
---> Package overpass-fonts.noarch 0:2.1-1.el7 will be installed
--> Processing Dependency: fontpackages-filesystem for package: overpass-fonts-2.1-1.el7.noarch
---> Package pacemaker-cli.x86_64 0:1.1.18-11.el7 will be installed
--> Processing Dependency: perl-TimeDate for package: pacemaker-cli-1.1.18-11.el7.x86_64
---> Package pacemaker-cluster-libs.x86_64 0:1.1.18-11.el7 will be installed
---> Package pacemaker-libs.x86_64 0:1.1.18-11.el7 will be installed
---> Package psmisc.x86_64 0:22.20-15.el7 will be installed
---> Package python-clufter.noarch 0:0.77.0-2.el7 will be installed
--> Processing Dependency: clufter-bin = 0.77.0-2.el7 for package: python-clufter-0.77.0-2.el7.noarch
---> Package python-lxml.x86_64 0:3.2.1-4.el7 will be installed
---> Package python-setuptools.noarch 0:0.9.8-7.el7 will be installed
--> Processing Dependency: python-backports-ssl_match_hostname for package: python-setuptools-0.9.8-7.el7.noarch
---> Package ruby.x86_64 0:2.0.0.648-33.el7_4 will be installed
--> Processing Dependency: rubygem(bigdecimal) >= 1.2.0 for package: ruby-2.0.0.648-33.el7_4.x86_64
--> Processing Dependency: ruby(rubygems) >= 2.0.14.1 for package: ruby-2.0.0.648-33.el7_4.x86_64
---> Package ruby-libs.x86_64 0:2.0.0.648-33.el7_4 will be installed
---> Package rubygem-json.x86_64 0:1.7.7-33.el7_4 will be installed
--> Running transaction check
---> Package clufter-bin.x86_64 0:0.77.0-2.el7 will be installed
--> Processing Dependency: clufter-common = 0.77.0-2.el7 for package: clufter-bin-0.77.0-2.el7.x86_64
---> Package device-mapper-event-libs.x86_64 7:1.02.146-4.el7 will be installed
---> Package device-mapper-multipath.x86_64 0:0.4.9-119.el7 will be installed
--> Processing Dependency: device-mapper-multipath-libs = 0.4.9-119.el7 for package: device-mapper-multipath-0.4.9-119.el7.x86_64
--> Processing Dependency: libmultipath.so.0()(64bit) for package: device-mapper-multipath-0.4.9-119.el7.x86_64
--> Processing Dependency: libmpathpersist.so.0()(64bit) for package: device-mapper-multipath-0.4.9-119.el7.x86_64
--> Processing Dependency: libmpathcmd.so.0()(64bit) for package: device-mapper-multipath-0.4.9-119.el7.x86_64
---> Package device-mapper-persistent-data.x86_64 0:0.7.3-3.el7 will be installed
--> Processing Dependency: libaio.so.1(LIBAIO_0.4)(64bit) for package: device-mapper-persistent-data-0.7.3-3.el7.x86_64
--> Processing Dependency: libaio.so.1(LIBAIO_0.1)(64bit) for package: device-mapper-persistent-data-0.7.3-3.el7.x86_64
--> Processing Dependency: libaio.so.1()(64bit) for package: device-mapper-persistent-data-0.7.3-3.el7.x86_64
---> Package fence-agents-common.x86_64 0:4.0.11-86.el7 will be installed
--> Processing Dependency: policycoreutils-python for package: fence-agents-common-4.0.11-86.el7.x86_64
--> Processing Dependency: pexpect for package: fence-agents-common-4.0.11-86.el7.x86_64
---> Package fontpackages-filesystem.noarch 0:1.44-8.el7 will be installed
---> Package gnutls-utils.x86_64 0:3.3.26-9.el7 will be installed
--> Processing Dependency: gnutls-dane(x86-64) = 3.3.26-9.el7 for package: gnutls-utils-3.3.26-9.el7.x86_64
--> Processing Dependency: libgnutls-dane.so.0(DANE_0_0)(64bit) for package: gnutls-utils-3.3.26-9.el7.x86_64
--> Processing Dependency: libunbound.so.2()(64bit) for package: gnutls-utils-3.3.26-9.el7.x86_64
--> Processing Dependency: libopts.so.25()(64bit) for package: gnutls-utils-3.3.26-9.el7.x86_64
--> Processing Dependency: libgnutls-dane.so.0()(64bit) for package: gnutls-utils-3.3.26-9.el7.x86_64
---> Package gssproxy.x86_64 0:0.7.0-17.el7 will be installed
--> Processing Dependency: libini_config >= 1.3.1-28 for package: gssproxy-0.7.0-17.el7.x86_64
--> Processing Dependency: libverto-module-base for package: gssproxy-0.7.0-17.el7.x86_64
--> Processing Dependency: libref_array.so.1(REF_ARRAY_0.1.1)(64bit) for package: gssproxy-0.7.0-17.el7.x86_64
--> Processing Dependency: libini_config.so.3(INI_CONFIG_1.2.0)(64bit) for package: gssproxy-0.7.0-17.el7.x86_64
--> Processing Dependency: libini_config.so.3(INI_CONFIG_1.1.0)(64bit) for package: gssproxy-0.7.0-17.el7.x86_64
--> Processing Dependency: libref_array.so.1()(64bit) for package: gssproxy-0.7.0-17.el7.x86_64
--> Processing Dependency: libini_config.so.3()(64bit) for package: gssproxy-0.7.0-17.el7.x86_64
--> Processing Dependency: libcollection.so.2()(64bit) for package: gssproxy-0.7.0-17.el7.x86_64
--> Processing Dependency: libbasicobjects.so.0()(64bit) for package: gssproxy-0.7.0-17.el7.x86_64
---> Package ipmitool.x86_64 0:1.8.18-7.el7 will be installed
--> Processing Dependency: OpenIPMI-modalias for package: ipmitool-1.8.18-7.el7.x86_64
---> Package keyutils.x86_64 0:1.5.8-3.el7 will be installed
---> Package libcgroup.x86_64 0:0.41-15.el7 will be installed
---> Package liberation-fonts-common.noarch 1:1.07.2-16.el7 will be installed
---> Package libevent.x86_64 0:2.0.21-4.el7 will be installed
---> Package libnfsidmap.x86_64 0:0.25-19.el7 will be installed
---> Package libtalloc.x86_64 0:2.1.10-1.el7 will be installed
---> Package libtirpc.x86_64 0:0.2.4-0.10.el7 will be installed
---> Package libwbclient.x86_64 0:4.7.1-6.el7 will be installed
--> Processing Dependency: samba-client-libs = 4.7.1-6.el7 for package: libwbclient-4.7.1-6.el7.x86_64
--> Processing Dependency: libreplace-samba4.so(SAMBA_4.7.1)(64bit) for package: libwbclient-4.7.1-6.el7.x86_64
--> Processing Dependency: libreplace-samba4.so()(64bit) for package: libwbclient-4.7.1-6.el7.x86_64
---> Package lvm2-libs.x86_64 7:2.02.177-4.el7 will be installed
--> Processing Dependency: device-mapper-event = 7:1.02.146-4.el7 for package: 7:lvm2-libs-2.02.177-4.el7.x86_64
---> Package net-snmp-libs.x86_64 1:5.7.2-32.el7 will be installed
---> Package net-snmp-utils.x86_64 1:5.7.2-32.el7 will be installed
---> Package nettle.x86_64 0:2.7.1-8.el7 will be installed
---> Package openwsman-python.x86_64 0:2.6.3-3.git4391e5c.el7 will be installed
--> Processing Dependency: libwsman1 = 2.6.3-3.git4391e5c.el7 for package: openwsman-python-2.6.3-3.git4391e5c.el7.x86_64
--> Processing Dependency: libwsman_curl_client_transport.so.1()(64bit) for package: openwsman-python-2.6.3-3.git4391e5c.el7.x86_64
--> Processing Dependency: libwsman_client.so.4()(64bit) for package: openwsman-python-2.6.3-3.git4391e5c.el7.x86_64
--> Processing Dependency: libwsman.so.1()(64bit) for package: openwsman-python-2.6.3-3.git4391e5c.el7.x86_64
---> Package perl-TimeDate.noarch 1:2.30-2.el7 will be installed
--> Processing Dependency: perl >= 5.002 for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl >= 5.000 for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(warnings) for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(vars) for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(utf8) for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(strict) for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(base) for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(Time::Local) for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(Exporter) for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(Carp) for package: 1:perl-TimeDate-2.30-2.el7.noarch
--> Processing Dependency: perl(:MODULE_COMPAT_5.16.3) for package: 1:perl-TimeDate-2.30-2.el7.noarch
---> Package python-backports-ssl_match_hostname.noarch 0:3.5.0.1-1.el7 will be installed
--> Processing Dependency: python-ipaddress for package: python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch
--> Processing Dependency: python-backports for package: python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch
---> Package python-requests.noarch 0:2.6.0-1.el7_1 will be installed
--> Processing Dependency: python-urllib3 >= 1.10.2-1 for package: python-requests-2.6.0-1.el7_1.noarch
--> Processing Dependency: python-chardet >= 2.2.1-1 for package: python-requests-2.6.0-1.el7_1.noarch
---> Package python-suds.noarch 0:0.4.1-5.el7 will be installed
---> Package quota.x86_64 1:4.01-17.el7 will be installed
--> Processing Dependency: quota-nls = 1:4.01-17.el7 for package: 1:quota-4.01-17.el7.x86_64
--> Processing Dependency: tcp_wrappers for package: 1:quota-4.01-17.el7.x86_64
---> Package rpcbind.x86_64 0:0.2.0-44.el7 will be installed
---> Package rubygem-bigdecimal.x86_64 0:1.2.0-33.el7_4 will be installed
---> Package rubygems.noarch 0:2.0.14.1-33.el7_4 will be installed
--> Processing Dependency: rubygem(rdoc) >= 4.0.0 for package: rubygems-2.0.14.1-33.el7_4.noarch
--> Processing Dependency: rubygem(psych) >= 2.0.0 for package: rubygems-2.0.14.1-33.el7_4.noarch
--> Processing Dependency: rubygem(io-console) >= 0.4.2 for package: rubygems-2.0.14.1-33.el7_4.noarch
---> Package trousers.x86_64 0:0.3.14-2.el7 will be installed
--> Running transaction check
---> Package OpenIPMI-modalias.x86_64 0:2.0.23-2.el7 will be installed
---> Package autogen-libopts.x86_64 0:5.18-5.el7 will be installed
---> Package clufter-common.noarch 0:0.77.0-2.el7 will be installed
---> Package device-mapper-event.x86_64 7:1.02.146-4.el7 will be installed
---> Package device-mapper-multipath-libs.x86_64 0:0.4.9-119.el7 will be installed
--> Processing Dependency: librados.so.2()(64bit) for package: device-mapper-multipath-libs-0.4.9-119.el7.x86_64
---> Package gnutls-dane.x86_64 0:3.3.26-9.el7 will be installed
---> Package libaio.x86_64 0:0.3.109-13.el7 will be installed
---> Package libbasicobjects.x86_64 0:0.1.1-29.el7 will be installed
---> Package libcollection.x86_64 0:0.7.0-29.el7 will be installed
---> Package libini_config.x86_64 0:1.3.1-29.el7 will be installed
--> Processing Dependency: libpath_utils.so.1(PATH_UTILS_0.2.1)(64bit) for package: libini_config-1.3.1-29.el7.x86_64
--> Processing Dependency: libpath_utils.so.1()(64bit) for package: libini_config-1.3.1-29.el7.x86_64
---> Package libref_array.x86_64 0:0.1.5-29.el7 will be installed
---> Package libverto-libevent.x86_64 0:0.2.5-4.el7 will be installed
---> Package libwsman1.x86_64 0:2.6.3-3.git4391e5c.el7 will be installed
---> Package perl.x86_64 4:5.16.3-292.el7 will be installed
--> Processing Dependency: perl-libs = 4:5.16.3-292.el7 for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Socket) >= 1.3 for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Scalar::Util) >= 1.10 for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl-macros for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl-libs for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(threads::shared) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(threads) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(constant) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Time::HiRes) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Storable) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Socket) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Scalar::Util) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Pod::Simple::XHTML) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Pod::Simple::Search) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Getopt::Long) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Filter::Util::Call) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(File::Temp) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(File::Spec::Unix) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(File::Spec::Functions) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(File::Spec) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(File::Path) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: perl(Cwd) for package: 4:perl-5.16.3-292.el7.x86_64
--> Processing Dependency: libperl.so()(64bit) for package: 4:perl-5.16.3-292.el7.x86_64
---> Package perl-Carp.noarch 0:1.26-244.el7 will be installed
---> Package perl-Exporter.noarch 0:5.68-3.el7 will be installed
---> Package perl-Time-Local.noarch 0:1.2300-2.el7 will be installed
---> Package pexpect.noarch 0:2.3-11.el7 will be installed
---> Package policycoreutils-python.x86_64 0:2.5-22.el7 will be installed
--> Processing Dependency: setools-libs >= 3.3.8-2 for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libsemanage-python >= 2.5-9 for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: audit-libs-python >= 2.1.3-4 for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: python-IPy for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libqpol.so.1(VERS_1.4)(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libqpol.so.1(VERS_1.2)(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libapol.so.4(VERS_4.0)(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: checkpolicy for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libqpol.so.1()(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
--> Processing Dependency: libapol.so.4()(64bit) for package: policycoreutils-python-2.5-22.el7.x86_64
---> Package python-backports.x86_64 0:1.0-8.el7 will be installed
---> Package python-chardet.noarch 0:2.2.1-1.el7_1 will be installed
---> Package python-ipaddress.noarch 0:1.0.16-2.el7 will be installed
---> Package python-urllib3.noarch 0:1.10.2-5.el7 will be installed
--> Processing Dependency: python-six for package: python-urllib3-1.10.2-5.el7.noarch
---> Package quota-nls.noarch 1:4.01-17.el7 will be installed
---> Package rubygem-io-console.x86_64 0:0.4.2-33.el7_4 will be installed
---> Package rubygem-psych.x86_64 0:2.0.0-33.el7_4 will be installed
--> Processing Dependency: libyaml-0.so.2()(64bit) for package: rubygem-psych-2.0.0-33.el7_4.x86_64
---> Package rubygem-rdoc.noarch 0:4.0.0-33.el7_4 will be installed
--> Processing Dependency: ruby(irb) = 2.0.0.648 for package: rubygem-rdoc-4.0.0-33.el7_4.noarch
---> Package samba-client-libs.x86_64 0:4.7.1-6.el7 will be installed
--> Processing Dependency: samba-common = 4.7.1-6.el7 for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: samba-common = 4.7.1-6.el7 for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.9)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.31)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.30)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.21)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.20)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.16)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.14)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.13)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0(TEVENT_0.9.12)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtdb.so.1(TDB_1.3.11)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtdb.so.1(TDB_1.3.0)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtdb.so.1(TDB_1.2.5)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtdb.so.1(TDB_1.2.2)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtdb.so.1(TDB_1.2.1)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libldb.so.1(LDB_1.1.30)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libldb.so.1(LDB_1.1.19)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libldb.so.1(LDB_1.1.1)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libldb.so.1(LDB_0.9.23)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libldb.so.1(LDB_0.9.15)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libldb.so.1(LDB_0.9.10)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libaesni-intel-samba4.so(SAMBA_4.7.1)(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtevent.so.0()(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libtdb.so.1()(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libldb.so.1()(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libcups.so.2()(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libavahi-common.so.3()(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libavahi-client.so.3()(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
--> Processing Dependency: libaesni-intel-samba4.so()(64bit) for package: samba-client-libs-4.7.1-6.el7.x86_64
---> Package tcp_wrappers.x86_64 0:7.6-77.el7 will be installed
---> Package unbound-libs.x86_64 0:1.6.6-1.el7 will be installed
--> Running transaction check
---> Package audit-libs-python.x86_64 0:2.8.1-3.el7 will be installed
---> Package avahi-libs.x86_64 0:0.6.31-19.el7 will be installed
---> Package checkpolicy.x86_64 0:2.5-6.el7 will be installed
---> Package cups-libs.x86_64 1:1.6.3-35.el7 will be installed
---> Package libldb.x86_64 0:1.2.2-1.el7 will be installed
---> Package libpath_utils.x86_64 0:0.2.1-29.el7 will be installed
---> Package librados2.x86_64 1:0.94.5-2.el7 will be installed
--> Processing Dependency: libboost_thread-mt.so.1.53.0()(64bit) for package: 1:librados2-0.94.5-2.el7.x86_64
--> Processing Dependency: libboost_system-mt.so.1.53.0()(64bit) for package: 1:librados2-0.94.5-2.el7.x86_64
---> Package libsemanage-python.x86_64 0:2.5-11.el7 will be installed
---> Package libtdb.x86_64 0:1.3.15-1.el7 will be installed
---> Package libtevent.x86_64 0:0.9.33-2.el7 will be installed
---> Package libyaml.x86_64 0:0.1.4-11.el7_0 will be installed
---> Package perl-File-Path.noarch 0:2.09-2.el7 will be installed
---> Package perl-File-Temp.noarch 0:0.23.01-3.el7 will be installed
---> Package perl-Filter.x86_64 0:1.49-3.el7 will be installed
---> Package perl-Getopt-Long.noarch 0:2.40-3.el7 will be installed
--> Processing Dependency: perl(Pod::Usage) >= 1.14 for package: perl-Getopt-Long-2.40-3.el7.noarch
--> Processing Dependency: perl(Text::ParseWords) for package: perl-Getopt-Long-2.40-3.el7.noarch
---> Package perl-PathTools.x86_64 0:3.40-5.el7 will be installed
---> Package perl-Pod-Simple.noarch 1:3.28-4.el7 will be installed
--> Processing Dependency: perl(Pod::Escapes) >= 1.04 for package: 1:perl-Pod-Simple-3.28-4.el7.noarch
--> Processing Dependency: perl(Encode) for package: 1:perl-Pod-Simple-3.28-4.el7.noarch
---> Package perl-Scalar-List-Utils.x86_64 0:1.27-248.el7 will be installed
---> Package perl-Socket.x86_64 0:2.010-4.el7 will be installed
---> Package perl-Storable.x86_64 0:2.45-3.el7 will be installed
---> Package perl-Time-HiRes.x86_64 4:1.9725-3.el7 will be installed
---> Package perl-constant.noarch 0:1.27-2.el7 will be installed
---> Package perl-libs.x86_64 4:5.16.3-292.el7 will be installed
---> Package perl-macros.x86_64 4:5.16.3-292.el7 will be installed
---> Package perl-threads.x86_64 0:1.87-4.el7 will be installed
---> Package perl-threads-shared.x86_64 0:1.43-6.el7 will be installed
---> Package python-IPy.noarch 0:0.75-6.el7 will be installed
---> Package python-six.noarch 0:1.9.0-2.el7 will be installed
---> Package ruby-irb.noarch 0:2.0.0.648-33.el7_4 will be installed
---> Package samba-common.noarch 0:4.7.1-6.el7 will be installed
---> Package samba-common-libs.x86_64 0:4.7.1-6.el7 will be installed
---> Package setools-libs.x86_64 0:3.3.8-2.el7 will be installed
--> Running transaction check
---> Package boost-system.x86_64 0:1.53.0-27.el7 will be installed
---> Package boost-thread.x86_64 0:1.53.0-27.el7 will be installed
---> Package perl-Encode.x86_64 0:2.51-7.el7 will be installed
---> Package perl-Pod-Escapes.noarch 1:1.04-292.el7 will be installed
---> Package perl-Pod-Usage.noarch 0:1.63-3.el7 will be installed
--> Processing Dependency: perl(Pod::Text) >= 3.15 for package: perl-Pod-Usage-1.63-3.el7.noarch
--> Processing Dependency: perl-Pod-Perldoc for package: perl-Pod-Usage-1.63-3.el7.noarch
---> Package perl-Text-ParseWords.noarch 0:3.29-4.el7 will be installed
--> Running transaction check
---> Package perl-Pod-Perldoc.noarch 0:3.20-4.el7 will be installed
--> Processing Dependency: perl(parent) for package: perl-Pod-Perldoc-3.20-4.el7.noarch
--> Processing Dependency: perl(HTTP::Tiny) for package: perl-Pod-Perldoc-3.20-4.el7.noarch
---> Package perl-podlators.noarch 0:2.5.1-3.el7 will be installed
--> Running transaction check
---> Package perl-HTTP-Tiny.noarch 0:0.033-3.el7 will be installed
---> Package perl-parent.noarch 1:0.225-244.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=====================================================================================================================================================================
 Package                                                 Arch                       Version                                      Repository                     Size
=====================================================================================================================================================================
Installing:
 fence-agents-all                                        x86_64                     4.0.11-86.el7                                c7-remote                      20 k
 pacemaker                                               x86_64                     1.1.18-11.el7                                c7-remote                     455 k
 pcs                                                     x86_64                     0.9.162-5.el7.centos                         c7-remote                     5.0 M
 resource-agents                                         x86_64                     3.9.5-124.el7                                c7-remote                     398 k
Installing for dependencies:
 OpenIPMI-modalias                                       x86_64                     2.0.23-2.el7                                 c7-remote                      16 k
 audit-libs-python                                       x86_64                     2.8.1-3.el7                                  c7-remote                      75 k
 autogen-libopts                                         x86_64                     5.18-5.el7                                   c7-remote                      66 k
 avahi-libs                                              x86_64                     0.6.31-19.el7                                c7-remote                      61 k
 bc                                                      x86_64                     1.06.95-13.el7                               c7-remote                     115 k
 boost-system                                            x86_64                     1.53.0-27.el7                                c7-remote                      40 k
 boost-thread                                            x86_64                     1.53.0-27.el7                                c7-remote                      57 k
 checkpolicy                                             x86_64                     2.5-6.el7                                    c7-remote                     294 k
 cifs-utils                                              x86_64                     6.2-10.el7                                   c7-remote                      85 k
 clufter-bin                                             x86_64                     0.77.0-2.el7                                 c7-remote                      25 k
 clufter-common                                          noarch                     0.77.0-2.el7                                 c7-remote                      72 k
 corosync                                                x86_64                     2.4.3-2.el7                                  c7-remote                     220 k
 corosynclib                                             x86_64                     2.4.3-2.el7                                  c7-remote                     131 k
 cups-libs                                               x86_64                     1:1.6.3-35.el7                               c7-remote                     357 k
 device-mapper-event                                     x86_64                     7:1.02.146-4.el7                             c7-remote                     185 k
 device-mapper-event-libs                                x86_64                     7:1.02.146-4.el7                             c7-remote                     184 k
 device-mapper-multipath                                 x86_64                     0.4.9-119.el7                                c7-remote                     137 k
 device-mapper-multipath-libs                            x86_64                     0.4.9-119.el7                                c7-remote                     257 k
 device-mapper-persistent-data                           x86_64                     0.7.3-3.el7                                  c7-remote                     405 k
 fence-agents-amt-ws                                     x86_64                     4.0.11-86.el7                                c7-remote                      24 k
 fence-agents-apc                                        x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-apc-snmp                                   x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-bladecenter                                x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-brocade                                    x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-cisco-mds                                  x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-cisco-ucs                                  x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-common                                     x86_64                     4.0.11-86.el7                                c7-remote                      63 k
 fence-agents-compute                                    x86_64                     4.0.11-86.el7                                c7-remote                      29 k
 fence-agents-drac5                                      x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-eaton-snmp                                 x86_64                     4.0.11-86.el7                                c7-remote                      24 k
 fence-agents-emerson                                    x86_64                     4.0.11-86.el7                                c7-remote                      22 k
 fence-agents-eps                                        x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-heuristics-ping                            x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-hpblade                                    x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-ibmblade                                   x86_64                     4.0.11-86.el7                                c7-remote                      22 k
 fence-agents-ifmib                                      x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-ilo-moonshot                               x86_64                     4.0.11-86.el7                                c7-remote                      22 k
 fence-agents-ilo-mp                                     x86_64                     4.0.11-86.el7                                c7-remote                      22 k
 fence-agents-ilo-ssh                                    x86_64                     4.0.11-86.el7                                c7-remote                      25 k
 fence-agents-ilo2                                       x86_64                     4.0.11-86.el7                                c7-remote                      24 k
 fence-agents-intelmodular                               x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-ipdu                                       x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-ipmilan                                    x86_64                     4.0.11-86.el7                                c7-remote                      31 k
 fence-agents-kdump                                      x86_64                     4.0.11-86.el7                                c7-remote                      33 k
 fence-agents-mpath                                      x86_64                     4.0.11-86.el7                                c7-remote                      24 k
 fence-agents-rhevm                                      x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-rsa                                        x86_64                     4.0.11-86.el7                                c7-remote                      22 k
 fence-agents-rsb                                        x86_64                     4.0.11-86.el7                                c7-remote                      22 k
 fence-agents-sbd                                        x86_64                     4.0.11-86.el7                                c7-remote                      24 k
 fence-agents-scsi                                       x86_64                     4.0.11-86.el7                                c7-remote                      26 k
 fence-agents-vmware-rest                                x86_64                     4.0.11-86.el7                                c7-remote                      23 k
 fence-agents-vmware-soap                                x86_64                     4.0.11-86.el7                                c7-remote                      24 k
 fence-agents-wti                                        x86_64                     4.0.11-86.el7                                c7-remote                      24 k
 fence-virt                                              x86_64                     0.3.2-13.el7                                 c7-remote                      41 k
 fontpackages-filesystem                                 noarch                     1.44-8.el7                                   c7-remote                     9.9 k
 gnutls                                                  x86_64                     3.3.26-9.el7                                 c7-remote                     677 k
 gnutls-dane                                             x86_64                     3.3.26-9.el7                                 c7-remote                      34 k
 gnutls-utils                                            x86_64                     3.3.26-9.el7                                 c7-remote                     237 k
 gssproxy                                                x86_64                     0.7.0-17.el7                                 c7-remote                     108 k
 ipmitool                                                x86_64                     1.8.18-7.el7                                 c7-remote                     441 k
 keyutils                                                x86_64                     1.5.8-3.el7                                  c7-remote                      54 k
 libaio                                                  x86_64                     0.3.109-13.el7                               c7-remote                      24 k
 libbasicobjects                                         x86_64                     0.1.1-29.el7                                 c7-remote                      25 k
 libcgroup                                               x86_64                     0.41-15.el7                                  c7-remote                      65 k
 libcollection                                           x86_64                     0.7.0-29.el7                                 c7-remote                      41 k
 liberation-fonts-common                                 noarch                     1:1.07.2-16.el7                              c7-remote                      27 k
 liberation-sans-fonts                                   noarch                     1:1.07.2-16.el7                              c7-remote                     279 k
 libevent                                                x86_64                     2.0.21-4.el7                                 c7-remote                     214 k
 libini_config                                           x86_64                     1.3.1-29.el7                                 c7-remote                      63 k
 libldb                                                  x86_64                     1.2.2-1.el7                                  c7-remote                     131 k
 libnfsidmap                                             x86_64                     0.25-19.el7                                  c7-remote                      50 k
 libpath_utils                                           x86_64                     0.2.1-29.el7                                 c7-remote                      28 k
 libqb                                                   x86_64                     1.0.1-6.el7                                  c7-remote                      95 k
 librados2                                               x86_64                     1:0.94.5-2.el7                               c7-remote                     1.7 M
 libref_array                                            x86_64                     0.1.5-29.el7                                 c7-remote                      26 k
 libsemanage-python                                      x86_64                     2.5-11.el7                                   c7-remote                     112 k
 libtalloc                                               x86_64                     2.1.10-1.el7                                 c7-remote                      33 k
 libtdb                                                  x86_64                     1.3.15-1.el7                                 c7-remote                      48 k
 libtevent                                               x86_64                     0.9.33-2.el7                                 c7-remote                      37 k
 libtirpc                                                x86_64                     0.2.4-0.10.el7                               c7-remote                      88 k
 libverto-libevent                                       x86_64                     0.2.5-4.el7                                  c7-remote                     8.9 k
 libwbclient                                             x86_64                     4.7.1-6.el7                                  c7-remote                     107 k
 libwsman1                                               x86_64                     2.6.3-3.git4391e5c.el7                       c7-remote                     139 k
 libxslt                                                 x86_64                     1.1.28-5.el7                                 c7-remote                     242 k
 libyaml                                                 x86_64                     0.1.4-11.el7_0                               c7-remote                      55 k
 lvm2                                                    x86_64                     7:2.02.177-4.el7                             c7-remote                     1.3 M
 lvm2-libs                                               x86_64                     7:2.02.177-4.el7                             c7-remote                     1.0 M
 net-snmp-libs                                           x86_64                     1:5.7.2-32.el7                               c7-remote                     748 k
 net-snmp-utils                                          x86_64                     1:5.7.2-32.el7                               c7-remote                     198 k
 net-tools                                               x86_64                     2.0-0.22.20131004git.el7                     c7-remote                     305 k
 nettle                                                  x86_64                     2.7.1-8.el7                                  c7-remote                     327 k
 nfs-utils                                               x86_64                     1:1.3.0-0.54.el7                             c7-remote                     407 k
 openwsman-python                                        x86_64                     2.6.3-3.git4391e5c.el7                       c7-remote                     109 k
 overpass-fonts                                          noarch                     2.1-1.el7                                    c7-remote                     700 k
 pacemaker-cli                                           x86_64                     1.1.18-11.el7                                c7-remote                     347 k
 pacemaker-cluster-libs                                  x86_64                     1.1.18-11.el7                                c7-remote                     151 k
 pacemaker-libs                                          x86_64                     1.1.18-11.el7                                c7-remote                     618 k
 perl                                                    x86_64                     4:5.16.3-292.el7                             c7-remote                     8.0 M
 perl-Carp                                               noarch                     1.26-244.el7                                 c7-remote                      19 k
 perl-Encode                                             x86_64                     2.51-7.el7                                   c7-remote                     1.5 M
 perl-Exporter                                           noarch                     5.68-3.el7                                   c7-remote                      28 k
 perl-File-Path                                          noarch                     2.09-2.el7                                   c7-remote                      26 k
 perl-File-Temp                                          noarch                     0.23.01-3.el7                                c7-remote                      56 k
 perl-Filter                                             x86_64                     1.49-3.el7                                   c7-remote                      76 k
 perl-Getopt-Long                                        noarch                     2.40-3.el7                                   c7-remote                      56 k
 perl-HTTP-Tiny                                          noarch                     0.033-3.el7                                  c7-remote                      38 k
 perl-PathTools                                          x86_64                     3.40-5.el7                                   c7-remote                      82 k
 perl-Pod-Escapes                                        noarch                     1:1.04-292.el7                               c7-remote                      51 k
 perl-Pod-Perldoc                                        noarch                     3.20-4.el7                                   c7-remote                      87 k
 perl-Pod-Simple                                         noarch                     1:3.28-4.el7                                 c7-remote                     216 k
 perl-Pod-Usage                                          noarch                     1.63-3.el7                                   c7-remote                      27 k
 perl-Scalar-List-Utils                                  x86_64                     1.27-248.el7                                 c7-remote                      36 k
 perl-Socket                                             x86_64                     2.010-4.el7                                  c7-remote                      49 k
 perl-Storable                                           x86_64                     2.45-3.el7                                   c7-remote                      77 k
 perl-Text-ParseWords                                    noarch                     3.29-4.el7                                   c7-remote                      14 k
 perl-Time-HiRes                                         x86_64                     4:1.9725-3.el7                               c7-remote                      45 k
 perl-Time-Local                                         noarch                     1.2300-2.el7                                 c7-remote                      24 k
 perl-TimeDate                                           noarch                     1:2.30-2.el7                                 c7-remote                      52 k
 perl-constant                                           noarch                     1.27-2.el7                                   c7-remote                      19 k
 perl-libs                                               x86_64                     4:5.16.3-292.el7                             c7-remote                     688 k
 perl-macros                                             x86_64                     4:5.16.3-292.el7                             c7-remote                      43 k
 perl-parent                                             noarch                     1:0.225-244.el7                              c7-remote                      12 k
 perl-podlators                                          noarch                     2.5.1-3.el7                                  c7-remote                     112 k
 perl-threads                                            x86_64                     1.87-4.el7                                   c7-remote                      49 k
 perl-threads-shared                                     x86_64                     1.43-6.el7                                   c7-remote                      39 k
 pexpect                                                 noarch                     2.3-11.el7                                   c7-remote                     142 k
 policycoreutils-python                                  x86_64                     2.5-22.el7                                   c7-remote                     454 k
 psmisc                                                  x86_64                     22.20-15.el7                                 c7-remote                     141 k
 python-IPy                                              noarch                     0.75-6.el7                                   c7-remote                      32 k
 python-backports                                        x86_64                     1.0-8.el7                                    c7-remote                     5.8 k
 python-backports-ssl_match_hostname                     noarch                     3.5.0.1-1.el7                                c7-remote                      13 k
 python-chardet                                          noarch                     2.2.1-1.el7_1                                c7-remote                     227 k
 python-clufter                                          noarch                     0.77.0-2.el7                                 c7-remote                     320 k
 python-ipaddress                                        noarch                     1.0.16-2.el7                                 c7-remote                      34 k
 python-lxml                                             x86_64                     3.2.1-4.el7                                  c7-remote                     758 k
 python-requests                                         noarch                     2.6.0-1.el7_1                                c7-remote                      94 k
 python-setuptools                                       noarch                     0.9.8-7.el7                                  c7-remote                     397 k
 python-six                                              noarch                     1.9.0-2.el7                                  c7-remote                      29 k
 python-suds                                             noarch                     0.4.1-5.el7                                  c7-remote                     204 k
 python-urllib3                                          noarch                     1.10.2-5.el7                                 c7-remote                     102 k
 quota                                                   x86_64                     1:4.01-17.el7                                c7-remote                     179 k
 quota-nls                                               noarch                     1:4.01-17.el7                                c7-remote                      90 k
 rpcbind                                                 x86_64                     0.2.0-44.el7                                 c7-remote                      59 k
 ruby                                                    x86_64                     2.0.0.648-33.el7_4                           c7-remote                      71 k
 ruby-irb                                                noarch                     2.0.0.648-33.el7_4                           c7-remote                      92 k
 ruby-libs                                               x86_64                     2.0.0.648-33.el7_4                           c7-remote                     2.8 M
 rubygem-bigdecimal                                      x86_64                     1.2.0-33.el7_4                               c7-remote                      83 k
 rubygem-io-console                                      x86_64                     0.4.2-33.el7_4                               c7-remote                      54 k
 rubygem-json                                            x86_64                     1.7.7-33.el7_4                               c7-remote                      79 k
 rubygem-psych                                           x86_64                     2.0.0-33.el7_4                               c7-remote                      82 k
 rubygem-rdoc                                            noarch                     4.0.0-33.el7_4                               c7-remote                     322 k
 rubygems                                                noarch                     2.0.14.1-33.el7_4                            c7-remote                     219 k
 samba-client-libs                                       x86_64                     4.7.1-6.el7                                  c7-remote                     4.8 M
 samba-common                                            noarch                     4.7.1-6.el7                                  c7-remote                     205 k
 samba-common-libs                                       x86_64                     4.7.1-6.el7                                  c7-remote                     162 k
 setools-libs                                            x86_64                     3.3.8-2.el7                                  c7-remote                     619 k
 tcp_wrappers                                            x86_64                     7.6-77.el7                                   c7-remote                      78 k
 trousers                                                x86_64                     0.3.14-2.el7                                 c7-remote                     289 k
 unbound-libs                                            x86_64                     1.6.6-1.el7                                  c7-remote                     405 k

Transaction Summary
=====================================================================================================================================================================
Install  4 Packages (+159 Dependent packages)

Total download size: 46 M
Installed size: 141 M
Downloading packages:
(1/163): OpenIPMI-modalias-2.0.23-2.el7.x86_64.rpm                                                                                            |  16 kB  00:00:00
(2/163): audit-libs-python-2.8.1-3.el7.x86_64.rpm                                                                                             |  75 kB  00:00:00
(3/163): autogen-libopts-5.18-5.el7.x86_64.rpm                                                                                                |  66 kB  00:00:00
(4/163): avahi-libs-0.6.31-19.el7.x86_64.rpm                                                                                                  |  61 kB  00:00:00
(5/163): bc-1.06.95-13.el7.x86_64.rpm                                                                                                         | 115 kB  00:00:00
(6/163): boost-system-1.53.0-27.el7.x86_64.rpm                                                                                                |  40 kB  00:00:00
(7/163): boost-thread-1.53.0-27.el7.x86_64.rpm                                                                                                |  57 kB  00:00:00
(8/163): cifs-utils-6.2-10.el7.x86_64.rpm                                                                                                     |  85 kB  00:00:00
(9/163): checkpolicy-2.5-6.el7.x86_64.rpm                                                                                                     | 294 kB  00:00:00
(10/163): clufter-bin-0.77.0-2.el7.x86_64.rpm                                                                                                 |  25 kB  00:00:00
(11/163): clufter-common-0.77.0-2.el7.noarch.rpm                                                                                              |  72 kB  00:00:00
(12/163): corosync-2.4.3-2.el7.x86_64.rpm                                                                                                     | 220 kB  00:00:00
(13/163): corosynclib-2.4.3-2.el7.x86_64.rpm                                                                                                  | 131 kB  00:00:00
(14/163): cups-libs-1.6.3-35.el7.x86_64.rpm                                                                                                   | 357 kB  00:00:00
(15/163): device-mapper-event-1.02.146-4.el7.x86_64.rpm                                                                                       | 185 kB  00:00:00
(16/163): device-mapper-event-libs-1.02.146-4.el7.x86_64.rpm                                                                                  | 184 kB  00:00:00
(17/163): device-mapper-multipath-0.4.9-119.el7.x86_64.rpm                                                                                    | 137 kB  00:00:00
(18/163): device-mapper-multipath-libs-0.4.9-119.el7.x86_64.rpm                                                                               | 257 kB  00:00:00
(19/163): device-mapper-persistent-data-0.7.3-3.el7.x86_64.rpm                                                                                | 405 kB  00:00:00
(20/163): fence-agents-all-4.0.11-86.el7.x86_64.rpm                                                                                           |  20 kB  00:00:00
(21/163): fence-agents-amt-ws-4.0.11-86.el7.x86_64.rpm                                                                                        |  24 kB  00:00:00
(22/163): fence-agents-apc-4.0.11-86.el7.x86_64.rpm                                                                                           |  23 kB  00:00:00
(23/163): fence-agents-apc-snmp-4.0.11-86.el7.x86_64.rpm                                                                                      |  23 kB  00:00:00
(24/163): fence-agents-bladecenter-4.0.11-86.el7.x86_64.rpm                                                                                   |  23 kB  00:00:00
(25/163): fence-agents-brocade-4.0.11-86.el7.x86_64.rpm                                                                                       |  23 kB  00:00:00
(26/163): fence-agents-cisco-mds-4.0.11-86.el7.x86_64.rpm                                                                                     |  23 kB  00:00:00
(27/163): fence-agents-cisco-ucs-4.0.11-86.el7.x86_64.rpm                                                                                     |  23 kB  00:00:00
(28/163): fence-agents-common-4.0.11-86.el7.x86_64.rpm                                                                                        |  63 kB  00:00:00
(29/163): fence-agents-compute-4.0.11-86.el7.x86_64.rpm                                                                                       |  29 kB  00:00:00
(30/163): fence-agents-drac5-4.0.11-86.el7.x86_64.rpm                                                                                         |  23 kB  00:00:00
(31/163): fence-agents-eaton-snmp-4.0.11-86.el7.x86_64.rpm                                                                                    |  24 kB  00:00:00
(32/163): fence-agents-emerson-4.0.11-86.el7.x86_64.rpm                                                                                       |  22 kB  00:00:00
(33/163): fence-agents-eps-4.0.11-86.el7.x86_64.rpm                                                                                           |  23 kB  00:00:00
(34/163): fence-agents-heuristics-ping-4.0.11-86.el7.x86_64.rpm                                                                               |  23 kB  00:00:00
(35/163): fence-agents-hpblade-4.0.11-86.el7.x86_64.rpm                                                                                       |  23 kB  00:00:00
(36/163): fence-agents-ibmblade-4.0.11-86.el7.x86_64.rpm                                                                                      |  22 kB  00:00:00
(37/163): fence-agents-ifmib-4.0.11-86.el7.x86_64.rpm                                                                                         |  23 kB  00:00:00
(38/163): fence-agents-ilo-moonshot-4.0.11-86.el7.x86_64.rpm                                                                                  |  22 kB  00:00:00
(39/163): fence-agents-ilo-mp-4.0.11-86.el7.x86_64.rpm                                                                                        |  22 kB  00:00:00
(40/163): fence-agents-ilo-ssh-4.0.11-86.el7.x86_64.rpm                                                                                       |  25 kB  00:00:00
(41/163): fence-agents-ilo2-4.0.11-86.el7.x86_64.rpm                                                                                          |  24 kB  00:00:00
(42/163): fence-agents-intelmodular-4.0.11-86.el7.x86_64.rpm                                                                                  |  23 kB  00:00:00
(43/163): fence-agents-ipdu-4.0.11-86.el7.x86_64.rpm                                                                                          |  23 kB  00:00:00
(44/163): fence-agents-ipmilan-4.0.11-86.el7.x86_64.rpm                                                                                       |  31 kB  00:00:00
(45/163): fence-agents-kdump-4.0.11-86.el7.x86_64.rpm                                                                                         |  33 kB  00:00:00
(46/163): fence-agents-mpath-4.0.11-86.el7.x86_64.rpm                                                                                         |  24 kB  00:00:00
(47/163): fence-agents-rhevm-4.0.11-86.el7.x86_64.rpm                                                                                         |  23 kB  00:00:00
(48/163): fence-agents-rsa-4.0.11-86.el7.x86_64.rpm                                                                                           |  22 kB  00:00:00
(49/163): fence-agents-rsb-4.0.11-86.el7.x86_64.rpm                                                                                           |  22 kB  00:00:00
(50/163): fence-agents-sbd-4.0.11-86.el7.x86_64.rpm                                                                                           |  24 kB  00:00:00
(51/163): fence-agents-scsi-4.0.11-86.el7.x86_64.rpm                                                                                          |  26 kB  00:00:00
(52/163): fence-agents-vmware-rest-4.0.11-86.el7.x86_64.rpm                                                                                   |  23 kB  00:00:00
(53/163): fence-agents-vmware-soap-4.0.11-86.el7.x86_64.rpm                                                                                   |  24 kB  00:00:00
(54/163): fence-agents-wti-4.0.11-86.el7.x86_64.rpm                                                                                           |  24 kB  00:00:00
(55/163): fence-virt-0.3.2-13.el7.x86_64.rpm                                                                                                  |  41 kB  00:00:00
(56/163): fontpackages-filesystem-1.44-8.el7.noarch.rpm                                                                                       | 9.9 kB  00:00:00
(57/163): gnutls-dane-3.3.26-9.el7.x86_64.rpm                                                                                                 |  34 kB  00:00:00
(58/163): gnutls-3.3.26-9.el7.x86_64.rpm                                                                                                      | 677 kB  00:00:00
(59/163): gnutls-utils-3.3.26-9.el7.x86_64.rpm                                                                                                | 237 kB  00:00:00
(60/163): gssproxy-0.7.0-17.el7.x86_64.rpm                                                                                                    | 108 kB  00:00:00
(61/163): keyutils-1.5.8-3.el7.x86_64.rpm                                                                                                     |  54 kB  00:00:00
(62/163): ipmitool-1.8.18-7.el7.x86_64.rpm                                                                                                    | 441 kB  00:00:00
(63/163): libaio-0.3.109-13.el7.x86_64.rpm                                                                                                    |  24 kB  00:00:00
(64/163): libbasicobjects-0.1.1-29.el7.x86_64.rpm                                                                                             |  25 kB  00:00:00
(65/163): libcgroup-0.41-15.el7.x86_64.rpm                                                                                                    |  65 kB  00:00:00
(66/163): libcollection-0.7.0-29.el7.x86_64.rpm                                                                                               |  41 kB  00:00:00
(67/163): liberation-fonts-common-1.07.2-16.el7.noarch.rpm                                                                                    |  27 kB  00:00:00
(68/163): liberation-sans-fonts-1.07.2-16.el7.noarch.rpm                                                                                      | 279 kB  00:00:00
(69/163): libevent-2.0.21-4.el7.x86_64.rpm                                                                                                    | 214 kB  00:00:00
(70/163): libini_config-1.3.1-29.el7.x86_64.rpm                                                                                               |  63 kB  00:00:00
(71/163): libnfsidmap-0.25-19.el7.x86_64.rpm                                                                                                  |  50 kB  00:00:00
(72/163): libpath_utils-0.2.1-29.el7.x86_64.rpm                                                                                               |  28 kB  00:00:00
(73/163): libqb-1.0.1-6.el7.x86_64.rpm                                                                                                        |  95 kB  00:00:00
(74/163): librados2-0.94.5-2.el7.x86_64.rpm                                                                                                   | 1.7 MB  00:00:00
(75/163): libref_array-0.1.5-29.el7.x86_64.rpm                                                                                                |  26 kB  00:00:00
(76/163): libsemanage-python-2.5-11.el7.x86_64.rpm                                                                                            | 112 kB  00:00:00
(77/163): libtalloc-2.1.10-1.el7.x86_64.rpm                                                                                                   |  33 kB  00:00:00
(78/163): libtdb-1.3.15-1.el7.x86_64.rpm                                                                                                      |  48 kB  00:00:00
(79/163): libtevent-0.9.33-2.el7.x86_64.rpm                                                                                                   |  37 kB  00:00:00
(80/163): libtirpc-0.2.4-0.10.el7.x86_64.rpm                                                                                                  |  88 kB  00:00:00
(81/163): libldb-1.2.2-1.el7.x86_64.rpm                                                                                                       | 131 kB  00:00:00
(82/163): libverto-libevent-0.2.5-4.el7.x86_64.rpm                                                                                            | 8.9 kB  00:00:00
(83/163): libwbclient-4.7.1-6.el7.x86_64.rpm                                                                                                  | 107 kB  00:00:00
(84/163): libwsman1-2.6.3-3.git4391e5c.el7.x86_64.rpm                                                                                         | 139 kB  00:00:00
(85/163): libxslt-1.1.28-5.el7.x86_64.rpm                                                                                                     | 242 kB  00:00:00
(86/163): libyaml-0.1.4-11.el7_0.x86_64.rpm                                                                                                   |  55 kB  00:00:00
(87/163): lvm2-libs-2.02.177-4.el7.x86_64.rpm                                                                                                 | 1.0 MB  00:00:00
(88/163): lvm2-2.02.177-4.el7.x86_64.rpm                                                                                                      | 1.3 MB  00:00:00
(89/163): net-snmp-libs-5.7.2-32.el7.x86_64.rpm                                                                                               | 748 kB  00:00:00
(90/163): net-snmp-utils-5.7.2-32.el7.x86_64.rpm                                                                                              | 198 kB  00:00:00
(91/163): net-tools-2.0-0.22.20131004git.el7.x86_64.rpm                                                                                       | 305 kB  00:00:00
(92/163): nettle-2.7.1-8.el7.x86_64.rpm                                                                                                       | 327 kB  00:00:00
(93/163): nfs-utils-1.3.0-0.54.el7.x86_64.rpm                                                                                                 | 407 kB  00:00:00
(94/163): openwsman-python-2.6.3-3.git4391e5c.el7.x86_64.rpm                                                                                  | 109 kB  00:00:00
(95/163): overpass-fonts-2.1-1.el7.noarch.rpm                                                                                                 | 700 kB  00:00:00
(96/163): pacemaker-1.1.18-11.el7.x86_64.rpm                                                                                                  | 455 kB  00:00:00
(97/163): pacemaker-cli-1.1.18-11.el7.x86_64.rpm                                                                                              | 347 kB  00:00:00
(98/163): pacemaker-cluster-libs-1.1.18-11.el7.x86_64.rpm                                                                                     | 151 kB  00:00:00
(99/163): pacemaker-libs-1.1.18-11.el7.x86_64.rpm                                                                                             | 618 kB  00:00:00
(100/163): pcs-0.9.162-5.el7.centos.x86_64.rpm                                                                                                | 5.0 MB  00:00:00
(101/163): perl-5.16.3-292.el7.x86_64.rpm                                                                                                     | 8.0 MB  00:00:00
(102/163): perl-Carp-1.26-244.el7.noarch.rpm                                                                                                  |  19 kB  00:00:00
(103/163): perl-Exporter-5.68-3.el7.noarch.rpm                                                                                                |  28 kB  00:00:00
(104/163): perl-Encode-2.51-7.el7.x86_64.rpm                                                                                                  | 1.5 MB  00:00:00
(105/163): perl-File-Path-2.09-2.el7.noarch.rpm                                                                                               |  26 kB  00:00:00
(106/163): perl-File-Temp-0.23.01-3.el7.noarch.rpm                                                                                            |  56 kB  00:00:00
(107/163): perl-Filter-1.49-3.el7.x86_64.rpm                                                                                                  |  76 kB  00:00:00
(108/163): perl-Getopt-Long-2.40-3.el7.noarch.rpm                                                                                             |  56 kB  00:00:00
(109/163): perl-HTTP-Tiny-0.033-3.el7.noarch.rpm                                                                                              |  38 kB  00:00:00
(110/163): perl-PathTools-3.40-5.el7.x86_64.rpm                                                                                               |  82 kB  00:00:00
(111/163): perl-Pod-Escapes-1.04-292.el7.noarch.rpm                                                                                           |  51 kB  00:00:00
(112/163): perl-Pod-Perldoc-3.20-4.el7.noarch.rpm                                                                                             |  87 kB  00:00:00
(113/163): perl-Pod-Simple-3.28-4.el7.noarch.rpm                                                                                              | 216 kB  00:00:00
(114/163): perl-Pod-Usage-1.63-3.el7.noarch.rpm                                                                                               |  27 kB  00:00:00
(115/163): perl-Scalar-List-Utils-1.27-248.el7.x86_64.rpm                                                                                     |  36 kB  00:00:00
(116/163): perl-Socket-2.010-4.el7.x86_64.rpm                                                                                                 |  49 kB  00:00:00
(117/163): perl-Storable-2.45-3.el7.x86_64.rpm                                                                                                |  77 kB  00:00:00
(118/163): perl-Text-ParseWords-3.29-4.el7.noarch.rpm                                                                                         |  14 kB  00:00:00
(119/163): perl-Time-HiRes-1.9725-3.el7.x86_64.rpm                                                                                            |  45 kB  00:00:00
(120/163): perl-Time-Local-1.2300-2.el7.noarch.rpm                                                                                            |  24 kB  00:00:00
(121/163): perl-TimeDate-2.30-2.el7.noarch.rpm                                                                                                |  52 kB  00:00:00
(122/163): perl-constant-1.27-2.el7.noarch.rpm                                                                                                |  19 kB  00:00:00
(123/163): perl-macros-5.16.3-292.el7.x86_64.rpm                                                                                              |  43 kB  00:00:00
(124/163): perl-libs-5.16.3-292.el7.x86_64.rpm                                                                                                | 688 kB  00:00:00
(125/163): perl-parent-0.225-244.el7.noarch.rpm                                                                                               |  12 kB  00:00:00
(126/163): perl-podlators-2.5.1-3.el7.noarch.rpm                                                                                              | 112 kB  00:00:00
(127/163): perl-threads-1.87-4.el7.x86_64.rpm                                                                                                 |  49 kB  00:00:00
(128/163): perl-threads-shared-1.43-6.el7.x86_64.rpm                                                                                          |  39 kB  00:00:00
(129/163): pexpect-2.3-11.el7.noarch.rpm                                                                                                      | 142 kB  00:00:00
(130/163): policycoreutils-python-2.5-22.el7.x86_64.rpm                                                                                       | 454 kB  00:00:00
(131/163): psmisc-22.20-15.el7.x86_64.rpm                                                                                                     | 141 kB  00:00:00
(132/163): python-IPy-0.75-6.el7.noarch.rpm                                                                                                   |  32 kB  00:00:00
(133/163): python-backports-1.0-8.el7.x86_64.rpm                                                                                              | 5.8 kB  00:00:00
(134/163): python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch.rpm                                                                       |  13 kB  00:00:00
(135/163): python-chardet-2.2.1-1.el7_1.noarch.rpm                                                                                            | 227 kB  00:00:00
(136/163): python-clufter-0.77.0-2.el7.noarch.rpm                                                                                             | 320 kB  00:00:00
(137/163): python-ipaddress-1.0.16-2.el7.noarch.rpm                                                                                           |  34 kB  00:00:00
(138/163): python-requests-2.6.0-1.el7_1.noarch.rpm                                                                                           |  94 kB  00:00:00
(139/163): python-lxml-3.2.1-4.el7.x86_64.rpm                                                                                                 | 758 kB  00:00:00
(140/163): python-setuptools-0.9.8-7.el7.noarch.rpm                                                                                           | 397 kB  00:00:00
(141/163): python-suds-0.4.1-5.el7.noarch.rpm                                                                                                 | 204 kB  00:00:00
(142/163): python-urllib3-1.10.2-5.el7.noarch.rpm                                                                                             | 102 kB  00:00:00
(143/163): quota-4.01-17.el7.x86_64.rpm                                                                                                       | 179 kB  00:00:00
(144/163): quota-nls-4.01-17.el7.noarch.rpm                                                                                                   |  90 kB  00:00:00
(145/163): resource-agents-3.9.5-124.el7.x86_64.rpm                                                                                           | 398 kB  00:00:00
(146/163): rpcbind-0.2.0-44.el7.x86_64.rpm                                                                                                    |  59 kB  00:00:00
(147/163): ruby-2.0.0.648-33.el7_4.x86_64.rpm                                                                                                 |  71 kB  00:00:00
(148/163): ruby-irb-2.0.0.648-33.el7_4.noarch.rpm                                                                                             |  92 kB  00:00:00
(149/163): ruby-libs-2.0.0.648-33.el7_4.x86_64.rpm                                                                                            | 2.8 MB  00:00:00
(150/163): python-six-1.9.0-2.el7.noarch.rpm                                                                                                  |  29 kB  00:00:00
(151/163): rubygem-bigdecimal-1.2.0-33.el7_4.x86_64.rpm                                                                                       |  83 kB  00:00:00
(152/163): rubygem-io-console-0.4.2-33.el7_4.x86_64.rpm                                                                                       |  54 kB  00:00:00
(153/163): rubygem-json-1.7.7-33.el7_4.x86_64.rpm                                                                                             |  79 kB  00:00:00
(154/163): rubygem-psych-2.0.0-33.el7_4.x86_64.rpm                                                                                            |  82 kB  00:00:00
(155/163): rubygem-rdoc-4.0.0-33.el7_4.noarch.rpm                                                                                             | 322 kB  00:00:00
(156/163): rubygems-2.0.14.1-33.el7_4.noarch.rpm                                                                                              | 219 kB  00:00:00
(157/163): samba-common-4.7.1-6.el7.noarch.rpm                                                                                                | 205 kB  00:00:00
(158/163): samba-common-libs-4.7.1-6.el7.x86_64.rpm                                                                                           | 162 kB  00:00:00
(159/163): setools-libs-3.3.8-2.el7.x86_64.rpm                                                                                                | 619 kB  00:00:00
(160/163): samba-client-libs-4.7.1-6.el7.x86_64.rpm                                                                                           | 4.8 MB  00:00:00
(161/163): tcp_wrappers-7.6-77.el7.x86_64.rpm                                                                                                 |  78 kB  00:00:00
(162/163): trousers-0.3.14-2.el7.x86_64.rpm                                                                                                   | 289 kB  00:00:00
(163/163): unbound-libs-1.6.6-1.el7.x86_64.rpm                                                                                                | 405 kB  00:00:00
---------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                 51 MB/s |  46 MB  00:00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Warning: RPMDB altered outside of yum.
  Installing : 1:perl-parent-0.225-244.el7.noarch                                                                                                              1/163
  Installing : perl-HTTP-Tiny-0.033-3.el7.noarch                                                                                                               2/163
  Installing : perl-podlators-2.5.1-3.el7.noarch                                                                                                               3/163
  Installing : perl-Pod-Perldoc-3.20-4.el7.noarch                                                                                                              4/163
  Installing : perl-Text-ParseWords-3.29-4.el7.noarch                                                                                                          5/163
  Installing : 1:perl-Pod-Escapes-1.04-292.el7.noarch                                                                                                          6/163
  Installing : perl-Encode-2.51-7.el7.x86_64                                                                                                                   7/163
  Installing : perl-Pod-Usage-1.63-3.el7.noarch                                                                                                                8/163
  Installing : 4:perl-libs-5.16.3-292.el7.x86_64                                                                                                               9/163
  Installing : 4:perl-macros-5.16.3-292.el7.x86_64                                                                                                            10/163
  Installing : perl-threads-1.87-4.el7.x86_64                                                                                                                 11/163
  Installing : perl-Socket-2.010-4.el7.x86_64                                                                                                                 12/163
  Installing : perl-Filter-1.49-3.el7.x86_64                                                                                                                  13/163
  Installing : perl-Storable-2.45-3.el7.x86_64                                                                                                                14/163
  Installing : 4:perl-Time-HiRes-1.9725-3.el7.x86_64                                                                                                          15/163
  Installing : perl-Exporter-5.68-3.el7.noarch                                                                                                                16/163
  Installing : perl-Carp-1.26-244.el7.noarch                                                                                                                  17/163
  Installing : perl-threads-shared-1.43-6.el7.x86_64                                                                                                          18/163
  Installing : perl-File-Path-2.09-2.el7.noarch                                                                                                               19/163
  Installing : perl-PathTools-3.40-5.el7.x86_64                                                                                                               20/163
  Installing : perl-Scalar-List-Utils-1.27-248.el7.x86_64                                                                                                     21/163
  Installing : perl-File-Temp-0.23.01-3.el7.noarch                                                                                                            22/163
  Installing : 1:perl-Pod-Simple-3.28-4.el7.noarch                                                                                                            23/163
  Installing : perl-Getopt-Long-2.40-3.el7.noarch                                                                                                             24/163
  Installing : perl-Time-Local-1.2300-2.el7.noarch                                                                                                            25/163
  Installing : perl-constant-1.27-2.el7.noarch                                                                                                                26/163
  Installing : 4:perl-5.16.3-292.el7.x86_64                                                                                                                   27/163
  Installing : ruby-libs-2.0.0.648-33.el7_4.x86_64                                                                                                            28/163
  Installing : libxslt-1.1.28-5.el7.x86_64                                                                                                                    29/163
  Installing : libqb-1.0.1-6.el7.x86_64                                                                                                                       30/163
  Installing : libtalloc-2.1.10-1.el7.x86_64                                                                                                                  31/163
  Installing : 7:device-mapper-event-libs-1.02.146-4.el7.x86_64                                                                                               32/163
  Installing : libtdb-1.3.15-1.el7.x86_64                                                                                                                     33/163
  Installing : libevent-2.0.21-4.el7.x86_64                                                                                                                   34/163
  Installing : nettle-2.7.1-8.el7.x86_64                                                                                                                      35/163
  Installing : unbound-libs-1.6.6-1.el7.x86_64                                                                                                                36/163
  Installing : libtevent-0.9.33-2.el7.x86_64                                                                                                                  37/163
  Installing : python-lxml-3.2.1-4.el7.x86_64                                                                                                                 38/163
  Installing : libtirpc-0.2.4-0.10.el7.x86_64                                                                                                                 39/163
  Installing : rpcbind-0.2.0-44.el7.x86_64                                                                                                                    40/163
  Installing : libcgroup-0.41-15.el7.x86_64                                                                                                                   41/163
  Installing : libaio-0.3.109-13.el7.x86_64                                                                                                                   42/163
  Installing : avahi-libs-0.6.31-19.el7.x86_64                                                                                                                43/163
  Installing : fontpackages-filesystem-1.44-8.el7.noarch                                                                                                      44/163
  Installing : samba-common-4.7.1-6.el7.noarch                                                                                                                45/163
  Installing : keyutils-1.5.8-3.el7.x86_64                                                                                                                    46/163
  Installing : psmisc-22.20-15.el7.x86_64                                                                                                                     47/163
  Installing : 1:net-snmp-libs-5.7.2-32.el7.x86_64                                                                                                            48/163
  Installing : 1:net-snmp-utils-5.7.2-32.el7.x86_64                                                                                                           49/163
  Installing : corosynclib-2.4.3-2.el7.x86_64                                                                                                                 50/163
  Installing : corosync-2.4.3-2.el7.x86_64                                                                                                                    51/163
  Installing : libcollection-0.7.0-29.el7.x86_64                                                                                                              52/163
  Installing : boost-system-1.53.0-27.el7.x86_64                                                                                                              53/163
  Installing : python-ipaddress-1.0.16-2.el7.noarch                                                                                                           54/163
  Installing : libref_array-0.1.5-29.el7.x86_64                                                                                                               55/163
  Installing : libbasicobjects-0.1.1-29.el7.x86_64                                                                                                            56/163
  Installing : boost-thread-1.53.0-27.el7.x86_64                                                                                                              57/163
  Installing : 1:librados2-0.94.5-2.el7.x86_64                                                                                                                58/163
  Installing : device-mapper-multipath-libs-0.4.9-119.el7.x86_64                                                                                              59/163
  Installing : device-mapper-multipath-0.4.9-119.el7.x86_64                                                                                                   60/163
  Installing : overpass-fonts-2.1-1.el7.noarch                                                                                                                61/163
  Installing : 1:liberation-fonts-common-1.07.2-16.el7.noarch                                                                                                 62/163
  Installing : 1:liberation-sans-fonts-1.07.2-16.el7.noarch                                                                                                   63/163
  Installing : 1:cups-libs-1.6.3-35.el7.x86_64                                                                                                                64/163
  Installing : device-mapper-persistent-data-0.7.3-3.el7.x86_64                                                                                               65/163
  Installing : libldb-1.2.2-1.el7.x86_64                                                                                                                      66/163
  Installing : libwbclient-4.7.1-6.el7.x86_64                                                                                                                 67/163
  Installing : samba-client-libs-4.7.1-6.el7.x86_64                                                                                                           68/163
  Installing : samba-common-libs-4.7.1-6.el7.x86_64                                                                                                           69/163
  Installing : cifs-utils-6.2-10.el7.x86_64                                                                                                                   70/163
  Installing : libverto-libevent-0.2.5-4.el7.x86_64                                                                                                           71/163
  Installing : 7:device-mapper-event-1.02.146-4.el7.x86_64                                                                                                    72/163
  Installing : 7:lvm2-libs-2.02.177-4.el7.x86_64                                                                                                              73/163
  Installing : 7:lvm2-2.02.177-4.el7.x86_64                                                                                                                   74/163
  Installing : 1:perl-TimeDate-2.30-2.el7.noarch                                                                                                              75/163
  Installing : python-chardet-2.2.1-1.el7_1.noarch                                                                                                            76/163
  Installing : 1:quota-nls-4.01-17.el7.noarch                                                                                                                 77/163
  Installing : python-six-1.9.0-2.el7.noarch                                                                                                                  78/163
  Installing : libwsman1-2.6.3-3.git4391e5c.el7.x86_64                                                                                                        79/163
  Installing : openwsman-python-2.6.3-3.git4391e5c.el7.x86_64                                                                                                 80/163
  Installing : pexpect-2.3-11.el7.noarch                                                                                                                      81/163
  Installing : tcp_wrappers-7.6-77.el7.x86_64                                                                                                                 82/163
  Installing : 1:quota-4.01-17.el7.x86_64                                                                                                                     83/163
  Installing : libyaml-0.1.4-11.el7_0.x86_64                                                                                                                  84/163
  Installing : rubygem-json-1.7.7-33.el7_4.x86_64                                                                                                             85/163
  Installing : rubygem-bigdecimal-1.2.0-33.el7_4.x86_64                                                                                                       86/163
  Installing : rubygem-io-console-0.4.2-33.el7_4.x86_64                                                                                                       87/163
  Installing : ruby-irb-2.0.0.648-33.el7_4.noarch                                                                                                             88/163
  Installing : rubygem-rdoc-4.0.0-33.el7_4.noarch                                                                                                             89/163
  Installing : ruby-2.0.0.648-33.el7_4.x86_64                                                                                                                 90/163
  Installing : rubygems-2.0.14.1-33.el7_4.noarch                                                                                                              91/163
  Installing : rubygem-psych-2.0.0-33.el7_4.x86_64                                                                                                            92/163
  Installing : audit-libs-python-2.8.1-3.el7.x86_64                                                                                                           93/163
  Installing : autogen-libopts-5.18-5.el7.x86_64                                                                                                              94/163
  Installing : fence-virt-0.3.2-13.el7.x86_64                                                                                                                 95/163
  Installing : bc-1.06.95-13.el7.x86_64                                                                                                                       96/163
  Installing : setools-libs-3.3.8-2.el7.x86_64                                                                                                                97/163
  Installing : clufter-common-0.77.0-2.el7.noarch                                                                                                             98/163
  Installing : clufter-bin-0.77.0-2.el7.x86_64                                                                                                                99/163
  Installing : python-clufter-0.77.0-2.el7.noarch                                                                                                            100/163
  Installing : checkpolicy-2.5-6.el7.x86_64                                                                                                                  101/163
  Installing : libnfsidmap-0.25-19.el7.x86_64                                                                                                                102/163
  Installing : libpath_utils-0.2.1-29.el7.x86_64                                                                                                             103/163
  Installing : libini_config-1.3.1-29.el7.x86_64                                                                                                             104/163
  Installing : gssproxy-0.7.0-17.el7.x86_64                                                                                                                  105/163
  Installing : 1:nfs-utils-1.3.0-0.54.el7.x86_64                                                                                                             106/163
  Installing : python-IPy-0.75-6.el7.noarch                                                                                                                  107/163
  Installing : net-tools-2.0-0.22.20131004git.el7.x86_64                                                                                                     108/163
  Installing : resource-agents-3.9.5-124.el7.x86_64                                                                                                          109/163
  Installing : trousers-0.3.14-2.el7.x86_64                                                                                                                  110/163
  Installing : gnutls-3.3.26-9.el7.x86_64                                                                                                                    111/163
  Installing : pacemaker-libs-1.1.18-11.el7.x86_64                                                                                                           112/163
  Installing : pacemaker-cli-1.1.18-11.el7.x86_64                                                                                                            113/163
  Installing : pacemaker-cluster-libs-1.1.18-11.el7.x86_64                                                                                                   114/163
  Installing : pacemaker-1.1.18-11.el7.x86_64                                                                                                                115/163
  Installing : gnutls-dane-3.3.26-9.el7.x86_64                                                                                                               116/163
  Installing : gnutls-utils-3.3.26-9.el7.x86_64                                                                                                              117/163
  Installing : python-backports-1.0-8.el7.x86_64                                                                                                             118/163
  Installing : python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch                                                                                      119/163
  Installing : python-setuptools-0.9.8-7.el7.noarch                                                                                                          120/163
  Installing : python-urllib3-1.10.2-5.el7.noarch                                                                                                            121/163
  Installing : python-requests-2.6.0-1.el7_1.noarch                                                                                                          122/163
  Installing : python-suds-0.4.1-5.el7.noarch                                                                                                                123/163
  Installing : OpenIPMI-modalias-2.0.23-2.el7.x86_64                                                                                                         124/163
  Installing : ipmitool-1.8.18-7.el7.x86_64                                                                                                                  125/163
  Installing : libsemanage-python-2.5-11.el7.x86_64                                                                                                          126/163
  Installing : policycoreutils-python-2.5-22.el7.x86_64                                                                                                      127/163
  Installing : fence-agents-common-4.0.11-86.el7.x86_64                                                                                                      128/163
  Installing : fence-agents-heuristics-ping-4.0.11-86.el7.x86_64                                                                                             129/163
  Installing : fence-agents-ipdu-4.0.11-86.el7.x86_64                                                                                                        130/163
  Installing : fence-agents-ilo2-4.0.11-86.el7.x86_64                                                                                                        131/163
  Installing : fence-agents-hpblade-4.0.11-86.el7.x86_64                                                                                                     132/163
  Installing : fence-agents-cisco-ucs-4.0.11-86.el7.x86_64                                                                                                   133/163
  Installing : fence-agents-rsa-4.0.11-86.el7.x86_64                                                                                                         134/163
  Installing : fence-agents-mpath-4.0.11-86.el7.x86_64                                                                                                       135/163
  Installing : fence-agents-ipmilan-4.0.11-86.el7.x86_64                                                                                                     136/163
  Installing : fence-agents-bladecenter-4.0.11-86.el7.x86_64                                                                                                 137/163
  Installing : fence-agents-ifmib-4.0.11-86.el7.x86_64                                                                                                       138/163
  Installing : fence-agents-apc-snmp-4.0.11-86.el7.x86_64                                                                                                    139/163
  Installing : fence-agents-intelmodular-4.0.11-86.el7.x86_64                                                                                                140/163
  Installing : fence-agents-drac5-4.0.11-86.el7.x86_64                                                                                                       141/163
  Installing : fence-agents-apc-4.0.11-86.el7.x86_64                                                                                                         142/163
  Installing : fence-agents-wti-4.0.11-86.el7.x86_64                                                                                                         143/163
  Installing : fence-agents-rsb-4.0.11-86.el7.x86_64                                                                                                         144/163
  Installing : fence-agents-vmware-soap-4.0.11-86.el7.x86_64                                                                                                 145/163
  Installing : fence-agents-ilo-moonshot-4.0.11-86.el7.x86_64                                                                                                146/163
  Installing : fence-agents-emerson-4.0.11-86.el7.x86_64                                                                                                     147/163
  Installing : fence-agents-vmware-rest-4.0.11-86.el7.x86_64                                                                                                 148/163
  Installing : fence-agents-ilo-ssh-4.0.11-86.el7.x86_64                                                                                                     149/163
  Installing : fence-agents-scsi-4.0.11-86.el7.x86_64                                                                                                        150/163
  Installing : fence-agents-cisco-mds-4.0.11-86.el7.x86_64                                                                                                   151/163
  Installing : fence-agents-amt-ws-4.0.11-86.el7.x86_64                                                                                                      152/163
  Installing : fence-agents-eps-4.0.11-86.el7.x86_64                                                                                                         153/163
  Installing : fence-agents-brocade-4.0.11-86.el7.x86_64                                                                                                     154/163
  Installing : fence-agents-kdump-4.0.11-86.el7.x86_64                                                                                                       155/163
  Installing : fence-agents-rhevm-4.0.11-86.el7.x86_64                                                                                                       156/163
  Installing : fence-agents-compute-4.0.11-86.el7.x86_64                                                                                                     157/163
  Installing : fence-agents-ilo-mp-4.0.11-86.el7.x86_64                                                                                                      158/163
  Installing : fence-agents-ibmblade-4.0.11-86.el7.x86_64                                                                                                    159/163
  Installing : fence-agents-sbd-4.0.11-86.el7.x86_64                                                                                                         160/163
  Installing : fence-agents-eaton-snmp-4.0.11-86.el7.x86_64                                                                                                  161/163
  Installing : fence-agents-all-4.0.11-86.el7.x86_64                                                                                                         162/163
  Installing : pcs-0.9.162-5.el7.centos.x86_64                                                                                                               163/163
sed: can\'t read /etc/sysconfig/ipmi: No such file or directory
  Verifying  : fence-agents-heuristics-ping-4.0.11-86.el7.x86_64                                                                                               1/163
  Verifying  : fence-agents-ipdu-4.0.11-86.el7.x86_64                                                                                                          2/163
  Verifying  : libsemanage-python-2.5-11.el7.x86_64                                                                                                            3/163
  Verifying  : ruby-libs-2.0.0.648-33.el7_4.x86_64                                                                                                             4/163
  Verifying  : pcs-0.9.162-5.el7.centos.x86_64                                                                                                                 5/163
  Verifying  : python-lxml-3.2.1-4.el7.x86_64                                                                                                                  6/163
  Verifying  : libbasicobjects-0.1.1-29.el7.x86_64                                                                                                             7/163
  Verifying  : nettle-2.7.1-8.el7.x86_64                                                                                                                       8/163
  Verifying  : libref_array-0.1.5-29.el7.x86_64                                                                                                                9/163
  Verifying  : OpenIPMI-modalias-2.0.23-2.el7.x86_64                                                                                                          10/163
  Verifying  : 4:perl-5.16.3-292.el7.x86_64                                                                                                                   11/163
  Verifying  : python-suds-0.4.1-5.el7.noarch                                                                                                                 12/163
  Verifying  : policycoreutils-python-2.5-22.el7.x86_64                                                                                                       13/163
  Verifying  : perl-File-Temp-0.23.01-3.el7.noarch                                                                                                            14/163
  Verifying  : boost-thread-1.53.0-27.el7.x86_64                                                                                                              15/163
  Verifying  : fence-agents-ilo2-4.0.11-86.el7.x86_64                                                                                                         16/163
  Verifying  : 1:liberation-sans-fonts-1.07.2-16.el7.noarch                                                                                                   17/163
  Verifying  : perl-Socket-2.010-4.el7.x86_64                                                                                                                 18/163
  Verifying  : perl-Text-ParseWords-3.29-4.el7.noarch                                                                                                         19/163
  Verifying  : python-backports-1.0-8.el7.x86_64                                                                                                              20/163
  Verifying  : unbound-libs-1.6.6-1.el7.x86_64                                                                                                                21/163
  Verifying  : cifs-utils-6.2-10.el7.x86_64                                                                                                                   22/163
  Verifying  : 1:net-snmp-utils-5.7.2-32.el7.x86_64                                                                                                           23/163
  Verifying  : 1:perl-Pod-Escapes-1.04-292.el7.noarch                                                                                                         24/163
  Verifying  : pacemaker-libs-1.1.18-11.el7.x86_64                                                                                                            25/163
  Verifying  : fence-agents-hpblade-4.0.11-86.el7.x86_64                                                                                                      26/163
  Verifying  : rpcbind-0.2.0-44.el7.x86_64                                                                                                                    27/163
  Verifying  : ruby-irb-2.0.0.648-33.el7_4.noarch                                                                                                             28/163
  Verifying  : python-ipaddress-1.0.16-2.el7.noarch                                                                                                           29/163
  Verifying  : 1:librados2-0.94.5-2.el7.x86_64                                                                                                                30/163
  Verifying  : perl-File-Path-2.09-2.el7.noarch                                                                                                               31/163
  Verifying  : fence-agents-cisco-ucs-4.0.11-86.el7.x86_64                                                                                                    32/163
  Verifying  : fence-agents-rsa-4.0.11-86.el7.x86_64                                                                                                          33/163
  Verifying  : fence-agents-mpath-4.0.11-86.el7.x86_64                                                                                                        34/163
  Verifying  : perl-HTTP-Tiny-0.033-3.el7.noarch                                                                                                              35/163
  Verifying  : trousers-0.3.14-2.el7.x86_64                                                                                                                   36/163
  Verifying  : boost-system-1.53.0-27.el7.x86_64                                                                                                              37/163
  Verifying  : fence-agents-ipmilan-4.0.11-86.el7.x86_64                                                                                                      38/163
  Verifying  : 7:device-mapper-event-1.02.146-4.el7.x86_64                                                                                                    39/163
  Verifying  : net-tools-2.0-0.22.20131004git.el7.x86_64                                                                                                      40/163
  Verifying  : fence-agents-bladecenter-4.0.11-86.el7.x86_64                                                                                                  41/163
  Verifying  : libcollection-0.7.0-29.el7.x86_64                                                                                                              42/163
  Verifying  : rubygem-rdoc-4.0.0-33.el7_4.noarch                                                                                                             43/163
  Verifying  : libqb-1.0.1-6.el7.x86_64                                                                                                                       44/163
  Verifying  : python-setuptools-0.9.8-7.el7.noarch                                                                                                           45/163
  Verifying  : fence-agents-ifmib-4.0.11-86.el7.x86_64                                                                                                        46/163
  Verifying  : fence-agents-apc-snmp-4.0.11-86.el7.x86_64                                                                                                     47/163
  Verifying  : fence-agents-intelmodular-4.0.11-86.el7.x86_64                                                                                                 48/163
  Verifying  : overpass-fonts-2.1-1.el7.noarch                                                                                                                49/163
  Verifying  : perl-Filter-1.49-3.el7.x86_64                                                                                                                  50/163
  Verifying  : python-IPy-0.75-6.el7.noarch                                                                                                                   51/163
  Verifying  : 1:net-snmp-libs-5.7.2-32.el7.x86_64                                                                                                            52/163
  Verifying  : samba-common-libs-4.7.1-6.el7.x86_64                                                                                                           53/163
  Verifying  : 4:perl-libs-5.16.3-292.el7.x86_64                                                                                                              54/163
  Verifying  : 1:nfs-utils-1.3.0-0.54.el7.x86_64                                                                                                              55/163
  Verifying  : psmisc-22.20-15.el7.x86_64                                                                                                                     56/163
  Verifying  : gnutls-dane-3.3.26-9.el7.x86_64                                                                                                                57/163
  Verifying  : python-urllib3-1.10.2-5.el7.noarch                                                                                                             58/163
  Verifying  : fence-agents-drac5-4.0.11-86.el7.x86_64                                                                                                        59/163
  Verifying  : fence-agents-apc-4.0.11-86.el7.x86_64                                                                                                          60/163
  Verifying  : rubygem-json-1.7.7-33.el7_4.x86_64                                                                                                             61/163
  Verifying  : gssproxy-0.7.0-17.el7.x86_64                                                                                                                   62/163
  Verifying  : clufter-bin-0.77.0-2.el7.x86_64                                                                                                                63/163
  Verifying  : fence-agents-wti-4.0.11-86.el7.x86_64                                                                                                          64/163
  Verifying  : perl-Pod-Usage-1.63-3.el7.noarch                                                                                                               65/163
  Verifying  : libpath_utils-0.2.1-29.el7.x86_64                                                                                                              66/163
  Verifying  : perl-Encode-2.51-7.el7.x86_64                                                                                                                  67/163
  Verifying  : libverto-libevent-0.2.5-4.el7.x86_64                                                                                                           68/163
  Verifying  : fence-agents-rsb-4.0.11-86.el7.x86_64                                                                                                          69/163
  Verifying  : libnfsidmap-0.25-19.el7.x86_64                                                                                                                 70/163
  Verifying  : perl-threads-1.87-4.el7.x86_64                                                                                                                 71/163
  Verifying  : keyutils-1.5.8-3.el7.x86_64                                                                                                                    72/163
  Verifying  : checkpolicy-2.5-6.el7.x86_64                                                                                                                   73/163
  Verifying  : 1:liberation-fonts-common-1.07.2-16.el7.noarch                                                                                                 74/163
  Verifying  : perl-Getopt-Long-2.40-3.el7.noarch                                                                                                             75/163
  Verifying  : clufter-common-0.77.0-2.el7.noarch                                                                                                             76/163
  Verifying  : 7:lvm2-libs-2.02.177-4.el7.x86_64                                                                                                              77/163
  Verifying  : python-backports-ssl_match_hostname-3.5.0.1-1.el7.noarch                                                                                       78/163
  Verifying  : fence-agents-vmware-soap-4.0.11-86.el7.x86_64                                                                                                  79/163
  Verifying  : setools-libs-3.3.8-2.el7.x86_64                                                                                                                80/163
  Verifying  : perl-threads-shared-1.43-6.el7.x86_64                                                                                                          81/163
  Verifying  : perl-Storable-2.45-3.el7.x86_64                                                                                                                82/163
  Verifying  : fence-agents-all-4.0.11-86.el7.x86_64                                                                                                          83/163
  Verifying  : 4:perl-macros-5.16.3-292.el7.x86_64                                                                                                            84/163
  Verifying  : samba-common-4.7.1-6.el7.noarch                                                                                                                85/163
  Verifying  : corosynclib-2.4.3-2.el7.x86_64                                                                                                                 86/163
  Verifying  : fence-agents-ilo-moonshot-4.0.11-86.el7.x86_64                                                                                                 87/163
  Verifying  : fontpackages-filesystem-1.44-8.el7.noarch                                                                                                      88/163
  Verifying  : bc-1.06.95-13.el7.x86_64                                                                                                                       89/163
  Verifying  : fence-agents-emerson-4.0.11-86.el7.x86_64                                                                                                      90/163
  Verifying  : 1:perl-parent-0.225-244.el7.noarch                                                                                                             91/163
  Verifying  : avahi-libs-0.6.31-19.el7.x86_64                                                                                                                92/163
  Verifying  : pacemaker-cluster-libs-1.1.18-11.el7.x86_64                                                                                                    93/163
  Verifying  : libldb-1.2.2-1.el7.x86_64                                                                                                                      94/163
  Verifying  : fence-agents-vmware-rest-4.0.11-86.el7.x86_64                                                                                                  95/163
  Verifying  : libaio-0.3.109-13.el7.x86_64                                                                                                                   96/163
  Verifying  : gnutls-3.3.26-9.el7.x86_64                                                                                                                     97/163
  Verifying  : corosync-2.4.3-2.el7.x86_64                                                                                                                    98/163
  Verifying  : libcgroup-0.41-15.el7.x86_64                                                                                                                   99/163
  Verifying  : fence-virt-0.3.2-13.el7.x86_64                                                                                                                100/163
  Verifying  : rubygems-2.0.14.1-33.el7_4.noarch                                                                                                             101/163
  Verifying  : device-mapper-persistent-data-0.7.3-3.el7.x86_64                                                                                              102/163
  Verifying  : fence-agents-ilo-ssh-4.0.11-86.el7.x86_64                                                                                                     103/163
  Verifying  : libevent-2.0.21-4.el7.x86_64                                                                                                                  104/163
  Verifying  : fence-agents-scsi-4.0.11-86.el7.x86_64                                                                                                        105/163
  Verifying  : autogen-libopts-5.18-5.el7.x86_64                                                                                                             106/163
  Verifying  : libtalloc-2.1.10-1.el7.x86_64                                                                                                                 107/163
  Verifying  : audit-libs-python-2.8.1-3.el7.x86_64                                                                                                          108/163
  Verifying  : pacemaker-1.1.18-11.el7.x86_64                                                                                                                109/163
  Verifying  : resource-agents-3.9.5-124.el7.x86_64                                                                                                          110/163
  Verifying  : 1:quota-4.01-17.el7.x86_64                                                                                                                    111/163
  Verifying  : libyaml-0.1.4-11.el7_0.x86_64                                                                                                                 112/163
  Verifying  : libtevent-0.9.33-2.el7.x86_64                                                                                                                 113/163
  Verifying  : perl-Pod-Perldoc-3.20-4.el7.noarch                                                                                                            114/163
  Verifying  : device-mapper-multipath-libs-0.4.9-119.el7.x86_64                                                                                             115/163
  Verifying  : openwsman-python-2.6.3-3.git4391e5c.el7.x86_64                                                                                                116/163
  Verifying  : 4:perl-Time-HiRes-1.9725-3.el7.x86_64                                                                                                         117/163
  Verifying  : tcp_wrappers-7.6-77.el7.x86_64                                                                                                                118/163
  Verifying  : fence-agents-cisco-mds-4.0.11-86.el7.x86_64                                                                                                   119/163
  Verifying  : python-requests-2.6.0-1.el7_1.noarch                                                                                                          120/163
  Verifying  : libini_config-1.3.1-29.el7.x86_64                                                                                                             121/163
  Verifying  : pexpect-2.3-11.el7.noarch                                                                                                                     122/163
  Verifying  : libtirpc-0.2.4-0.10.el7.x86_64                                                                                                                123/163
  Verifying  : fence-agents-amt-ws-4.0.11-86.el7.x86_64                                                                                                      124/163
  Verifying  : fence-agents-eps-4.0.11-86.el7.x86_64                                                                                                         125/163
  Verifying  : perl-Exporter-5.68-3.el7.noarch                                                                                                               126/163
  Verifying  : libwsman1-2.6.3-3.git4391e5c.el7.x86_64                                                                                                       127/163
  Verifying  : perl-PathTools-3.40-5.el7.x86_64                                                                                                              128/163
  Verifying  : fence-agents-common-4.0.11-86.el7.x86_64                                                                                                      129/163
  Verifying  : perl-Carp-1.26-244.el7.noarch                                                                                                                 130/163
  Verifying  : fence-agents-brocade-4.0.11-86.el7.x86_64                                                                                                     131/163
  Verifying  : device-mapper-multipath-0.4.9-119.el7.x86_64                                                                                                  132/163
  Verifying  : pacemaker-cli-1.1.18-11.el7.x86_64                                                                                                            133/163
  Verifying  : rubygem-bigdecimal-1.2.0-33.el7_4.x86_64                                                                                                      134/163
  Verifying  : rubygem-io-console-0.4.2-33.el7_4.x86_64                                                                                                      135/163
  Verifying  : 1:perl-Pod-Simple-3.28-4.el7.noarch                                                                                                           136/163
  Verifying  : fence-agents-kdump-4.0.11-86.el7.x86_64                                                                                                       137/163
  Verifying  : perl-Time-Local-1.2300-2.el7.noarch                                                                                                           138/163
  Verifying  : fence-agents-rhevm-4.0.11-86.el7.x86_64                                                                                                       139/163
  Verifying  : python-six-1.9.0-2.el7.noarch                                                                                                                 140/163
  Verifying  : 7:lvm2-2.02.177-4.el7.x86_64                                                                                                                  141/163
  Verifying  : python-clufter-0.77.0-2.el7.noarch                                                                                                            142/163
  Verifying  : 1:quota-nls-4.01-17.el7.noarch                                                                                                                143/163
  Verifying  : libtdb-1.3.15-1.el7.x86_64                                                                                                                    144/163
  Verifying  : samba-client-libs-4.7.1-6.el7.x86_64                                                                                                          145/163
  Verifying  : libxslt-1.1.28-5.el7.x86_64                                                                                                                   146/163
  Verifying  : fence-agents-compute-4.0.11-86.el7.x86_64                                                                                                     147/163
  Verifying  : gnutls-utils-3.3.26-9.el7.x86_64                                                                                                              148/163
  Verifying  : fence-agents-ilo-mp-4.0.11-86.el7.x86_64                                                                                                      149/163
  Verifying  : perl-Scalar-List-Utils-1.27-248.el7.x86_64                                                                                                    150/163
  Verifying  : libwbclient-4.7.1-6.el7.x86_64                                                                                                                151/163
  Verifying  : fence-agents-ibmblade-4.0.11-86.el7.x86_64                                                                                                    152/163
  Verifying  : fence-agents-sbd-4.0.11-86.el7.x86_64                                                                                                         153/163
  Verifying  : ruby-2.0.0.648-33.el7_4.x86_64                                                                                                                154/163
  Verifying  : 1:cups-libs-1.6.3-35.el7.x86_64                                                                                                               155/163
  Verifying  : perl-podlators-2.5.1-3.el7.noarch                                                                                                             156/163
  Verifying  : 7:device-mapper-event-libs-1.02.146-4.el7.x86_64                                                                                              157/163
  Verifying  : ipmitool-1.8.18-7.el7.x86_64                                                                                                                  158/163
  Verifying  : 1:perl-TimeDate-2.30-2.el7.noarch                                                                                                             159/163
  Verifying  : perl-constant-1.27-2.el7.noarch                                                                                                               160/163
  Verifying  : python-chardet-2.2.1-1.el7_1.noarch                                                                                                           161/163
  Verifying  : fence-agents-eaton-snmp-4.0.11-86.el7.x86_64                                                                                                  162/163
  Verifying  : rubygem-psych-2.0.0-33.el7_4.x86_64                                                                                                           163/163

Installed:
  fence-agents-all.x86_64 0:4.0.11-86.el7     pacemaker.x86_64 0:1.1.18-11.el7     pcs.x86_64 0:0.9.162-5.el7.centos     resource-agents.x86_64 0:3.9.5-124.el7

Dependency Installed:
  OpenIPMI-modalias.x86_64 0:2.0.23-2.el7            audit-libs-python.x86_64 0:2.8.1-3.el7                     autogen-libopts.x86_64 0:5.18-5.el7
  avahi-libs.x86_64 0:0.6.31-19.el7                  bc.x86_64 0:1.06.95-13.el7                                 boost-system.x86_64 0:1.53.0-27.el7
  boost-thread.x86_64 0:1.53.0-27.el7                checkpolicy.x86_64 0:2.5-6.el7                             cifs-utils.x86_64 0:6.2-10.el7
  clufter-bin.x86_64 0:0.77.0-2.el7                  clufter-common.noarch 0:0.77.0-2.el7                       corosync.x86_64 0:2.4.3-2.el7
  corosynclib.x86_64 0:2.4.3-2.el7                   cups-libs.x86_64 1:1.6.3-35.el7                            device-mapper-event.x86_64 7:1.02.146-4.el7
  device-mapper-event-libs.x86_64 7:1.02.146-4.el7   device-mapper-multipath.x86_64 0:0.4.9-119.el7             device-mapper-multipath-libs.x86_64 0:0.4.9-119.el7
  device-mapper-persistent-data.x86_64 0:0.7.3-3.el7 fence-agents-amt-ws.x86_64 0:4.0.11-86.el7                 fence-agents-apc.x86_64 0:4.0.11-86.el7
  fence-agents-apc-snmp.x86_64 0:4.0.11-86.el7       fence-agents-bladecenter.x86_64 0:4.0.11-86.el7            fence-agents-brocade.x86_64 0:4.0.11-86.el7
  fence-agents-cisco-mds.x86_64 0:4.0.11-86.el7      fence-agents-cisco-ucs.x86_64 0:4.0.11-86.el7              fence-agents-common.x86_64 0:4.0.11-86.el7
  fence-agents-compute.x86_64 0:4.0.11-86.el7        fence-agents-drac5.x86_64 0:4.0.11-86.el7                  fence-agents-eaton-snmp.x86_64 0:4.0.11-86.el7
  fence-agents-emerson.x86_64 0:4.0.11-86.el7        fence-agents-eps.x86_64 0:4.0.11-86.el7                    fence-agents-heuristics-ping.x86_64 0:4.0.11-86.el7
  fence-agents-hpblade.x86_64 0:4.0.11-86.el7        fence-agents-ibmblade.x86_64 0:4.0.11-86.el7               fence-agents-ifmib.x86_64 0:4.0.11-86.el7
  fence-agents-ilo-moonshot.x86_64 0:4.0.11-86.el7   fence-agents-ilo-mp.x86_64 0:4.0.11-86.el7                 fence-agents-ilo-ssh.x86_64 0:4.0.11-86.el7
  fence-agents-ilo2.x86_64 0:4.0.11-86.el7           fence-agents-intelmodular.x86_64 0:4.0.11-86.el7           fence-agents-ipdu.x86_64 0:4.0.11-86.el7
  fence-agents-ipmilan.x86_64 0:4.0.11-86.el7        fence-agents-kdump.x86_64 0:4.0.11-86.el7                  fence-agents-mpath.x86_64 0:4.0.11-86.el7
  fence-agents-rhevm.x86_64 0:4.0.11-86.el7          fence-agents-rsa.x86_64 0:4.0.11-86.el7                    fence-agents-rsb.x86_64 0:4.0.11-86.el7
  fence-agents-sbd.x86_64 0:4.0.11-86.el7            fence-agents-scsi.x86_64 0:4.0.11-86.el7                   fence-agents-vmware-rest.x86_64 0:4.0.11-86.el7
  fence-agents-vmware-soap.x86_64 0:4.0.11-86.el7    fence-agents-wti.x86_64 0:4.0.11-86.el7                    fence-virt.x86_64 0:0.3.2-13.el7
  fontpackages-filesystem.noarch 0:1.44-8.el7        gnutls.x86_64 0:3.3.26-9.el7                               gnutls-dane.x86_64 0:3.3.26-9.el7
  gnutls-utils.x86_64 0:3.3.26-9.el7                 gssproxy.x86_64 0:0.7.0-17.el7                             ipmitool.x86_64 0:1.8.18-7.el7
  keyutils.x86_64 0:1.5.8-3.el7                      libaio.x86_64 0:0.3.109-13.el7                             libbasicobjects.x86_64 0:0.1.1-29.el7
  libcgroup.x86_64 0:0.41-15.el7                     libcollection.x86_64 0:0.7.0-29.el7                        liberation-fonts-common.noarch 1:1.07.2-16.el7
  liberation-sans-fonts.noarch 1:1.07.2-16.el7       libevent.x86_64 0:2.0.21-4.el7                             libini_config.x86_64 0:1.3.1-29.el7
  libldb.x86_64 0:1.2.2-1.el7                        libnfsidmap.x86_64 0:0.25-19.el7                           libpath_utils.x86_64 0:0.2.1-29.el7
  libqb.x86_64 0:1.0.1-6.el7                         librados2.x86_64 1:0.94.5-2.el7                            libref_array.x86_64 0:0.1.5-29.el7
  libsemanage-python.x86_64 0:2.5-11.el7             libtalloc.x86_64 0:2.1.10-1.el7                            libtdb.x86_64 0:1.3.15-1.el7
  libtevent.x86_64 0:0.9.33-2.el7                    libtirpc.x86_64 0:0.2.4-0.10.el7                           libverto-libevent.x86_64 0:0.2.5-4.el7
  libwbclient.x86_64 0:4.7.1-6.el7                   libwsman1.x86_64 0:2.6.3-3.git4391e5c.el7                  libxslt.x86_64 0:1.1.28-5.el7
  libyaml.x86_64 0:0.1.4-11.el7_0                    lvm2.x86_64 7:2.02.177-4.el7                               lvm2-libs.x86_64 7:2.02.177-4.el7
  net-snmp-libs.x86_64 1:5.7.2-32.el7                net-snmp-utils.x86_64 1:5.7.2-32.el7                       net-tools.x86_64 0:2.0-0.22.20131004git.el7
  nettle.x86_64 0:2.7.1-8.el7                        nfs-utils.x86_64 1:1.3.0-0.54.el7                          openwsman-python.x86_64 0:2.6.3-3.git4391e5c.el7
  overpass-fonts.noarch 0:2.1-1.el7                  pacemaker-cli.x86_64 0:1.1.18-11.el7                       pacemaker-cluster-libs.x86_64 0:1.1.18-11.el7
  pacemaker-libs.x86_64 0:1.1.18-11.el7              perl.x86_64 4:5.16.3-292.el7                               perl-Carp.noarch 0:1.26-244.el7
  perl-Encode.x86_64 0:2.51-7.el7                    perl-Exporter.noarch 0:5.68-3.el7                          perl-File-Path.noarch 0:2.09-2.el7
  perl-File-Temp.noarch 0:0.23.01-3.el7              perl-Filter.x86_64 0:1.49-3.el7                            perl-Getopt-Long.noarch 0:2.40-3.el7
  perl-HTTP-Tiny.noarch 0:0.033-3.el7                perl-PathTools.x86_64 0:3.40-5.el7                         perl-Pod-Escapes.noarch 1:1.04-292.el7
  perl-Pod-Perldoc.noarch 0:3.20-4.el7               perl-Pod-Simple.noarch 1:3.28-4.el7                        perl-Pod-Usage.noarch 0:1.63-3.el7
  perl-Scalar-List-Utils.x86_64 0:1.27-248.el7       perl-Socket.x86_64 0:2.010-4.el7                           perl-Storable.x86_64 0:2.45-3.el7
  perl-Text-ParseWords.noarch 0:3.29-4.el7           perl-Time-HiRes.x86_64 4:1.9725-3.el7                      perl-Time-Local.noarch 0:1.2300-2.el7
  perl-TimeDate.noarch 1:2.30-2.el7                  perl-constant.noarch 0:1.27-2.el7                          perl-libs.x86_64 4:5.16.3-292.el7
  perl-macros.x86_64 4:5.16.3-292.el7                perl-parent.noarch 1:0.225-244.el7                         perl-podlators.noarch 0:2.5.1-3.el7
  perl-threads.x86_64 0:1.87-4.el7                   perl-threads-shared.x86_64 0:1.43-6.el7                    pexpect.noarch 0:2.3-11.el7
  policycoreutils-python.x86_64 0:2.5-22.el7         psmisc.x86_64 0:22.20-15.el7                               python-IPy.noarch 0:0.75-6.el7
  python-backports.x86_64 0:1.0-8.el7                python-backports-ssl_match_hostname.noarch 0:3.5.0.1-1.el7 python-chardet.noarch 0:2.2.1-1.el7_1
  python-clufter.noarch 0:0.77.0-2.el7               python-ipaddress.noarch 0:1.0.16-2.el7                     python-lxml.x86_64 0:3.2.1-4.el7
  python-requests.noarch 0:2.6.0-1.el7_1             python-setuptools.noarch 0:0.9.8-7.el7                     python-six.noarch 0:1.9.0-2.el7
  python-suds.noarch 0:0.4.1-5.el7                   python-urllib3.noarch 0:1.10.2-5.el7                       quota.x86_64 1:4.01-17.el7
  quota-nls.noarch 1:4.01-17.el7                     rpcbind.x86_64 0:0.2.0-44.el7                              ruby.x86_64 0:2.0.0.648-33.el7_4
  ruby-irb.noarch 0:2.0.0.648-33.el7_4               ruby-libs.x86_64 0:2.0.0.648-33.el7_4                      rubygem-bigdecimal.x86_64 0:1.2.0-33.el7_4
  rubygem-io-console.x86_64 0:0.4.2-33.el7_4         rubygem-json.x86_64 0:1.7.7-33.el7_4                       rubygem-psych.x86_64 0:2.0.0-33.el7_4
  rubygem-rdoc.noarch 0:4.0.0-33.el7_4               rubygems.noarch 0:2.0.14.1-33.el7_4                        samba-client-libs.x86_64 0:4.7.1-6.el7
  samba-common.noarch 0:4.7.1-6.el7                  samba-common-libs.x86_64 0:4.7.1-6.el7                     setools-libs.x86_64 0:3.3.8-2.el7
  tcp_wrappers.x86_64 0:7.6-77.el7                   trousers.x86_64 0:0.3.14-2.el7                             unbound-libs.x86_64 0:1.6.6-1.el7

Complete!
```