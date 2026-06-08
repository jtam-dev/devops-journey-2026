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

Ctrl + C,Cancel / Cut,"""C 就係 Cancel，緊急剎車！""",中斷指令（最重要）
Ctrl + Z,Zuspend / Zzz,"""Z 就係瞓覺，暫停程式""",暫停指令（放 background）
Ctrl + D,Done / Delete,"""D 就係 Done，登出/退出""",登出 Terminal
Ctrl + L,Lean / List clear,"""L 就係 Clean 螢幕，好似抹枱""",清屏（代替 clear）
Ctrl + A,All the way to Ahead,"""A = 最 A頭（Beginning）""",跳到行首
Ctrl + E,End,"""E = End，最尾""",跳到行尾
Ctrl + U,Unload / Up,"""U = 清晒 Up面全部""",清空整行
Ctrl + K,Kill,"""K = Kill 殺到尾""",刪除游標之後所有字
Ctrl + W,Word,"""W = 刪一個 Word""",刪除前一個單詞
Ctrl + R,Reverse search,"""R = Recall，回憶之前打過嘅指令""",搜尋歷史指令（最強）