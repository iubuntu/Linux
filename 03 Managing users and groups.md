
## Introduction to users and groups

Each `user` is associated with a unique numerical identification number called _user ID_(**UID**). 
Each `group` is associated with a _group ID_ (**GID**). 

Users within a group share the same permissions to read, write, and execute files owned by that group.

## Configuring reserved user and group IDs

> RHEL reserves user and group IDs below 1000 for system users and groups.

| uid   | meaning          |
| ----- | ---------------- |
| 0     | root             |
| 1-999 | system reservers |
| 1000+ | normal users     |

- `/etc/login.defs`

The first User ID
```
# Min/max values for automatic uid selection in useradd
#
UID_MIN                  1000
```

The first Group Id
```
# Min/max values for automatic gid selection in groupadd
#
GID_MIN                  **1000**
```

# user
## add

```
没有指定任何选项：
# useradd user10
# grep 'user10' /etc/passwd /etc/shadow /etc/group
/etc/passwd:user10:x:506:510::/home/user10:/bin/bash
/etc/shadow:user10:!!:15949:0:99999:7:::
/etc/group:user10:x:510:
小结：当创建一个用户时，如果没有指定用户的主组，将会创建一个同名的组作为用户的主组。

# id user10
uid=506(user10) gid=510(user10) groups=510(user10)

# ll -d /home/user10/
drwx------ 3 user10 user10 4096 09-01 21:14 /home/user10/		//HOME目录
# ll /var/spool/mail/user10 									//用户mail spool
-rw-rw---- 1 user10 mail 0 09-01 21:14 /var/spool/mail/user10
```

## delete

```
# userdel user10		//删除用户user10，但不删除用户家目录和mail spool
# ll -d /home/user10/
drwx------ 3 506 510 4096 09-01 21:14 /home/user10/
# ll /var/spool/mail/user10 
-rw-rw---- 1 506 mail 0 09-01 21:14 /var/spool/mail/user10

# userdel -r user11
# ll /home/user11
ls: /home/user11: 没有那个文件或目录
# ll /var/spool/mail/user11
ls: /var/spool/mail/user11: 没有那个文件或目录
```

## add users with options
```
[root@station230 ~]# useradd user01		
[root@station230 ~]# useradd user02 -u 503				//创建用户usr02，指定uid
[root@station230 ~]# useradd user03 -d /aaa				//创建用户user03 指定家目录
[root@station230 ~]# useradd user04 -M						//创建用户user04，不创建家目录
[root@station230 ~]# useradd user05 -s /sbin/nologin 	//创建用户并指定shell
[root@station230 ~]# useradd user06 -g hr					//创建用户，指定主组
[root@station230 ~]# useradd user07 -G sale				//创建用户，指定附加组
[root@station230 ~]# useradd user08 -e 2013-04-01  	//指定过期时间
[root@station230 ~]# useradd user10 -u 4000 -s /sbin/nologin
```

## modify a user account
- change default shell

```
[root@station230 ~]# usermod --help
[root@station230 ~]# useradd user10
[root@station230 ~]# grep 'user10' /etc/passwd
user10:x:509:509::/home/user10:/bin/bash
[root@station230 ~]# usermod -u 2000 user10					//修改用户uid
[root@station230 ~]# usermod -s /sbin/nologin user10		//修改用户shell
```

- lock/unlock user
```
[root@station80 ~]# useradd user1000
[root@station80 ~]# passwd user1000
[root@station80 ~]# grep 'user1000' /etc/shadow
user1000:$1$Hw2wCJoe$FU91eSBsBx1W0CGdIhTwh/:15775:0:99999:7:::
[root@station80 ~]# usermod -L user1000
[root@station80 ~]# grep 'user1000' /etc/shadow
user1000:!$1$Hw2wCJoe$FU91eSBsBx1W0CGdIhTwh/:15775:0:99999:7:::
登录测试

[root@station80 ~]# usermod -U user1000
[root@station80 ~]# grep 'user1000' /etc/shadow
user1000:$1$Hw2wCJoe$FU91eSBsBx1W0CGdIhTwh/:15775:0:99999:7:::
登录测试
```
- user expire
```
＝＝设置账号过期＝＝
[root@station80 ~]# date
2013年 03月 11日 星期一 15:36:19 CST
[root@station80 ~]# usermod -e 2013-02-11 user1000
[root@station80 ~]# grep 'user1000' /etc/shadow
user1000:$1$Hw2wCJoe$FU91eSBsBx1W0CGdIhTwh/:15775:0:99999:7::15747:
登录测试
```

# group

```
# groupadd hr
# groupadd sale
# groupadd it
# groupadd net01 -g 2000		添加组net01，并指定gid 2000
# groupdel net01					删除组net01
# grep 'net01' /etc/group		查看/etc/group中组net01信息
```

## group members
```
注意：gpasswd将用户添加到组或从组中删除，只针对已存在的用户
[root@station230 ~]# gpasswd -a user07 it					//将某个用户加入到某个组
[root@station230 ~]# gpasswd -M user02,user03,user04 it  //将多个用户加入到it组
[root@station230 ~]# grep 'it' /etc/group						//查看it组中的成员
it:x:505:user02,user03,user04
[root@station230 ~]# gpasswd -d user07 it					//删除用户usr07从it组
```

>A list of all groups is stored in the `/etc/group` configuration file.


# reset root password

[reset passwrod
](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_basic_system_settings/managing-users-and-groups_configuring-basic-system-settings#resetting-the-forgotten-root-password-on-boot_changing-and-resetting-the-root-password-from-the-command-line)


















