

# Fundamental Concepts

##  Programs 

Programs normally exist in two forms. 
- The first form is source code, human-readable text consisting of a series of statements written in a programming language such as `C`. 
- To be executed, source code must be converted to the second form: `binary` machine-language instructions that the computer can understand.
> A static file in the disk.
## process
A process is an instance of an executing program. 
When a program is executed, the kernel loads the code of the program into virtual memory, and sets up kernel bookkeeping data structures to record various information 
(such as process ID, termination status, user IDs, and group IDs) about the process.
When the process terminates, all such resources are released.

## Process creation and program execution
- A program can create more than one processes
- A process can create more than more child processes via the `fork` system call
	- the parent process calling the `fork`
	- the child process created by the `fork`
- When the parent process exit, all child processes are terminated.

```
[root@localhost ~]# pstree -a | less
...
  |-httpd -DFOREGROUND
  |   |-httpd -DFOREGROUND
  |   |-httpd -DFOREGROUND
  |   |   `-52*[{httpd}]
  |   |-httpd -DFOREGROUND
  |   |   `-52*[{httpd}]
  |   `-httpd -DFOREGROUND
  |       `-68*[{httpd}]
...
[root@localhost ~]# ps -elf | grep httpd
F S UID          PID    PPID  C PRI  NI ADDR SZ WCHAN  STIME TTY          TIME CMD
4 S root        7792       1  0  80   0 -  7412 do_sel 13:58 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
5 S apache      7793    7792  0  80   0 -  7939 skb_wa 13:58 ?        00:00:00 /usr/sbin/httpd -DFOREGROUND
5 S apache      7794    7792  0  80   0 - 543502 pipe_r 13:58 ?       00:00:01 /usr/sbin/httpd -DFOREGROUND
5 S apache      7795    7792  0  80   0 - 543502 pipe_r 13:58 ?       00:00:01 /usr/sbin/httpd -DFOREGROUND
5 S apache      7796    7792  0  80   0 - 592910 pipe_r 13:58 ?       00:00:01 /usr/sbin/httpd -DFOREGROUND
0 S root        8088    7192  0  80   0 - 55358 pipe_r 14:37 pts/0    00:00:00 grep --color=auto httpd
```

---
# Checking processes
## ps
> report a snapshot of the current processes
```
USER: 	运行进程的用户
PID： 	进程ID
%CPU: 	CPU占用率
%MEM: 内存占用率
VSZ：	占用虚拟内存
RSS:  	占用实际内存
TTY： 	进程运行的终端
STAT：	进程状态	 man ps (/STATE)			
	   D    uninterruptible sleep (usually IO)
	   I    Idle kernel thread
	   R    running or runnable (on run queue)
	   S    interruptible sleep (waiting for an event to complete)
	   T    stopped by job control signal
	   t    stopped by debugger during the tracing
	   W    paging (not valid since the 2.6.xx kernel)
	   X    dead (should never be seen)
	   Z    defunct ("zombie") process, terminated but not reaped by its parent

For BSD formats and when the stat keyword is used, additional characters may be displayed:

	   <    high-priority (not nice to other users)
	   N    low-priority (nice to other users)
	   L    has pages locked into memory (for real-time and custom IO)
	   s    is a session leader
	   l    is multi-threaded (using CLONE_THREAD, like NPTL pthreads do)
	   +    is in the foreground process group
		
START:	进程的启动时间
TIME：	进程占用CPU的总时间
COMMAND： 进程文件，进程名   [5]  带中括号的为kernel的不带为用户
```
### common options
```
ps aux
ps -elf
```

### customising the columns
```
[root@localhost ~]# ps axo user,pid,ppid,%mem,command |grep httpd
root        8248       1  0.2 /usr/sbin/httpd -DFOREGROUND
apache      8249    8248  0.2 /usr/sbin/httpd -DFOREGROUND
apache      8250    8248  0.5 /usr/sbin/httpd -DFOREGROUND
apache      8251    8248  0.5 /usr/sbin/httpd -DFOREGROUND
apache      8252    8248  0.4 /usr/sbin/httpd -DFOREGROUND
root        8554    7192  0.0 grep --color=auto httpd
```

## pstree
> display a tree of processes

```
pstree
```
## pgrep
>list the process Id by the  process name
```
[root@localhost ~]# pgrep httpd
8248
8249
8250
8251
8252
```
## pidof
> find the process ID of a running program

```
[root@localhost ~]# pidof httpd
8252 8251 8250 8249 8248
[root@localhost ~]# pidof http
[root@localhost ~]# pgrep http
8248
8249
8250
8251
8252
```

## top
> a  dynamic  real-time  view of a running system

```
[root@station230 ~]# top
[root@station230 ~]# top -d 1
[root@station230 ~]# top -d 1 -p 10126					查看指定进程的动态信息
[root@station230 ~]# top -d 1 -p `pgrep sshd`    	命令替换
[root@station230 ~]# top -d 1 -p $(pgrep sshd)   	命令替换
[root@station230 ~]# top -d 1 -p $(pgrep vino-server),1
[root@station230 ~]# top -d 1 -u apache				查看指定用户的进程
[root@station230 ~]# top -b -n 2 > top.txt 			将2次top信息写入到文件
```

- SUMMARY Display
	- UPTIME and LOAD Averages
	- TASK and CPU States
	- MEMORY Usage
```
top - 15:08:34 up  7:04,  4 users,  load average: 0.03, 0.01, 0.00
Tasks: 257 total,   1 running, 256 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  1.5 sy,  0.0 ni, 98.5 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   3584.2 total,   1424.3 free,   1149.4 used,   1207.0 buff/cache
MiB Swap:   4036.0 total,   4036.0 free,      0.0 used.   2434.8 avail Mem
```
- process information
	- %CPU  --  CPU Usage
	- %MEM  --  Memory Usage (RES)
	- RES  --  Resident Memory Size (KiB)
	- S  --  Process Status
```
    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   8749 root      20   0  226176   3968   3200 R  12.5   0.1   0:00.02 top
      1 root      20   0  175788  15652   9180 S   0.0   0.4   0:02.10 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.04 kthreadd
```

- adjusting the output
```
M	按内存的使用排序
P	按CPU使用排序
N	以PID的大小排序
R	对排序进行反转
f	自定义显示字段
1	显示所有CPU的负载

h|?	帮助
<	向前
>	向后
z	彩色
```
---

# Network process
> Print network connections

```
[root@localhost ~]# netstat -tnlp
-t   tcp
-u  udp
-l   listen
-p  PID/Program name
-n  Show numerical addresses instead of trying to determine symbolic host, port or user names.（80 ---> http）
```
- check the which process is listening on the tcp 80 port
```
[root@localhost ~]#  netstat -tnlp |grep :80
tcp6       0      0 :::80                   :::*                    LISTEN      9766/httpd
[root@localhost ~]# systemctl stop httpd
[root@localhost ~]#  netstat -tnlp |grep :80
```
- check which process is connecting the web
```
[root@localhost ~]# netstat -ap | grep :http
tcp        0      0 localhost.localdo:55026 17.165.36.34.bc.g:https TIME_WAIT   -
tcp        0      0 localhost.localdo:50608 ec2-63-35-152-215:https ESTABLISHED 10167/firefox
tcp        0      0 localhost.localdo:38626 mel04s02-in-f2.1e:https TIME_WAIT   -
tcp        0      0 localhost.localdo:49140 104.17.249.203:https    ESTABLISHED 10167/firefox
tcp        0      0 localhost.localdo:50660 a23-38-166-200.dep:http ESTABLISHED 10167/firefox
```

---
# Signals

A signal is a notice to a process that an event has occurred. They are a lightweight form of IPC that can be sent between processes to handle events like process termination or user-defined events.
When a process received a signal
- it ignores the signal
- it is killed by the signal
- or it is suspended until later being resumed by receipt of a special-purpose signal.

## kill
> Sending a signal in shell

- list all signal
> Print a list of signal names, or convert the given signal number to a name
```
[root@localhost ~]# kill -l
1) SIGHUP 		重启
9) SIGKILL		强制终止
15) SIGTERM	终止（正常退出，干净），缺省信号
[root@localhost ~]# kill -l 9
KILL
[root@localhost ~]# kill -L 11
SEGV
```
- kill a process 
```
[root@localhost ~]# pgrep httpd
9389
9390
9391
9392
9393
[root@localhost ~]# kill 9389 # the parent id of all httpd
[root@localhost ~]# pgrep httpd
[root@localhost ~]# systemctl start httpd
[root@localhost ~]# pgrep httpd
9577
9578
9579
9580
9581
[root@localhost ~]# pkill httpd
[root@localhost ~]# pgrep httpd
[root@localhost ~]# systemctl start httpd
[root@localhost ~]# pgrep httpd
9766
9767
9768
9769
9948
[root@localhost ~]# kill 9948 # one of the child process
[root@localhost ~]# ps aux | grep 9948
apache      9948  0.1  0.4 2239544 17764 ?       Sl   15:35   0:00 /usr/sbin/httpd -DFOREGROUND
[root@localhost ~]# kill -9 9948
[root@localhost ~]# ps aux | grep 9948
```


---
# Job control
```
[root@station230 ~]# sleep 3000 &		//运行程序（时），让其在后台执行
[root@station230 ~]# sleep 4000			//^z,将前台的程序挂起（暂停）到后台
[2]+  Stopped                 sleep 4000

[root@station230 ~]# ps aux |grep sleep
root      8895  0.0  0.0 100900   556 pts/0    S    12:13   0:00 sleep 3000
root      8896  0.0  0.0 100900   556 pts/0    T    12:13   0:00 sleep 4000
[root@station230 ~]# jobs 						//查看后台作业
[1]-  Running                 sleep 3000 &
[2]+  Stopped               sleep 4000

[root@station230 ~]# bg %2					//让作业2在后台运行
[root@station230 ~]# fg %1					//将作业1调回到前台

[root@station230 ~]# nohup sleep 8000 &
[root@station230 ~]# jobs 
[1]-  Running                 nohup sleep 1000 &
[2]+  Stopped               sleep 2000

[root@station230 ~]# kill %1					//kill 1，杀死PID为1的进程

[root@station230 ~]# gedit &
[root@station230 ~]# nohup gedit &		//该进程在运行时，不依赖于任何终端
```








