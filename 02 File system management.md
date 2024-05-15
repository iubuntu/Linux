# File Hierarchy Standard
```
[a@localhost ~]$ ls /
afs  bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```
## Common directories

| Directory                                              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/`                                                    | _Primary hierarchy_ root and [root directory](https://en.wikipedia.org/wiki/Root_directory "Root directory") of the entire file system hierarchy.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `/bin`                                                 | Essential command [binaries](https://en.wikipedia.org/wiki/Executable "Executable") that need to be available in [single-user mode](https://en.wikipedia.org/wiki/Single-user_mode "Single-user mode"), including to bring up the system or repair it,[[3]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-3) for all users (e.g., [cat](https://en.wikipedia.org/wiki/Cat_(Unix) "Cat (Unix)"), [ls](https://en.wikipedia.org/wiki/Ls "Ls"), [cp](https://en.wikipedia.org/wiki/Cp_(Unix) "Cp (Unix)")).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `[/boot](https://en.wikipedia.org/wiki//boot "/boot")` | [Boot loader](https://en.wikipedia.org/wiki/Boot_loader "Boot loader") files (e.g., [kernels](https://en.wikipedia.org/wiki/Kernel_(operating_system) "Kernel (operating system)"), [initrd](https://en.wikipedia.org/wiki/Initrd "Initrd")).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `[/dev](https://en.wikipedia.org/wiki//dev "/dev")`    | [Device files](https://en.wikipedia.org/wiki/Device_file "Device file") (e.g., `[/dev/null](https://en.wikipedia.org/wiki/Null_device "Null device")`, `/dev/disk0`,  `/dev/sda1`, `/dev/tty`, `[/dev/random](https://en.wikipedia.org/wiki//dev/random "/dev/random")`).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `/etc`                                                 | Host-specific system-wide [configuration files](https://en.wikipedia.org/wiki/Configuration_file "Configuration file").  <br><br>There has been controversy over the meaning of the name itself. In early versions of the UNIX Implementation Document from Bell Labs, `/etc` is referred to as the _[etcetera](https://en.wikipedia.org/wiki/Et_cetera "Et cetera") directory_,[[4]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-4) as this directory historically held everything that did not belong elsewhere (however, the FHS restricts `/etc` to static configuration files and may not contain binaries).[[5]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-/etc-5) Since the publication of early documentation, the directory name has been re-explained in various ways. Recent interpretations include [backronyms](https://en.wikipedia.org/wiki/Backronym "Backronym")such as "Editable Text Configuration" or "Extended Tool Chest".[[6]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-6) |
| `/home`                                                | Users' [home directories](https://en.wikipedia.org/wiki/Home_directory "Home directory"), containing saved files, personal settings, etc.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `/lib`                                                 | [Libraries](https://en.wikipedia.org/wiki/Library_(computer_science) "Library (computer science)") essential for the [binaries](https://en.wikipedia.org/wiki/Binaries "Binaries") in `/bin` and `/sbin`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `/media`                                               | Mount points for [removable media](https://en.wikipedia.org/wiki/Removable_media "Removable media") such as [CD-ROMs](https://en.wikipedia.org/wiki/CD-ROM "CD-ROM") (appeared in FHS-2.3 in 2004).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `/mnt`                                                 | Temporarily [mounted](https://en.wikipedia.org/wiki/Mount_(computing) "Mount (computing)") filesystems.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `/opt`                                                 | Add-on [application software](https://en.wikipedia.org/wiki/Application_software "Application software") [packages](https://en.wikipedia.org/wiki/Software_package_(installation) "Software package (installation)").[[7]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-/opt-7)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `[/proc](https://en.wikipedia.org/wiki//proc "/proc")` | Virtual [filesystem](https://en.wikipedia.org/wiki/File_system "File system") providing [process](https://en.wikipedia.org/wiki/Process_(computing) "Process (computing)") and [kernel](https://en.wikipedia.org/wiki/Kernel_(operating_system) "Kernel (operating system)") information as files. In Linux, corresponds to a [procfs](https://en.wikipedia.org/wiki/Procfs "Procfs") mount. Generally, automatically generated and populated by the system, on the fly.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `/root`                                                | [Home directory](https://en.wikipedia.org/wiki/Home_directory "Home directory") for the [root](https://en.wikipedia.org/wiki/Superuser "Superuser") user.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `/run`                                                 | Run-time variable data: Information about the running system since last boot, e.g., currently logged-in users and running [daemons](https://en.wikipedia.org/wiki/Daemon_(computer_software) "Daemon (computer software)"). Files under this directory must be either removed or truncated at the beginning of the boot process, but this is not necessary on systems that provide this directory as a [temporary filesystem](https://en.wikipedia.org/wiki/Temporary_filesystem "Temporary filesystem") ([tmpfs](https://en.wikipedia.org/wiki/Tmpfs "Tmpfs")).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `/sbin`                                                | Essential system binaries (e.g., [fsck](https://en.wikipedia.org/wiki/Fsck "Fsck"), [init](https://en.wikipedia.org/wiki/Init "Init"), [route](https://en.wikipedia.org/wiki/Route_(command) "Route (command)")).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `/srv`                                                 | Site-specific data served by this system, such as data and scripts for web servers, data offered by [FTP](https://en.wikipedia.org/wiki/FTP "FTP") servers, and repositories for [version control systems](https://en.wikipedia.org/wiki/Version_control_systems "Version control systems") (appeared in FHS-2.3 in 2004).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `/sys`                                                 | Contains information about devices, drivers, and some kernel features.[[8]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-/sys-8)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `/tmp`                                                 | [Directory for temporary files](https://en.wikipedia.org/wiki/Temporary_folder "Temporary folder") (see also `/var/tmp`). Often not preserved between system reboots and may be severely size-restricted.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `/usr`                                                 | _Secondary hierarchy_ for read-only user data; contains the majority of ([multi-](https://en.wikipedia.org/wiki/Multi-user "Multi-user"))user utilities and applications. Should be shareable and read-only.[[9]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-9)[[10]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-10)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `/usr/bin`                                             | Non-essential command [binaries](https://en.wikipedia.org/wiki/Executable "Executable") (not needed in [single-user mode](https://en.wikipedia.org/wiki/Single-user_mode "Single-user mode")); for all users.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `/usr/include`                                         | Standard [include files](https://en.wikipedia.org/wiki/Header_file "Header file").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `/usr/lib`                                             | [Libraries](https://en.wikipedia.org/wiki/Library_(computer_science) "Library (computer science)") for the [binaries](https://en.wikipedia.org/wiki/Binaries "Binaries") in `/usr/bin` and `/usr/sbin`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `/usr/lib<qual>`                                       | Alternative-format libraries (e.g., `/usr/lib32` for 32-bit libraries on a 64-bit machine (optional)).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `/usr/local`                                           | _Tertiary hierarchy_ for local data, specific to this host. Typically has further subdirectories (e.g., `bin`, `lib`, `share`).[[NB 1]](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard#cite_note-11)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `/usr/sbin`                                            | Non-essential system binaries (e.g., [daemons](https://en.wikipedia.org/wiki/Daemon_(computer_software) "Daemon (computer software)") for various [network services](https://en.wikipedia.org/wiki/Network_service "Network service")).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `/var`                                                 | Variable files: files whose content is expected to continually change during normal operation of the system, such as logs, spool files, and temporary e-mail files.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `/var/lib`                                             | State information. Persistent data modified by programs as they run (e.g., databases, packaging system metadata, etc.).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `/var/log`                                             | Log files. Various logs.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
## PATH

## Absolute Path-name
- Start at the root directory ( / ) and work down
## Relative path
- The path is related to the present working directly(pwd). 
- Start at the current directory and **never starts with a /** .

```
[a@localhost ~]$ cat a.txt
a.txt under home
[a@localhost ~]$ cat /a.txt
a.txt under root
[a@localhost ~]$ cat ./a.txt
a.txt under home
[a@localhost ~]$ cat ~/a.txt
a.txt under home
[a@localhost ~]$ cat /home/a/a.txt
a.txt under home
```

| Punctuation | meaning                                   |
| ----------- | ----------------------------------------- |
| `.`         | the current directory                     |
| `..`        | the parent directory                      |
| `~`         | the `HOME` directory for the current user |
| `/`         | the `root` directory                      |
-  change directory
> **cd** => Change the current directory to dir.  if dir is not supplied, the value of the `HOME` shell variable is the default.
```bash
[a@localhost ~]$ cd /etc
[a@localhost etc]$ pwd
/etc
[a@localhost etc]$ cd ~
[a@localhost ~]$
[a@localhost home]$ pwd
/home
[a@localhost home]$ cd
[a@localhost ~]$ pwd
/home/a
```

An argument of `-` is converted to `$OLDPWD` before the directory change is attempted.
```
[a@localhost ~]$ echo $OLDPWD
/home
[a@localhost ~]$ cd -
/home
```
# File operation commands
## create a file
- touch 
## create a directory
- mkdir
```
-m, --mode=MODE
	  set file mode (as in chmod), not a=rwx - umask

-p, --parents
	  no error if existing, make parent directories as needed
```

## copy
- cp
> copy files and directories

### SYNOPSIS
```
cp [OPTION]... [-T] SOURCE DEST
cp [OPTION]... SOURCE... DIRECTORY
cp [OPTION]... -t DIRECTORY SOURCE...
```

| option                 | description                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| -f, --force            | if an existing destination file cannot be opened, remove it and try again (this option is ignored when the -n option is also used)    |
| -R, -r, --recursive    | copy directories recursively                                                                                                          |
| -v, --verbose          | explain what is being done                                                                                                            |
| --preserve[=ATTR_LIST] | preserve the specified attributes (default: mode,ownership,timestamps), if possible additional attributes: context, links, xattr, all |
| -a, --archive          | same as -dR --preserve=all                                                                                                            |
## move
- mv 
> move (rename) files

| option        | meaning                          |
| ------------- | -------------------------------- |
| -v, --verbose | explain what is being done       |
| -f, --force   | do not prompt before overwriting |


## remove
- rm
> Remove (unlink) the FILE(s).

```
-f, --force
	  ignore nonexistent files and arguments, never prompt

-i     prompt before every removal
-d, --dir
	  remove empty directories
```


## read files
- cat / tac
- less
- more
- head / tail

```
# head  /etc/passwd
# head -2 /etc/passwd
# tail /etc/passwd
# tail -1 /etc/passwd
# tail -f /var/log/messages  	
```

## search file content
- grep
>  grep, egrep, fgrep - print lines that match patterns

```
[a@localhost ~]$ grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin 
```
- count
```
[a@localhost ~]$ grep -c root /etc/passwd
2
```

- recursive
```
[a@localhost ~]$ grep -r  PATH .
./.bashrc:if ! [[ "$PATH" =~ "$HOME/.local/bin:$HOME/bin:" ]]
./.bashrc:    PATH="$HOME/.local/bin:$HOME/bin:$PATH"
./.bashrc:export PATH
grep: ./.cache/gstreamer-1.0/registry.aarch64.bin: binary file matches
grep: ./.cache/gnome-software/appstream/components.xmlb: binary file matches
grep: ./.cache/mozilla/firefox/1e99v5rp.default-default/startupCache/scriptCache.bin: binary file matches
grep: ./.cache/mozilla/firefox/1e99v5rp.default-default/startupCache/scriptCache-child.bin: binary file matches
grep: ./.cache/mozilla/firefox/1e99v5rp.default-default/startupCache/startupCache.8.little: binary file matches
./.bash_history:echo ${PATH}
./.bash_history:printf ${PATH}
./.bash_history:echo ${PATH}
./.bash_history:echo ${PATH}
./.bash_history:echo ${PATH}
```
- line number
```
[a@localhost ~]$ grep -n root /etc/passwd
1:root:x:0:0:root:/root:/bin/bash
10:operator:x:11:0:operator:/root:/sbin/nologin
```

## Edit files
- vi

