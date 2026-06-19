# Day 1 Linux Practice Notes
Date: Mon Jun  8 15:20:35 HKT 2026

## Basic Commands Learned
- TAB key

### Navigation
- pwd : 
- ls :
- ls -la :


### File & Folder
- mkdir test-folder
- cd test-folder
- touch test-file.txt
- ls

- df 
- df --all
- df -hi -all (Inode -data structure // File ID Card included owener permission data blocks pointer..etc, excluded file name)

### Two types of commands 
- executed files on the disk (type df, type apt)
- shell built in command (type cd, type alias, type umask)

### Net-tools
- ifconfig 

output:
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500 (network interface, up, wifi)
        inet 172.17.225.166  netmask 255.255.240.0  broadcast 172.17.239.255 (ip,subnet mask,broadcast)
        inet6 fe80::215:5dff:fe85:ece2  prefixlen 64  scopeid 0x20<link>
        ether 00:15:5d:85:ec:e2  txqueuelen 1000  (Ethernet) (Mac address)
        RX packets 6761  bytes 55633137 (55.6 MB) (RX = receive)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 6534  bytes 881118 (881.1 KB) (TX = Transmit)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536 (Loop back to localhost)
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 12853  bytes 42765982 (42.7 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 12853  bytes 42765982 (42.7 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


###  Short keys

- Ctrl + C,Cancel /  (kill the process)
- Ctrl + Z,Zuspend / (stop the process)
- Ctrl + D,Done / (sign out) 
- Ctrl + L,Clear / (clean the terminal)
- Ctrl + A,Ahead / (go to beginging)
- Ctrl + E,End / (go to the end)
- Ctrl + U,Unload / (delete a line)
- Ctrl + K,Kill / (clean all after the cursor)
- Ctrl + W,Word / (delete a word before )
- Ctrl + R,Reverse search / (search for command history)