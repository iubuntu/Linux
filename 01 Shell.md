# Bash
> Bash is an sh-compatible command language `interpreter` that executes commands read from the standard input or from a file.

> GNU Bourne-Again SHell

The improvements offered by Bash include:

- command-line editing,
- unlimited size command history,
- job control,
- shell functions and aliases,
- indexed arrays of unlimited size,
- integer arithmetic in any base from two to sixty-four.
## PROMPTING
```
[a@localhost ~]$
[a@localhost ~]$ echo $PS1
[\u@\h \W]\$
```
- `\u`     the username of the current user 
- `\h`     the hostname up to the first `.'
- `\W`     the `basename` of the current working directory, with `$HOME` abbreviated with a [[Punctuation#^b43454 | tilde]] (~)

You can find the all supported special characters at [[PROMPTING characters]]

---
# Syntax 
> `command` `[options]` `[parameters]`

-  The `ls` command
> list directory contents
```bash
[a@localhost ~]$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```
- The command with an option `-l` 
```bash
[a@localhost ~]$ ls -l
total 0
drwxr-xr-x. 2 a a  6 May  5 11:41 Desktop
drwxr-xr-x. 2 a a  6 May  5 11:41 Documents
drwxr-xr-x. 3 a a 17 May  5 13:39 Downloads
drwxr-xr-x. 2 a a  6 May  5 11:41 Music
drwxr-xr-x. 2 a a  6 May  5 11:41 Pictures
drwxr-xr-x. 2 a a  6 May  5 11:41 Public
drwxr-xr-x. 2 a a  6 May  5 11:41 Templates
drwxr-xr-x. 2 a a  6 May  5 11:41 Videos
```
> `-l` => use a long listing format
- The command with an option `-l` and a parameter `a.txt`
```
[a@localhost ~]$ touch a.txt
[a@localhost ~]$ ls -l a.txt
-rw-r--r--. 1 a a 0 May  7 14:11 a.txt
```
- The command with more than one option `-l`, `-h`, and `-a`
```
[a@localhost ~]$ ls -lha
total 36K
drwx------. 14 a    a    4.0K May  7 14:11 .
drwxr-xr-x.  3 root root   15 May  5 11:40 ..
-rw-r--r--.  1 a    a       0 May  7 14:11 a.txt
-rw-------.  1 a    a    1.7K May  6 06:50 .bash_history
-rw-r--r--.  1 a    a      18 Feb 16 02:31 .bash_logout
-rw-r--r--.  1 a    a     141 Feb 16 02:31 .bash_profile
-rw-r--r--.  1 a    a     492 Feb 16 02:31 .bashrc
drwx------. 12 a    a    4.0K May  6 14:40 .cache
drwxr-xr-x.  9 a    a    4.0K May  6 06:50 .config
drwxr-xr-x.  2 a    a       6 May  5 11:41 Desktop
drwxr-xr-x.  2 a    a       6 May  5 11:41 Documents
drwxr-xr-x.  3 a    a      17 May  5 13:39 Downloads
-rw-------.  1 a    a     112 May  7 14:10 .lesshst
drwx------.  5 a    a      43 May  5 14:01 .local
drwxr-xr-x.  5 a    a      54 May  5 11:45 .mozilla
drwxr-xr-x.  2 a    a       6 May  5 11:41 Music
drwxr-xr-x.  2 a    a       6 May  5 11:41 Pictures
drwxr-xr-x.  2 a    a       6 May  5 11:41 Public
drwxr-xr-x.  2 a    a       6 May  5 11:41 Templates
drwxr-xr-x.  2 a    a       6 May  5 11:41 Videos
-rw-------.  1 a    a    2.3K May  5 14:41 .viminfo
[a@localhost ~]$ ls -l -h -a
total 36K
drwx------. 14 a    a    4.0K May  7 14:11 .
drwxr-xr-x.  3 root root   15 May  5 11:40 ..
-rw-r--r--.  1 a    a       0 May  7 14:11 a.txt
-rw-------.  1 a    a    1.7K May  6 06:50 .bash_history
-rw-r--r--.  1 a    a      18 Feb 16 02:31 .bash_logout
-rw-r--r--.  1 a    a     141 Feb 16 02:31 .bash_profile
-rw-r--r--.  1 a    a     492 Feb 16 02:31 .bashrc
drwx------. 12 a    a    4.0K May  6 14:40 .cache
drwxr-xr-x.  9 a    a    4.0K May  6 06:50 .config
drwxr-xr-x.  2 a    a       6 May  5 11:41 Desktop
drwxr-xr-x.  2 a    a       6 May  5 11:41 Documents
drwxr-xr-x.  3 a    a      17 May  5 13:39 Downloads
-rw-------.  1 a    a     112 May  7 14:10 .lesshst
drwx------.  5 a    a      43 May  5 14:01 .local
drwxr-xr-x.  5 a    a      54 May  5 11:45 .mozilla
drwxr-xr-x.  2 a    a       6 May  5 11:41 Music
drwxr-xr-x.  2 a    a       6 May  5 11:41 Pictures
drwxr-xr-x.  2 a    a       6 May  5 11:41 Public
drwxr-xr-x.  2 a    a       6 May  5 11:41 Templates
drwxr-xr-x.  2 a    a       6 May  5 11:41 Videos
-rw-------.  1 a    a    2.3K May  5 14:41 .viminfo
```

# Command Search and Execution

After a command has been split into words, if it results in a simple command and an optional list of arguments, the following actions are taken.

1. If the command name contains no slashes, the shell attempts to locate it. If there exists a shell function by that name, that function is invoked as described in [Shell Functions](https://www.gnu.org/software/bash/manual/bash.html#Shell-Functions).
2. If the name does not match a function, the shell searches for it in the list of shell builtins. If a match is found, that builtin is invoked.
3. If the name is neither a shell function nor a builtin, and contains no slashes, Bash searches each element of `$PATH` for a directory containing an executable file by that name. Bash uses a hash table to remember the full pathnames of executable files to avoid multiple `PATH` searches (see the description of `hash` in [Bourne Shell Builtins](https://www.gnu.org/software/bash/manual/bash.html#Bourne-Shell-Builtins)). A full search of the directories in `$PATH` is performed only if the command is not found in the hash table. If the search is unsuccessful, the shell searches for a defined shell function named `command_not_found_handle`. If that function exists, it is invoked in a separate execution environment with the original command and the original command’s arguments as its arguments, and the function’s exit status becomes the exit status of that subshell. If that function is not defined, the shell prints an error message and returns an exit status of 127.
4. If the search is successful, or if the command name contains one or more slashes, the shell executes the named program in a separate execution environment. Argument 0 is set to the name given, and the remaining arguments to the command are set to the arguments supplied, if any.
5. If this execution fails because the file is not in executable format, and the file is not a directory, it is assumed to be a _shell script_ and the shell executes it as described in [Shell Scripts](https://www.gnu.org/software/bash/manual/bash.html#Shell-Scripts).
6. If the command was not begun asynchronously, the shell waits for the command to complete and collects its exit status.
# Shortcut


![visual cheetsheet](https://raw.githubusercontent.com/fliptheweb/bash-shortcuts-cheat-sheet/master/moving_cli.png)

## Moving

| command  | description                    |
|----------|--------------------------------|
| ctrl + a | Goto BEGINNING of command line |
| ctrl + e | Goto END of command line       |
| ctrl + b | move back one character        |
| ctrl + f | move forward one character     |
| alt + f  | move cursor FORWARD one word   |
| alt + b  | move cursor BACK one word      |
| ctrl + xx | Toggle between the start of line and current cursor position |
| ctrl + ] + x	 | Where x is any character, moves the cursor forward to the next occurance of x |
| alt + ctrl + ] + x  | Where x is any character, moves the cursor backwards to the previous occurance of x |

## Edit / Other

| command  | description                    |
|----------|--------------------------------|
| ctrl + d          | Delete the character under the cursor |
| ctrl + h          | Delete the previous character before cursor |
| ctrl + u          | Clear all / cut BEFORE cursor |
| ctrl + k          | Clear all / cut AFTER cursor |
| ctrl + w          | delete the word BEFORE the cursor |
| alt + d           | delete the word FROM the cursor |
| ctrl + y          | paste (if you used a previous command to delete) |
| ctrl + i          | command completion like Tab
| ctrl + l          | Clear the screen (same as clear command) |
| ctrl + c          | kill whatever is running |
| ctrl + d          | Exit shell (same as exit command when cursor line is empty) |
| ctrl + z          | Place current process in background |
| ctrl + _          | Undo |
| ctrl + x ctrl + u	| Undo the last changes. ctrl+ _ does the same |
| ctrl + t          | Swap the last two characters before the cursor |
| esc + t           | Swap last two words before the cursor |
| alt + t           | swap current word with previous |
| esc + .           | |
| esc + _           | |
| alt + [Backspace] | delete PREVIOUS word |
| alt + <           | Move to the first line in the history |
| alt + >           | Move to the end of the input history, i.e., the line currently being entered |
| alt + ?           | display the file/folder names in the current path as help |
| alt + *           | print all the file/folder names in the current path as parameter |
| alt + .           | print the LAST ARGUMENT (ie "vim file1.txt file2.txt" will yield "file2.txt") |
| alt + c           | capitalize the first character to end of word starting at cursor (whole word if cursor is at the beginning of word)|
| alt + u           | make uppercase from cursor to end of word |
| alt + l           | make lowercase from cursor to end of word |
| alt + n           | |
| alt + p           | Non-incremental reverse search of history. |
| alt + r           |Undo all changes to the line|
| alt + ctl + e     |Expand command line. |
| ~[TAB][TAB]       | List all users |
| $[TAB][TAB]       | List all system variables |
| @[TAB][TAB]       | List all entries in your /etc/hosts file |
| [TAB]             | Auto complete |
| cd -              | change to PREVIOUS working directory |

## History

| command  | description                    |
|----------|--------------------------------|
| ctrl + r          | Search backward starting at the current line and moving 'up' through the history as necessary |
| crtl + s          | Search forward starting at the current line and moving 'down' through the history as necessary |
| ctrl + p          | Fetch the previous command from the history list, moving back in the list (same as up arrow) |
| ctrl + n          | Fetch the next command from the history list, moving forward in the list (same as down arrow) |
| ctrl + o          | Execute the command found via Ctrl+r or Ctrl+s |
| ctrl + g          | Escape from history searching mode |
| !!                | Run PREVIOUS command (ie `sudo !!`) |
| !vi               | Run PREVIOUS command that BEGINS with vi |
| !vi:p             | Print previously run command that BEGINS with vi |
| !n		            | Execute nth command in history |
| !$		            | Last argument of last command |
| !^		            | First argument of last command |
| ^abc^xyz	        | Replace first occurance of abc with xyz in last command and execute it |

## References

1. http://cnswww.cns.cwru.edu/php/chet/readline/readline.html
2. https://github.com/fliptheweb/bash-shortcuts-cheat-sheet/blob/master/README.md
