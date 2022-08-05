# Network & Directory Scanning
---
## Network Scanning
`sudo nmap -sC -sV -oN nmap/initial $IP`

- threader3000
---
## Directory Scanning
`gobuster dir --url <ip/url> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`

`gobuster dir --url <ip/url> -w /usr/share/wordlists/dirb/common.txt`

`ffuf -u /FUZZ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/big.txt`
