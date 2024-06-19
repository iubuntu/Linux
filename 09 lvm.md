
```
创建	 		扫描		   显示详细		显示	 	扩展           	缩小  			删除         	更改
pvcreate	pvscan	   pvdisplay    pvs									    pvremove
vgcreate	vgscan	   vgdisplay	vgs 	vgextend  						vgremove       	vgchange
lvcreate	lvscan	   lvdisplay    lvs		lvextend	 	  lvreduce		lvremove       	lvchange

```

# LVM architecture

![[Pasted image 20240619204047.png]]

- Physical volume

A physical volume (PV) is a partition or whole disk designated for LVM use. For more information, see [Managing LVM physical volumes](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_and_managing_logical_volumes/managing-lvm-physical-volumes_configuring-and-managing-logical-volumes).

- Volume group

A volume group (VG) is a collection of physical volumes (PVs), which creates a pool of disk space out of which logical volumes can be allocated. For more information, see [Managing LVM volume groups](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_and_managing_logical_volumes/managing-lvm-volume-groups_configuring-and-managing-logical-volumes).

- Logical volume

A logical volume represents a mountable storage device. For more information, see [Managing LVM logical volumes](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_and_managing_logical_volumes/managing-lvm-logical-volumes_configuring-and-managing-logical-volumes).

#  Managing LVM physical volumes
## Creating LVM physical volume

```
[root@localhost ~]# pvcreate /dev/nvme0n1
  Physical volume "/dev/nvme0n1" successfully created.
```


## checking the created physical volumes
- pvs
```
[root@localhost ~]# pvs
  PV           VG Fmt  Attr PSize  PFree
  /dev/nvme0n1    lvm2 ---  10.00g 10.00g
  /dev/vda3    cs lvm2 a--  62.41g     0
[root@localhost ~]# pvs /dev/nvme0n1
  PV           VG Fmt  Attr PSize  PFree
  /dev/nvme0n1    lvm2 ---  10.00g 10.00g
```

- pvdisplay
```
[root@localhost ~]# pvdisplay /dev/nvme0n1
  "/dev/nvme0n1" is a new physical volume of "10.00 GiB"
  --- NEW Physical volume ---
  PV Name               /dev/nvme0n1
  VG Name
  PV Size               10.00 GiB
  Allocatable           NO
  PE Size               0
  Total PE              0
  Free PE               0
  Allocated PE          0
  PV UUID               Dcp3qO-uViY-P5ew-2ElR-2c3u-ESn6-6YMkV9
```
- pvscan
```
[root@localhost ~]# pvscan
  PV /dev/vda3      VG cs   lvm2 [62.41 GiB / 0    free]
  PV /dev/nvme0n1           lvm2 [10.00 GiB]
  Total: 2 [72.41 GiB] / in use: 1 [62.41 GiB] / in no VG: 1 [10.00 GiB]
```

# Managing LVM volume groups

## Creating LVM volume group

```
[root@localhost ~]# vgcreate mysql /dev/nvme0n1
  Volume group "mysql" successfully created
```
## checking volume group
- vgs
```
[root@localhost ~]# vgs
  VG    #PV #LV #SN Attr   VSize   VFree
  cs      1   3   0 wz--n-  62.41g      0
  mysql   1   0   0 wz--n- <10.00g <10.00g
[root@localhost ~]# vgs mysql
  VG    #PV #LV #SN Attr   VSize   VFree
  mysql   1   0   0 wz--n- <10.00g <10.00g
```
- vgdisplay
```
[root@localhost ~]# vgdisplay mysql
  --- Volume group ---
  VG Name               mysql
  System ID
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  1
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                0
  Open LV               0
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <10.00 GiB
  PE Size               4.00 MiB
  Total PE              2559
  Alloc PE / Size       0 / 0
  Free  PE / Size       2559 / <10.00 GiB
  VG UUID               jG84vB-ZVQc-J5xk-85ha-AIFp-GoSo-pYQaKF
```
- vgscan
```
[root@localhost ~]# vgscan
  Found volume group "cs" using metadata type lvm2
  Found volume group "mysql" using metadata type lvm2
```

## Increasing a vg’s capacity
- adding one or more free physical volumes
```
[root@localhost ~]# pvcreate /dev/nvme1n1
  Physical volume "/dev/nvme1n1" successfully created.
```
- extending vg
```
[root@localhost ~]# vgextend mysql /dev/nvme1n1
  Volume group "mysql" successfully extended
```
- checking vg
```
[root@localhost ~]# vgs mysql
  VG    #PV #LV #SN Attr   VSize  VFree
  mysql   2   0   0 wz--n- 19.99g 19.99g
``` 
# Managing LVM logical volumes
## Creating LVM logical volume

```
[root@localhost ~]# lvcreate -n 3306 -L 500M mysql
  Logical volume "3306" created
```

- the `-n` option to set the LV name to _mylv_, 
- the `-L` option to set the size of LV in units of Mb, but it is possible to use any other units. 
- The LV type is `linear` by default, but the user can specify the desired type by using the `--type` option.
# Checking lv

- lvs
```
[root@localhost ~]# lvs mysql/3306
  LV   VG    Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  3306 mysql -wi-a----- 500.00m
[root@localhost ~]# lvs
  LV   VG    Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  home cs    -wi-ao---- <19.18g
  root cs    -wi-ao---- <39.29g
  swap cs    -wi-ao----   3.94g
  3306 mysql -wi-a----- 500.00m
```
- lvdisplay
```
[root@localhost ~]# lvdisplay mysql/3306
  --- Logical volume ---
  LV Path                /dev/mysql/3306
  LV Name                3306
  VG Name                mysql
  LV UUID                kjdcb2-F5Kp-GdQO-i4pH-O09c-olgU-XXbCze
  LV Write Access        read/write
  LV Creation host, time localhost.localdomain, 2024-06-19 20:54:37 +1000
  LV Status              available
  # open                 0
  LV Size                500.00 MiB
  Current LE             125
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           253:3
  ```

- lvscan
```
[root@localhost ~]# lvscan
  ACTIVE            '/dev/cs/swap' [3.94 GiB] inherit
  ACTIVE            '/dev/cs/home' [<19.18 GiB] inherit
  ACTIVE            '/dev/cs/root' [<39.29 GiB] inherit
  ACTIVE            '/dev/mysql/3306' [500.00 MiB] inherit
```

---
## Using lv
- creating a file system
```
[root@localhost ~]# mkfs.xfs /dev/mysql/3306
meta-data=/dev/mysql/3306        isize=512    agcount=4, agsize=32000 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=1 inobtcount=1 nrext64=0
data     =                       bsize=4096   blocks=128000, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=16384, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
Discarding blocks...Done
```

- mounting
```
[root@localhost ~]# mount /dev/mysql/3306 /data/3306
[root@localhost ~]# df  -Ph /data/3306
Filesystem              Size  Used Avail Use% Mounted on
/dev/mapper/mysql-3306  436M   29M  408M   7% /data/3306
```

# Modifying the size of a logical volume
- Increasing to 1G

```
[root@localhost ~]# lvextend -r -L 1G /dev/mysql/3306
  Size of logical volume mysql/3306 changed from 500.00 MiB (125 extents) to 1.00 GiB (256 extents).
  File system xfs found on mysql/3306 mounted at /data/3306.
  Extending file system xfs to 1.00 GiB (1073741824 bytes) on mysql/3306...
xfs_growfs /dev/mysql/3306
meta-data=/dev/mapper/mysql-3306 isize=512    agcount=4, agsize=32000 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=1 inobtcount=1 nrext64=0
data     =                       bsize=4096   blocks=128000, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=16384, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 128000 to 262144
xfs_growfs done
  Extended file system xfs on mysql/3306.
  Logical volume mysql/3306 successfully resized.
[root@localhost ~]# df  -Ph /data/3306
Filesystem              Size  Used Avail Use% Mounted on
/dev/mapper/mysql-3306  960M   33M  928M   4% /data/3306
```
- Filling all of the unallocated space
1. lvextend
```
[root@localhost ~]# lvextend -l +100%FREE /dev/mysql/3306
  Size of logical volume mysql/3306 changed from 1.00 GiB (256 extents) to 19.99 GiB (5118 extents).
  Logical volume mysql/3306 successfully resized.
```
2. growing file system
```
[root@localhost ~]# xfs_growfs /dev/mysql/3306
meta-data=/dev/mapper/mysql-3306 isize=512    agcount=9, agsize=32000 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=1, sparse=1, rmapbt=0
         =                       reflink=1    bigtime=1 inobtcount=1 nrext64=0
data     =                       bsize=4096   blocks=262144, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
log      =internal log           bsize=4096   blocks=16384, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 262144 to 5240832
[root@localhost ~]# df  -Ph /data/3306
Filesystem              Size  Used Avail Use% Mounted on
/dev/mapper/mysql-3306   20G  177M   20G   1% /data/3306
```

# Snapshot of logical volumes

[snapshot](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_and_managing_logical_volumes/snapshot-of-logical-volumes_configuring-and-managing-logical-volumes)

# Documentation

[LVM](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_and_managing_logical_volumes/index)
