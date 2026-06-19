# Day 3 - Linux Basics (2026-06-13)

## Learning Objectives
- "cut" & "tee" command
- Finding Files and Directories ("which","plocate","found")
- Find and Exec 
- Searching for String Patterns in Text Files (grep)


## Source
*data.txt*
John,25,Developer
Jane,30,Designer
Jack,22,Analyst

### "cut" command  : extract the exact specific sections from each line of input 
- `cut -d',' -f1 data.txt`: `-d ','` (delimiter is a comma ,) ; `-f1` (get the first field)

*terminal*
John
Jane
Jack

### "tee" command : reads from standard input and writes to both standard output (the screen) and a file
- `ls | tee output.txt` : read ls and writes to terminal & the output.txt *two output*

*terminal & output.txt*
README.md
day1-linux-notes.md
day2-linux-notes.md
day3-linux-notes.md
data.txt

### Finding Files and Directories ("which","plocate","found")
- which: *only locates executable files* that are in your system's *PATH*
- `which rm` : /usr/bin/rm
- `which -a find` : `-a` = all location , /usr/bin/find  /bin/find

- plocate: is fast, as it searches a pre built database - *all files* on the systems but maybe outdated (from db)
- `sudo apt install plocate` , `sudo updatedb` : install & update plocate db
- `plocate passwords`:/usr/lib/python3/dist-packages/cloudinit/config/set_passwords.py....etc
*basename* : basename /home/jason/devops-journey-2026/day3-linux-notes.md  = day3-linux-notes
- `plocate swords`: `-b` (basename) , search from basename ; /usr/lib/python3/dist-packages/cloudinit/config/set_passwords.py

- find: is the most powerful and versatile but slower, as it searches in real-time on the filesystem
*by name*
- `find . -name data.txt`: find from current directory by name -> ./data.txt
- `sudo find /etc/ -name passwd`: find from /etc/ by bame -> /etc/passwd & /etc/pam.d/passwd

*by type*
- `find /etc/ -type d -maxdepth 2 -perm 755|wc -l` : `-d` directory only;  `maxdepth 2` itself and one level of subdirectories below it; `perm 755` permission bits = 755 (learn later) ; wc -l count how many lines of output
- `find /var -type f -size 100k -ls`: files exactly 100kilobytes in longlist

*by time*
- `find /var -type f -mtime 0 -ls`: files modified within 24 hours

*by user*
- `sudo find /var/ -type f -user jason -ls`: files owned by user 'jason'

### Find and Exec ###
- `sudo find /etc -type f -mtime 0 -exec cat {} \`: Executes 'cat'  on each file found, where {} is the placeholder for the current file and \; signifies the end of the command 

- `sudo find /etc/ -type f -mtime -7 -exec cp {} /root/backup \;`: copy last 7 days data to /root/backup

### Searching for String Patterns in Text Files (grep) ### 

- `grep "user" /etc/ssh/ssh_config`: search "user" 
- `grep -i "SSH" /etc/ssh/ssh_config` :`-i` search "ssh" ignore case(case insensitive)
- `grep -i -n "SSH" /etc/ssh/ssh_config` : `-n` show line numbers along with matching result
- `sudo grep -R "127.0.0.1" /etc/` : `-R` searches all files and directories (/etc/ & all files & directories below /etc/)
- `grep "error" /var/log/syslog | wc -l` || `grep -c error /var/log/syslof`: `-c` count the number of matching lines

*The Kernel Ring Buffer* is like the "Black Box Flight Recorder" of your Linux server. It is a highly protected, small slice of memory (RAM) where the Linux Kernel immediately logs everything happening at the lowest level of the computer.

- `dmesg|grep -A 3 -B 4 "error"` :  display message -> "Kernal Ring Buffer" ;`-A` after 3 lines , `-B` before 4 lines
- `sudo ss -tupan | grep "53"` : check netstat, -tupan  (tcp, udp ,pid ,all ,number)


