```
@root
   11  useradd user1
   12  useradd user2
   13  useradd user3
   14  id user1

   17  groupadd rd
   18  groupadd sa
   19  groupadd se
   20  groupadd sales
   21  id user1
   22  ls -l /etc/group
   23  vi /etc/group

   25  id user1
   27  vipw
   29  tail /etc/passwd
   30  tail /etc/group
   31  clear
   37  passwd user1

@centos
   98  sudo su -
  102  su
  104  su -

  110  ssh user1@localhost
  131  echo 123 > 123.txt
  132  cat 123.txt
  133  echo 456 >> 123.txt
  134  cat 123.txt
  135  tac 123.txt

  139  date
  142  date "+%Y%m%d"
  143  man date
  ```  
  ### su  

使用 su 指令可以切換到指定的帳號，su 若加入 -（su -）代表要完全切換到目標帳號（亦取代目前登入帳號之所有環境變數）。

一般使用要切換到到其它帳號必須要有目標之密碼，root 則不限制。

### date  

date 可以顯示系統目前時間，透過格式化參數可以修改輸出項目。

可用的格式化參數可以使用下列方式取得：

```centos$ man date```  

### 練習  
Output spec: ```20190306-145031```  
```centos$ date "+%Y%m%d-%H%M%S"```  

### free  

使用 free 可以顯示系統記憶體狀態，透過 -h 或 -m 參數可以把數值自動轉為最合適的單位表示或以 MB 來表示。

### 練習  
```
centos$ free -m
              total        used        free      shared  buff/cache   available
Mem:           1839        1034         106          66         698         531
Swap:          2047         144        1903
```
以上輸出中，系統總記憶體為 1839MB，已經使用 1034MB。


### top  
```top``` 可以檢示系統目前運作狀態

### 練習  
```
centos$ top  
top - 16:40:01 up 374 days, 16:31,  1 user,  load average: 0.00, 0.01, 0.05
Tasks: 121 total,   1 running, 120 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  6.2 sy,  0.0 ni, 93.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  1883560 total,   109256 free,  1057360 used,   716944 buff/cache
KiB Swap:  2097136 total,  1949132 free,   148004 used.   546168 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND     
    1 root      20   0  190852   2600   1552 S  0.0  0.1  74:24.82 systemd     
    2 root      20   0       0      0      0 S  0.0  0.0   0:00.85 kthreadd    
    3 root      20   0       0      0      0 S  0.0  0.0   3:32.72 ksoftirqd/0
  ```

以上輸出中：

* 系統 1m, 5m, 15m（m 為分鐘）負載為 0.00, 0.01, 0.05  
* 系統閒置率為 93.8  
* 系統有 1 個登入者  
* 系統有 121 個行程  
* 系統有 1 個行程正在運作  
* 系統有 120 個行程進入睡眠等待呼叫  


### df  
df 可以檢視目前系統磁碟使用狀態

### 練習  
```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/vda1        40G   17G   21G  44% /
devtmpfs        911M     0  911M   0% /dev
tmpfs           920M     0  920M   0% /dev/shm
tmpfs           920M  105M  816M  12% /run
tmpfs           920M     0  920M   0% /sys/fs/cgroup
/dev/sda         20G   18G  2.4G  89% /MDDATA
tmpfs           184M     0  184M   0% /run/user/1000
```
* 系統根目錄 / 共有 40G 空間，已使用 44%  
* /DATA 尚有 18G 空間可以使用  
