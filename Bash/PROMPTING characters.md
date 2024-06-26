
 When executing interactively, bash displays the primary prompt PS1 when it is ready to read a command, and the secondary prompt PS2  when  it  needs more  input to complete a command.  Bash displays PS0 after it reads a command but before executing it.  Bash displays PS4 as described above before tracing each command when the -x option is enabled.  Bash allows these prompt strings to be customized by inserting a  number  of  backslash-escaped special characters that are decoded as follows:
```txt
\a     an ASCII bell character (07)
\d     the date in "Weekday Month Date" format (e.g., "Tue May 26")
\D{format}
	 the  format  is  passed to strftime(3) and the result is inserted into the prompt string; an empty format results in a locale-specific
	 time representation.  The braces are required
\e     an ASCII escape character (033)
\h     the hostname up to the first `.'
\H     the hostname
\j     the number of jobs currently managed by the shell
\l     the basename of the shell's terminal device name
\n     newline
\r     carriage return
\s     the name of the shell, the basename of $0 (the portion following the final slash)
\t     the current time in 24-hour HH:MM:SS format
\T     the current time in 12-hour HH:MM:SS format
\@     the current time in 12-hour am/pm format
\A     the current time in 24-hour HH:MM format
\u     the username of the current user
\v     the version of bash (e.g., 2.00)
\V     the release of bash, version + patch level (e.g., 2.00.0)
\w     the current working directory, with $HOME abbreviated with a tilde (uses the value of the PROMPT_DIRTRIM variable)
\W     the basename of the current working directory, with $HOME abbreviated with a tilde
\!     the history number of this command
\#     the command number of this command
\$     if the effective UID is 0, a #, otherwise a $
\nnn   the character corresponding to the octal number nnn
\\     a backslash
\[     begin a sequence of non-printing characters, which could be used to embed a terminal control sequence into the prompt
\]     end a sequence of non-printing characters
```