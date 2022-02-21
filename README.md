# Part 1 General Knowledge

## 1. ps -ef | grep python | wc -l
 
1. basic linux syntax *comand * --/- switch for commands options
```
ps -e or -a           show all process 
ps -f                 full-format, including command lines
```
![image](https://user-images.githubusercontent.com/47614594/154872675-bcd18ea0-f4e6-47c9-914c-9f27bb1915e2.png)

* PID – This is the unique process ID. 
* PID 0 - swapper/sched - used to control memory. PID 1 - Init - Open other process. 
This number may be used as a parameter in various function calls, allowing processes to be manipulated, such as adjusting the process's priority or killing it altogether. 

* TTY – This is the typeof terminal that the user is logged in to
* TIME – This is the time in minutes and seconds that the process has been running
* CMD – The command that launched the process

```|``` in linux send output from privius commnad to next command

2. ``` grep python``` - Usage: grep [OPTION]... PATTERNS [FILE]...

![image](https://user-images.githubusercontent.com/47614594/154873647-21eabab4-eccc-4a33-9eea-f9d7ce554a07.png)


Search for PATTERNS in each FILE.
Example: grep -i 'hello world' menu.h main.c

PATTERNS can contain multiple patterns separated by **newlines**. - _this newlines will be uesd in wc_

3. ```  wc -l, --lines            print the newline counts```- Usage: wc [OPTION]... [FILE]... 

![image](https://user-images.githubusercontent.com/47614594/154873728-5e54cb85-79d7-4d0b-8177-a6e13d0a0fba.png)

**Print newline**, word, and byte **counts** for each FILE, and a total line if
more than one FILE is specified.

### Summary: 
1. ps list all proces and send this informations
2. grep looking for given phrase and show only lines with given word 
3. wc -l cout all new lines on screan (grep show 3 lines - output 3)