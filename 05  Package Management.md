- [packages](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/packaging_and_distributing_software/index)

# Install Applications / software
- source code
- binary files
- package manager 

# 1. source code
- download source code
```sh
wget https://github.com/iubuntu/learningLinux/archive/refs/tags/v1.0.tar.gz
tar xf v1.0.tar.gz
cd learningLinux-1.0
```
### CMake
> sudo yum install cmake gcc gcc-c++

- configure
```
mkdir build
cd build
cmake ../
```
- build
```
 make
```

- install
```
sudo make install
```
> you can specific the command location with the `--prefix` 

# 2. binary files
- [releases](https://github.com/iubuntu/learningLinux/releases)
### download the binary files
- ARM
```
wget https://github.com/iubuntu/learningLinux/releases/download/v1.0/learningLinux_1.0_aarch64.tar.gz
```
- X86
```
wget https://github.com/iubuntu/learningLinux/releases/download/v1.0/learningLinux_1.0_amd64.tar.gz
```

### Install
```
tar xf learningLinux_1.0_amd64.tar.gz
ls
```

# 3. RPM

RPM stands for `Red Hat Package Manager`. It was developed by `Red Hat` and is primarily used on Red Hat-based Linux operating systems 
- [Fedora](https://fedoraproject.org)
- CentOS
- RHEL
- [Amazon Linux 2](https://aws.amazon.com/amazon-linux-2/)

An RPM package uses the `.rpm` extension and is a bundle (a collection) of different files. It can contain the following:

- Binary files, also known as executables (`nmap`, `stat`, `xattr`, `ssh`, `sshd`, and so on).
- Configuration files (`sshd.conf`, `updatedb.conf`, `logrotate.conf`, etc.).
- Documentation files (`README`, `TODO`, `AUTHOR`, etc.).
### Naming

The name of an RPM package follows this format:

```plaintext
<name>-<version>-<release>.<distribution>.<arch>.rpm
```
For example
```

learninglinux-1.1-1.el9.aarch64.rpm
    ^          ^  ^  ^    ^
    |          |  |  |    |
    |          |  |  |    + -> architecture
    |          |  |  +-------> distribution
    |          |  +----------> release
    |          +-------------> version
    +------------------------> name
```

### installing rpm
- download rpm
```
wget https://github.com/iubuntu/learningLinux/releases/download/v1.1/learninglinux-1.1-1.el9.aarch64.rpm
```
- install rpm
```
rpm -ivh learninglinux-1.1-1.el9.aarch64.rpm
```

### removing rpm

```
rpm -e learninglinux-1.1-1.el9.aarch64
```

### common commands
- query an installed package
```
[root@localhost ~]# rpm -q learninglinux				//查询指定包是否安装
[root@localhost ~]# rpm -qa |grep learninglinux   
[root@localhost ~]# rpm -ql learninglinux				//查询learninglinux安装的文件   	
[root@localhost ~]# rpm -qf /usr/bin/learningLinux_bin	//查询该文件属于哪个rpm包
[root@localhost ~]# rpm -qi learninglinux				//查询包的information
[root@localhost ~]# rpm -qc openssh				        //查询某个包安装的配置文件
[root@localhost ~]# rpm -qd openssh					    //查询某个包安装的帮助文档
```
- query an uninstall package file

```
[a@localhost build]$ rpm -qlp learninglinux-1.1-1.el9.aarch64.rpm
```
>-p, --package `PACKAGE_FILE`
 Query an (uninstalled) package `PACKAGE_FILE`.  
 The PACKAGE_FILE may be specified as an ftp or http style URL, in  which case  the  package  header will be downloaded and queried.  

----

### building rpm packages
>yum install -y rpmdevtools rpmlint

- download source code
```
wget https://github.com/iubuntu/learningLinux/archive/refs/tags/v1.1.tar.gz
tar xf v1.1.tar.gz
cd learningLinux-1.1
mkdir build
cd build
```
- cmake
```
cmake ../
```

- build rpm 
```
cpack -G RPM
```

## yum / dnf
> DNF  is the next upcoming major version of YUM, a package manager for RPM-based Linux distributions. 

### Fixing dependencies
- error example
```
[root@localhost ~]# rpm -ivh sysstat-12.5.4-7.el9.aarch64.rpm
error: Failed dependencies:
	libpcp.so.3()(64bit) is needed by sysstat-12.5.4-7.el9.aarch64
	libpcp.so.3(PCP_3.22)(64bit) is needed by sysstat-12.5.4-7.el9.aarch64
	libpcp_import.so.1()(64bit) is needed by sysstat-12.5.4-7.el9.aarch64
	libpcp_import.so.1(PCP_IMPORT_1.0)(64bit) is needed by sysstat-12.5.4-7.el9.aarch64
	libsensors.so.4()(64bit) is needed by sysstat-12.5.4-7.el9.aarch64
```

### Repositories
#### defaults repo
```
[root@localhost ~]# dnf repolist
repo id                                                   repo name
appstream                                                 CentOS Stream 9 - AppStream
baseos                                                    CentOS Stream 9 - BaseOS
extras-common                                             CentOS Stream 9 - Extras packages
```

- BaseOS

Content in the BaseOS repository consists of the core set of the underlying operating system functionality that provides the foundation for all installations. This content is available in the RPM format and is subject to support terms similar to those in earlier releases of RHEL.

- AppStream

Content in the AppStream repository includes additional user-space applications, runtime languages, and databases in support of the varied workloads and use cases.

#### installing third repos
- [MySQL repo](https://dev.mysql.com/downloads/repo/yum/)

```
yum install https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm
```
- new repos
```
[root@localhost ~]# ls -lha /etc/yum.repos.d/
total 36K
drwxr-xr-x.   2 root root  152 May 14 15:20 .
drwxr-xr-x. 130 root root 8.0K May 14 14:40 ..
-rw-r--r--.   1 root root 4.2K Jan 20 01:27 centos-addons.repo
-rw-r--r--.   1 root root 2.6K Jan 20 01:27 centos.repo
-rw-r--r--.   1 root root 2.9K Apr 22 19:42 mysql-community-debuginfo.repo
-rw-r--r--.   1 root root 2.5K Apr 22 19:42 mysql-community.repo
-rw-r--r--.   1 root root 2.7K Apr 22 19:42 mysql-community-source.repo
[root@localhost ~]# dnf repolist
repo id                                                           repo name
appstream                                                         CentOS Stream 9 - AppStream
baseos                                                            CentOS Stream 9 - BaseOS
extras-common                                                     CentOS Stream 9 - Extras packages
mysql-8.4-lts-community                                           MySQL 8.4 LTS Community Server
mysql-connectors-community                                        MySQL Connectors Community
mysql-tools-8.4-lts-community                                     MySQL Tools 8.4 LTS Community
```

### Installing packages

```
dnf install <package_name_1> <package_name_2> ....
```

```
[root@localhost build]# dnf install learninglinux-1.1-1.el9.aarch64.rpm sysstat

Last metadata expiration check: 0:14:18 ago on Tue 14 May 2024 15:21:59.
Dependencies resolved.
========================================================================================================================================
 Package                            Architecture               Version                            Repository                       Size
========================================================================================================================================
Installing:
 learninglinux                      aarch64                    1.1-1.el9                          @commandline                     10 k
 sysstat                            aarch64                    12.5.4-7.el9                       appstream                       452 k
Installing dependencies:
 lm_sensors-libs                    aarch64                    3.6.0-10.el9                       appstream                        42 k
 pcp-conf                           aarch64                    6.2.1-1.el9                        appstream                        29 k
 pcp-libs                           aarch64                    6.2.1-1.el9                        appstream                       625 k

Transaction Summary
========================================================================================================================================
Install  5 Packages

Total size: 1.1 M
Total download size: 1.1 M
Installed size: 3.7 M
Is this ok [y/N]: y
Downloading Packages:
```
### removing packages
```
dnf remove learninglinux
```

### Reference
- [DNF](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/managing_software_with_the_dnf_tool/index)
- [dnf command list](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/managing_software_with_the_dnf_tool/index#assembly_yum-commands-list_managing-software-with-the-dnf-tool)
