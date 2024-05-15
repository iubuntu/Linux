> File system permissions control the ability of user and group accounts to read, modify, and execute the contents of the files and to enter directories. Set permissions carefully to protect your data against unauthorized access.

## Managing file permissions

Every file or directory has three levels of ownership:

- User owner (**u**).
- Group owner (**g**).
- Others (**o**).

Each level of ownership can be assigned the following permissions:

- Read (**r**).        => 4
- Write (**w**).      => 2
- Execute (**x**).  => 1


| Permission           | Symbolic value | r   | w   | x   | Octal value |
| -------------------- | -------------- | --- | --- | --- | ----------- |
| No permission        | ---            | 0   | 0   | 0   | 0           |
| Execute              | --x            | 0   | 0   | 1   | 1           |
| Write                | -w-            | 0   | 1   | 0   | 2           |
| Read                 | r--            | 1   | 0   | 0   | 4           |
| Write, Execute       | -wx            | 0   | 1   | 1   | 3           |
| Read, Execute        | r-x            | 1   | 0   | 1   | 5           |
| Read, Write          | rw-            | 1   | 1   | 0   | 6           |
| Read, Write, Execute | rwx            | 1   | 1   | 1   | 7           |


---
## permissions

- Base permission  [base permission
](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_basic_system_settings/managing-file-system-permissions_configuring-basic-system-settings#base-permissions_assembly_managing-file-permissions)
- The _user file-creation mode mask_ (**umask**).


### directory permission

The base permission for a directory is `777` (`drwxrwxrwx`), which grants everyone the permissions to read, write, and execute. This means that the directory owner, the group, and others can list the contents of the directory, create, delete, and edit items within the directory, and descend into it.

Note that individual files within a directory can have their own permission that might prevent you from editing them, despite having unrestricted access to the directory.

### file permission
The base permission for a file is `666` (`-rw-rw-rw-`), which grants everyone the permissions to read and write. This means that the file owner, the group, and others can read and edit the file.
### umask command
```
[root@station230 ~]# umask 				//查看当前用户的umask权限
0022
[root@station230 ~]# umask -S
u=rwx,g=rx,o=rx

[root@station230 ~]# umask 000		//设置umask权限
[root@station230 ~]# umask 
0000
[root@station230 ~]# touch file8		//创建file8文件
[root@station230 ~]# mkdir dir8		//创建目录
[root@station230 ~]# ll -d dir8 file8	//查看文件目录权限
drwxrwxrwx 2 root root 4096 10-26 14:10 dir8
-rw-rw-rw- 1 root root    0 10-26 14:10 file8
[root@station230 ~]# umask 222
[root@station230 ~]# umask 
0222

==============================================================
小知识：
[root@station230 ~]# umask 077; touch file60		//当前shell生效
[root@station230 ~]# (umask 077; touch file70)	//()表示在子shell生效 sub shell
[root@station230 ~]# ll file70 
-rw------- 1 root root 0 10-26 14:31 file70
[root@station230 ~]# 
[root@station230 ~]# umask 
0022
```
---

## modify permissions
### change owner 
```
[root@station230 ~]# chown alice.hr file1 	//改属主、属组
[root@station230 ~]# chown alice     file1 		//只改属主
[root@station230 ~]# chown        .hr file1		//只改属组
[root@station230 ~]# chown -R alice:alice dir1	//修改所有在dir1下的 目录和文件的 owner和group 
```
### change group
```
[root@station230 ~]# chgrp it file1				//改文件属组
[root@station230 ~]# chgrp -R it dir1			//改文件属组
```

## change file modes or Access Control Lists

To add or remove permissions you can use the following _signs_:

- `+` to add the permissions on top of the existing permissions
- `-` to remove the permissions from the existing permission
- `=` to remove the existing permissions and explicitly define the new ones

|       |  levels of ownership | operator / signs | permission |
| ----- | -------------------- | ---------------- | ---------- |
| chmod | u                    | +                | r          |
|       | g                    | -                | w          |
|       | o                    | =                | x          |
|       | a                    |                  |            |
```
[root@station230 ~]# chmod u+x file1			//属主增加执行
[root@station230 ~]# chmod a=rwx file1		//所有人等于读写执行
[root@station230 ~]# chmod a=- file1			//所有人没有权限
[root@station230 ~]# chmod ug=rw,o=r file1 	 //属主属组等于读写，其他人只读
[root@station230 ~]# ll file1 			 				//以长模式方式查看文件权限
-rw-rw-r-- 1 alice it 17 10-25 16:45 file1	 		//显示的结果

=b. 数字
[root@station230 ~]# chmod 644 file1
[root@station230 ~]# ll file1
-rw-r--r-- 1 alice it 17 10-25 16:45 file1

=================================================================
小知识： r、w、x权限对文件和目录的意义

=================================================================
```

## Special permission explained
```
suid	4
sgid	2
sticky	1
```

Special permissions make up a fourth access level in addition to **user**, **group**, and **other**. Special permissions allow for additional privileges over the standard permission sets (as the name suggests). There is a special permission option for each access level discussed previously. Let's take a look at each one individually, beginning with Set UID:

## user + s (pecial)

Commonly noted as **SUID**, the special permission for the user access level has a single function: A file with **SUID** always executes as the user who owns the file, regardless of the user passing the command. If the file owner doesn't have execute permissions, then use an uppercase **S** here.

Now, to see this in a practical light, let's look at the `/usr/bin/passwd` command. This command, by default, has the SUID permission set:

```shell
[tcarrigan@server ~]$ ls -l /usr/bin/passwd 
-rwsr-xr-x. 1 root root 33544 Dec 13  2019 /usr/bin/passwd
```

Note the **s** where **x** would usually indicate execute permissions for the user.

## group + s (pecial)

Commonly noted as **SGID**, this special permission has a couple of functions:

- If set on a file, it allows the file to be executed as the **group** that owns the file (similar to SUID)
- If set on a directory, any files created in the directory will have their **group** ownership set to that of the directory owner

```shell
[tcarrigan@server article_submissions]$ ls -l 
total 0
drwxrws---. 2 tcarrigan tcarrigan  69 Apr  7 11:31 my_articles
```


This permission set is noted by a lowercase **s** where the **x** would normally indicate **execute** privileges for the **group**. It is also especially useful for directories that are often used in collaborative efforts between members of a group. Any member of the group can access any new file. This applies to the execution of files, as well. **SGID** is very powerful when utilized properly.

As noted previously for **SUID**, if the owning group does not have execute permissions, then an uppercase **S** is used.

## other + t (sticky)

The last special permission has been dubbed the "sticky bit." This permission does not affect individual files. However, at the directory level, it restricts file deletion. Only the **owner** (and **root**) of a file can remove the file within that directory. A common example of this is the `/tmp` directory:

```shell
[tcarrigan@server article_submissions]$ ls -ld /tmp/
drwxrwxrwt. 15 root root 4096 Sep 22 15:28 /tmp/
```

The permission set is noted by the lowercase **t**, where the **x** would normally indicate the execute privilege.

## Setting special permissions

To set special permissions on a file or directory, you can utilize either of the two methods outlined for standard permissions above: Symbolic or numerical.

Let's assume that we want to set **SGID** on the directory `community_content`.

To do this using the symbolic method, we do the following:

```shell
[tcarrigan@server article_submissions]$ chmod g+s community_content/
```

Using the numerical method, we need to pass a fourth, preceding digit in our `chmod`command. The digit used is calculated similarly to the standard permission digits:

- Start at 0
- SUID = 4
- SGID = 2
- Sticky = 1

The syntax is:

```shell
[tcarrigan@server ~]$ chmod X### file | directory
```

Where **X** is the special permissions digit.

Here is the command to set **SGID** on `community_content` using the numerical method:

```shell
[tcarrigan@server article_submissions]$ chmod 2770 community_content/
[tcarrigan@server article_submissions]$ ls -ld community_content/
drwxrws---. 2 tcarrigan tcarrigan 113 Apr  7 11:32 community_content/
```





---
## Access Control List (ACL)

[ACL
](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/configuring_basic_system_settings/managing-file-system-permissions_configuring-basic-system-settings#assembly_managing-access-control-list_managing-file-system-permissions)



```
文件权限管理之四： ACL: UGO权限的扩展
UGO传统权限：只能一个用户，一个组和其他人
＝ACL基本＝
设置：
[root@station230 ~]# touch /home/test.txt
[root@station230 ~]# ll /home/test.txt	
-rw-r--r-- 1 root root 0 10-26 13:59 /home/test.txt

[root@station230 ~]# getfacl /home/test.txt
[root@station230 ~]# setfacl -m u:alice:rw /home/test.txt	//增加用户alice权限
[root@station230 ~]# setfacl -m u:jack:- /home/test.txt     	//增加用户jack权限

查看/删除：
[root@station230 ~]# ll /home/test.txt 
-rw-rw-r--+ 1 root root 0 10-26 13:59 /home/test.txt
[root@station230 ~]# getfacl /home/test.txt

[root@station230 ~]# setfacl -m g:hr:r /home/test.txt
[root@station230 ~]# setfacl -x g:hr /home/test.txt	 			//删除组hr的权限
[root@station230 ~]# setfacl -b /home/test.txt 		 				//删除所有acl权限

帮助：
man setfacl
/EXAMPLES


＝ACL高级＝
mask：
用于临时降低用户（除属主和其他人）的权限
[root@yangs ~]# setfacl -m m::--- /home/file100.txt


default: 继承（默认）
要求： 希望/home/hr下所有文件（包括以后产生文件），alice都可以读写执行

思路：
步骤一： 将/home/hr下现有的文件赋予alice读写权限
[root@yangs ~]# setfacl -R -m u:alice:rwx /home/hr

步骤二： 使alice的权限继承
[root@yangs ~]# setfacl -m d:u:alice:rwx /home/hr
```

---
## File attributes

The format of a symbolic mode is +-=[aAcCdDeFijmPsStTux].
The letters 'aAcCdDeFijmPsStTux' select the new attributes for the files:
- append only  (a)
-  no atime updates (A)
- compressed (c)
- no copy on write (C)
- no dump (d)
- synchronous directory updates (D)
- ex‐ent format (e)
- case-insensitive directory lookups (F)
- immutable (i)
- data  journaling  (j)
- don't compress  (m)
- project  hierarchy  (P)
- secure deletion (s)
- synchronous updates (S)
- no tail-merging (t)
- top of directory hierarchy (T)
- undeletable (u)
- and direct access for files (x).

The following attributes are read-only, and may be listed by lsattr(1) but not modified by chattr: 
- en‐crypted (E)
- indexed directory (I)
- inline data (N)
-  verity (V).

```
设置文件属性(权限)，针对所有用户，包括root
[root@station230 ~]# lsattr file100 file200 file300 
-------------e- file100
-------------e- file200
-------------e- file300
[root@station230 ~]# chattr +a file100 
[root@station230 ~]# chattr +i file200 
[root@station230 ~]# chattr +A file300

[root@station230 ~]# lsattr file100 file200 file300 
-----a-------e- file100
----i--------e- file200
-------A-----e- file300

[root@station230 ~]# echo 111 > file100
bash: file100: Operation not permitted
[root@station230 ~]# rm -rf file100 
rm: cannot remove `file100': Operation not permitted
[root@station230 ~]# echo 111 >> file100

# echo 111 > file200
bash: file200: Permission denied
[root@instructor ~]# echo 111 >> file200
bash: file200: Permission denied
[root@instructor ~]# rm -rf file200 
rm: cannot remove `file200': Operation not permitted

# chattr -a file100
[root@instructor ~]# chattr -i file200
[root@instructor ~]# chattr -i file200
```