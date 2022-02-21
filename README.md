# Part 1 General Knowledge

## 1) ps -ef | grep python | wc -l
 
#### 1. basic linux syntax *comand * --/- switch for commands options
```
ps -e or -a           show all process 
ps -f                 full-format, including command lines
```
![image](https://user-images.githubusercontent.com/47614594/154872675-bcd18ea0-f4e6-47c9-914c-9f27bb1915e2.png)

* UID – numeric user ID. 0 - root , 1-100 demons, >100 users
* PID – This is the unique process ID. PID 0 - swapper/sched - used to control memory. PID 1 - Init - Open other process. 
This number may be used as a parameter in various function calls, allowing processes to be manipulated, such as adjusting the process's priority or killing it altogether. 

* TTY – This is the typeof terminal that the user is logged in to
* TIME – This is the time in minutes and seconds that the process has been running
* CMD – The command that launched the process

```|``` in linux send output from privius commnad to next command

#### 2. ``` grep python``` - Usage: grep [OPTION]... PATTERNS [FILE]...

![image](https://user-images.githubusercontent.com/47614594/154873647-21eabab4-eccc-4a33-9eea-f9d7ce554a07.png)


Search for PATTERNS in each FILE.
Example: grep -i 'hello world' menu.h main.c

PATTERNS can contain multiple patterns separated by **newlines**. - _this newlines will be uesd in wc_

#### 3. ```  wc -l, --lines            print the newline counts```- Usage: wc [OPTION]... [FILE]... 

![image](https://user-images.githubusercontent.com/47614594/154873728-5e54cb85-79d7-4d0b-8177-a6e13d0a0fba.png)

**Print newline**, word, and byte **counts** for each FILE, and a total line if
more than one FILE is specified.

#### Summary: 
1. ps list all proces and send this informations
2. grep looking for given phrase and show only lines with given word 
3. wc -l cout all new lines on screan (grep show 3 lines - output 3)

## 2) Is 172.56.23.5 a public or private IP address?
a) it's a IPv4 Adress 
![image](https://user-images.githubusercontent.com/47614594/154874690-a4c2d397-a3a7-4e45-a402-97546a06335b.png)

we need to remeber about 127.0.0.1 – 127.255.255.254 (loopback) and 169.254.0.1 – 169.254.255.254 (ang. Local-Link) or 192.0.2.0 – 192.0.2.254 (ang. Test-Net)

it's out of private range (+those special one) it mean it'a public IP. This ip belond to  OrgName: T-Mobile USA, Inc. :) 

## 3) How many IP address are available in this subnet 192.168.0.0 / 28

number of 1 in mask - 28

number 0 in mask = 32-28=**4**

Number of host = 2^**4**-2=16-2=14 // we need to decrease by 2 beasue 192.168.0.0 is network address, and a 192.168.0.15 is brodcast.

## 4) lsof | grep /tmp 2>&1 | awk {'print $2'} | sort -u

#### 1. lsof is a command meaning "list open files", which is used in many Unix-like systems to report a list of all open files and the processes that opened them. 

Open files in the system include disk files, named pipes, network sockets and devices opened by all processes. One use for this command is when a disk cannot be unmounted because (unspecified) files are in use. The listing of open files can be consulted (suitably filtered if necessary) to identify the process that is using the files. 

![image](https://user-images.githubusercontent.com/47614594/154877179-f29e6a1c-fbcc-427e-8c47-7ab61a1186f3.png)

#### 2. grep /tmp 2>&1 

> standard solutions and outputs in linux outputs are numbered (STDIN - 0 STDOUT - 1, DERR - 2), to redirect one of them to the other, you need to fill in the spare (2> 1 redirect STDERR STDOUT, 1> & 2 redirect STDOUT to STDERR etc.) .
> The whole thing can be explained as: Redirect standard error entries to standard games, and redirect standard games to null.


It mean that typical serching "/tmp" 
![image](https://user-images.githubusercontent.com/47614594/154877995-e3b5bf24-ef26-43c0-8ae9-69cc997af769.png)

but now "2>&1 " Redirect DERR(error messages) in to normal nomralout. **It mean our commnand collect errors AND a normal output. **
#### 3. awk {'print $2'}

AWK is a domain-specific language designed for text processing and typically used as a data extraction and reporting tool.

syntax: awk options 'selection _criteria {action }' input-file > output-file

awk {'print $2'} - use command print to show result on termina, $2 contain hole info in 2nd column. (in our command 2nd column is a PID-expalained before).

![image](https://user-images.githubusercontent.com/47614594/154880257-80b40fb7-c7da-448f-8867-132d359fb446.png)

#### 4. sort -u

Write sorted concatenation of all FILE(s) to standard output.
Usage: sort [OPTION]... [FILE]...

```sort  -u, --unique              with -c, check for strict ordering;```

![image](https://user-images.githubusercontent.com/47614594/154880621-7510f80c-51a6-4f63-868e-8425f9f41196.png)

_**On end i can guess**_: we collect all open files/network sockets/etcetras in system, we filter those informations to find only form /temp, then we try to collet all notworking "process" **instead**/with insted normal one. Then we collest just PID of notworking process, last step will be sort and take uniqe PIDS.  

## 5) How would you check the status of a service running on a centos 8 machine?

ofcourse service --status-all is deprecated

i will use: 

```systemctl
systemctl | more
systemctl | grep httpd
systemctl list-units --type service
systemctl list-units --type mount
```

OR
```
systemctl list-unit-files
```
i can use command 

```systemd-cgtop``` to see if service dosen't take 99% of cpu 

i use few times in my work experiance this command : 

```systemctl status *service name*```

## 5) If I wanted to set a static IP address on an interface which should be persisted over reboot, should I use the command

ipconfig - used in windows - NOT ONE I MADE A MISTAKE :D 

ifconfig - it wille be lost after reboot - it can be fixed by:

modify configuration files like /etc/network/interfaces. For example, to disable an interface you can simply remove its config part from the file.

Content of /etc/network/interfaces:
```
iface eth0 inet static
address <ip_address>
netmask <network_mask>
gateway <gateway_ip>
````

Then we need to reload a interaface 
```
sudo systemctl restart networking.service
```

for centos and redhat linux - https://devconnected.com/how-to-change-ip-address-on-linux/ 

nmcli - is used in AlmaLinux or centos exp. to reset interface - https://www.layerstack.com/resources/tutorials/How-to-restart-Network-Interface-or-Network-Adapter-on-Linux-and-Windows-Cloud-Servers
```
# nmcli networking off
# nmcli networking on
or
# systemctl restart NetworkManager - AlmaLinux
# systemctl restart NetworkManager.service - centos
```
