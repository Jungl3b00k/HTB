## Hack the Box Reference.<br>
Contains commands,Link and tricks for challenges<br>
gzip<br>
gzip -d file.gz<br>

masscan probe to establish the open ports in the host.<br>
#masscan -e tun0 -p1-65535,U:1-65535 10.10.10.101 --rate=700<br>

##nmap scanning the discovered ports to see what are the services.##<br>
#nmap -sV -v -O -sS -T5 <target><br>

##Gobuster Dir enumeration##<br>
```gobuster -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -t 20 -e -x php,htm,html,txt -u http://target<br>

##bypass-bash-restrictions##<br>
https://book.hacktricks.xyz/linux-unix/useful-linux-commands/bypass-bash-restrictions<br>
